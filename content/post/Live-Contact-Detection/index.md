---
title: Live Contact Detection
description: Detecting Touches in Human-Human Interactions (HHI) in Real-Time!
date: 2025-05-01
categories:
  - Exploration
---

## Problem Statement

Human-Human Interactions (HHI) is a huge field. Most of the research in this field is focused on understanding human interactions, activities and their dynamics in a video. And for most of the problems, the solutions include understanding of multiple frames inside a video. Touch detection is a sub-problem of many such problems. It is nothing but the detection of exact point where a person is touching another and at what frame. But it doesn't require understanding of multiple frames. A single frame is sufficient to detect a simple visible touch. Although detecting the touch and predicting the location when it is invisible in the camera is still an unsolved problem. My focus is building a practical real-time solution for the prior problem using only a single image as an input.

## My Approach

Assuming it is a CCTV camera or an ordinary camera with a fixed position and lacking any depth and motion sensors, the only kind of input I have is a series of images from the camera. At a high-level overview, my approach boils down to the following 4 steps:

1. Keypoint or Pose Estimation using [YOLO11x](https://docs.ultralytics.com/models/yolo11/).
2. Metric Depth Estimation using [Apple's Depth-Pro](https://github.com/apple/ml-depth-pro).
3. 2D to 3D coordinate conversion using [my custom algorithm](https://navam9530.github.io/post/mapping-2d-to-3d/).
4. Distance calculation and touch detection using the 3D coordinates.

## 1. Keypoint or Pose Estimation

There are many models for keypoint estimation. Most of them generate 2d keypoints. But for this problem, we need 3D keypoints. At the point of writing this, there is no good 3d model for keypoint estimation. Even there are some, they provide relative 3D points, which are of no use to us. So, I am using a 2D model and then I will convert the 2D coordinates to 3D coordinates using the depth estimation and my custom algorithm.

The current state-of-the-art 2D keypoint estimation model, supporting multiple people, is [YOLO11x](https://docs.ultralytics.com/models/yolo11/). There are 5 models under the YOLO11 family, namely, YOLO11n, YOLO11s, YOLO11m, YOLO11l and YOLO11x. The model with the highest accuracy with a slight tradeoff in speed is YOLO11x. It generates 17 2D keypoints for each person in the image whether it is visible or not. For every point predicted, the model also provides a confidence score. The model outputs very low confidence scores for the invisible or partailly visible keypoints.

## 2. Metric Depth Estimation

Depth Estimation can be classified either as Absolute (Metric) or Relative. Absolute Depth Maps provide the distance of each point measured from the camera. Whereas the Relative Depth Maps provide only the distances between the objects in the scene (unrelated to the camera's position). So, we need Absolute Depth Maps in order to solve our problem.

I recommend [Apple's Depth-Pro](https://github.com/apple/ml-depth-pro) for this task since it is the current state-of-the-art model. It performs absolute depth estimation and provides the output in meters. To access the depth of a point (x, y), use `depth[y, x]`.

## 3. 2D to 3D Coordinate Conversion

I have already written a detailed post on this topic. You can read it [here](https://navam9530.github.io/post/mapping-2d-to-3d/). I will be using my custom algorithm for this step. The algorithm has many applications in the field of computer vision. Read the article to get a complete understanding on how it works or watch the below video for a glimpse of its capabilities.

{{< embed/video src="2d_to_3d.mp4" >}}

The video contains 2 parts arranged vertically. The top part is a footage taken inside a TDM (Team Deathmatch) map of the game BGMI. The bottom part contains the 3D trajectory of the person head plotted inside a 3D model of the same map and visualized in [Intel's Open3D](https://www.open3d.org/). Although the top footage is processed offline, for the sake of demonstration, I have synced them together. This is just one of the many applications possible with the algorithm including this post.

## 4. Distance Calculation and Touch Detection

After getting the 17 3D coordinates for each keypoint of each person present in the image, we can calculate the euclidean distance between each hand keypoint of each person with the keypoints of every other person. If the distance is less than a certain threshold, we can say that there is a touch between those two keypoints. The indices of the keypoints for the hands are 9 and 10. Unfortunately, there is no other method than performing brute-force distance calculation for this step.

## Python Code

Here is a sample python code for live touch detection using the above approach. The code is not optimized for parallel processing and it is just for demonstration purposes. You can optimize it further by using multiprocessing or other techniques.

```python
import cv2
import torch
import depth_pro
import numpy as np
from ultralytics import YOLO

def get_quadrant(x, y, iw, ih):
    xdir = 'Positive' if x >= iw / 2 else 'Negative'
    ydir = 'Positive' if y >= ih / 2 else 'Negative'
    if xdir == 'Positive' and ydir == 'Positive':
        quadrant = 4
    elif xdir == 'Negative' and ydir == 'Positive':
        quadrant = 3
    elif xdir == 'Negative' and ydir == 'Negative':
        quadrant = 2
    else:
        quadrant = 1
    return quadrant

def get_xyz(x, y, iw, ih, fx, d, u, f, c, scale=1):
    fx = np.deg2rad(fx)
    quadrant = get_quadrant(x, y, iw, ih)
    if quadrant == 1:
        alpha = np.arctan(np.tan(fx/2) * (2*x/iw-1))
        beta = np.arctan((ih-2*y)*np.sin(alpha)/(2*x-iw))
    elif quadrant == 2:
        alpha = np.arctan(np.tan(fx/2) * (1-2*x/iw))
        beta = np.arctan((ih-2*y)*np.sin(alpha)/(iw-2*x))
    elif quadrant == 3:
        alpha = np.arctan(np.tan(fx/2) * (1-2*x/iw))
        beta = np.arctan((2*y-ih)*np.sin(alpha)/(iw-2*x))
    else:
        alpha = np.arctan(np.tan(fx/2) * (2*x/iw-1))
        beta = np.arctan((2*y-ih)*np.sin(alpha)/(2*x-iw))
    X = d * np.cos(beta) * np.sin(alpha)
    Y = d * np.sin(beta)
    Z = X / np.tan(alpha)
    o = -Z * f
    if quadrant == 2 or quadrant == 3:
        o -= X * np.cross(u, f)
    else:
        o += X * np.cross(u, f)
    if quadrant == 1 or quadrant == 2:
        o += Y * u
    else:
        o -= Y * u
    p = c + scale * o
    return p

fov = 70
u = np.array([0, 1, 0])
f = np.array([0, 0, 1])
c = np.array([0, 0, 0])

pose_model = YOLO('checkpoints/yolo11x-pose.pt')
depth_model, transform = depth_pro.create_model_and_transforms(
    device=torch.device("cuda"), precision=torch.float16
)
depth_model.eval()

cap = cv2.VideoCapture(0)
if not cap.isOpened():
    print("Webcam could not be opened.")
    exit()

width = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))
height = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))
print(f"Webcam resolution: {width}x{height}")
frame_no = 0

while True:
    ret, frame = cap.read()
    if not ret:
        print("Frame read failed. Exiting.")
        break
    print(f'Frame: {frame_no}', end='\r')
    frame_no += 1
    results = pose_model(frame)
    keypoints = []
    for result in results:
        if result.keypoints is None:
            continue
        keypoints = result.keypoints.data

    if frame_no % 30 == 0:
        depth_image = transform(frame)
        prediction = depth_model.infer(depth_image)
        depth = prediction["depth"]

        keypoints_3d = []
        for id, person in enumerate(keypoints):
            keypoint_3d = []
            for no, kp in enumerate(person):
                x, y, conf = kp.tolist()
                if (x > 1) and (y > 1) and (round(x) < width) and \
                (round(y) < height) and (conf > 0.5):
                    z = float(depth[round(y), round(x)])
                    p = get_xyz(x, y, width, height, fov, z, u, f, c, 1)
                    keypoint_3d.append([no, p])
            keypoints_3d.append([id, keypoint_3d])

        threshold = 0.1
        for i, (id_i, keypoints_i) in enumerate(keypoints_3d):
            wrist_points = [kp for kp in keypoints_i if kp[0] in [9, 10]]
            for wrist_id, wrist_xyz in wrist_points:
                for j, (id_j, keypoints_j) in enumerate(keypoints_3d):
                    if id_i == id_j:
                        continue
                    for _, other_xyz in keypoints_j:
                        dist = np.linalg.norm(wrist_xyz - other_xyz)
                        if dist < threshold:
                            wrist_2d = keypoints[id_i][wrist_id][:2]
                            x, y = int(wrist_2d[0]), int(wrist_2d[1])
                            cv2.circle(frame, (x, y), 10, (0, 0, 255), -1)
                            print('Detected')
                            filename = f"frames/{frame_no}.jpg"
                            break

    annotated_frame = results[0].plot()
    cv2.imshow("Pose Estimation", frame)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
```
