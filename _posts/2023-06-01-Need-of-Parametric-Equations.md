---
description: A Line is represented by 1 Equation in 2D but by 3 Equations in 3D. Why?
category: Discoveries
math: True
---

> Refresh the page once if the math doesn't get rendered properly!
{: .prompt-info }

## Addressing the main question

A line in $\mathbb{R}^{2}$ is represented as $y=mx+c$. It is a single equation involving 2 variables. Similarly, if we write an equation involving 3 variables, say $ax+by+cz=d$, then we are told that it is no more a line, but a plane in $\mathbb{R}^{3}$. So what is the equation of a line in $\mathbb{R}^{3}$? Surprisingly, it is not a single equation, but a set of 3 equations:

$$\begin{aligned}
x &= x_0+ta\\
y &= y_0+tb\\
z &= z_0+tc
\end{aligned}$$

But why do we need 3 equations to represent a single object in space? If you are going to answer "As there are 3 dimensions, there are 3 equations!", then why is the line in a 2D space had only 1 equation? By applying your logic, it should contain 2 equations right?

Before I begin answering the question, I want to clarify two terms here:

Object
: The m-dimensional shape that you are willing to represent

Space
: The n-dimensional scope that you are willing to represent the object in

I am going to answer the question in 2 parts. First I will address the equations of lines in $\mathbb{R}^{2}$ and $\mathbb{R}^{3}$ and then the equation of plane in $\mathbb{R}^{3}$.

## Line equations in $\mathbb{R}^{2}$ and $\mathbb{R}^{3}$

In $\mathbb{R}^{2}$, to represent any point, we can use a tuple $(x,y)$, where $x$ and $y$ can be any unrelated random numbers. That is, $x$ and $y$ are independent variables.

When you draw a line in $\mathbb{R}^{2}$, all of the individual points in the line should satisfy the line equation. If you observe, for a particular value of $x$, there is a corresponding $y$ value. It means the variable $y$ is no more independent. It becomes a dependent variable. Then the set of points representing the line can be represented as $(x, f(x))$. To generate the points, we can input any random number in the $x$ slot (since it's independent), and then compute $y$ using:

$$f(x)=y=mx+c$$

If you notice, a single equation is enough to represent all the points in the line.

Similarly, if you apply the same logic in $\mathbb{R}^{3}$, to represent any point, we can use another tuple $(x, y, z)$, where $x$, $y$ and $z$ can be any unrelated random numbers. That is, $x$, $y$ and $z$ are independent variables.

When you draw a line in $\mathbb{R}^{3}$, all of the individual points in the line should satisfy the line equation. If you observe, for a particular value of $x$, there is corresponding $y$ and $z$ values. It means the variables $y$ and $z$ are no more independent. They become dependent variables. Then the set of points representing the line can be represented as $(x, f(x), g(x))$. To generate the points, we can input any random number in the $x$ slot (since it's independent), and then compute $y$ and $z$ using:

$$\begin{aligned}
f(x) &= y=m_1x+y_0\\
g(x) &= z=m_2x+z_0
\end{aligned}$$

If you notice, now we need 2 equations to represent all the points in the line. Then why are 3 equations given?

Actually, the 3 equations are generated from the 2 equations we formed. Let us call the form of our equations as '`General` Form'. The form of the 3 equations is called as '`Parametric` Form'. If you rearrange the `Parametric` equations, we get back our `General` equations.

$$x=x_0+ta \implies t=\frac{x-x_0}{a}$$

Substituting $t$ in $y$ gives:

$$\begin{aligned}
y & =y_0+tb\\
& =y_0+(\frac{x-x_0}{a})b\\
\therefore y & =f(x)
\end{aligned}$$

Substituting $t$ in $z$ gives:

$$\begin{aligned}
z & =z_0+tc\\
& =z_0+(\frac{x-x_0}{a})c\\
\therefore z & =g(x)
\end{aligned}$$

See, we can convert the `Parametric` equations into `General` equations and vice-versa. We have understood that rewriting our `General` equations as `Parametric` equations is completely valid. But why do we need them in the first place? Is it because of symmetry? Well, it is more than just for symmetrical purposes. To understand its significance, let us address the second part too.

## Plane equation in $\mathbb{R}^{3}$

Let us rearrange the line equation (`General`) in $\mathbb{R}^{2}$ to a more general format.
$$y=mx+c \implies mx-y=-c$$
It is in the form $ax+by=c$ and let us proceed with that equation.

Let us remove the constant term $c$ and replace it with a variable $t$. Then the equation becomes $ax+by=t$. Guess what points satisfy the equation? Well if we take any random value as $x$ and scale it and do similar with $y$ and add them and you say the result equals whatever random value. This clarifies that any point in $\mathbb{R}^{2}$ satisfies the equation. So, the equation represents $\mathbb{R}^{2}$ itself. Yes, it of course is a plane equation. If you rearrange the equation, you get in the format that we are familiar with i.e., $ax+by+cz=d$ (where $c=-1$ and $d=0$). Hence, this is a plane equation.

When we remove $t$ and replace our $c$ again, it becomes the equation of line, which indirectly means that if you restrict the sum to be a constant, we are decreasing 1 dimension of the object.

Similarly take $ax+by+cz=t$. Now, which points satisfy the equation? As you guessed it, the equation represents the whole 3-dimensional space itself. If you again restrict the sum to be a constant, we get the equation of a 2-dimensional object caused by the decrement of 1 dimension.

The same process is applicable for higher dimensions also. The key takeaway here is that if we restrict the sum to be constant, we are reducing one dimension of the object.

Let us take the plane equation and rearrange the terms in it.

$$\begin{aligned}
ax+by+cz &= d\\
z &= \frac{d-ax-by}{c}\\
z &= f(x, y)
\end{aligned}$$

This says that if we restrict the sum to be constant, it is equivalent to converting an independent variable to dependent variable. Here the conversion can be applied on any independent variable, but let us stick to $z$.

Let us experiment with this then. What happens if we convert another independent variable to dependent, say $y=g(x)$ or $y=g(x,z)$ in the same example? Well $y=g(x,z)$ gives another plane equation. This leads us back to our first part where the points $(x,g(x,z),f(x,y))$ represent a line equation. Another way to view this scenario is the intersection of 2 (non-parallel) planes results in line.

Let us make the last independent variable i.e, $x$ as dependent, which means $x=h(y,z)$

Now, you get the equation of a point. This can be viewed from many perspectives, such as the intersection of 3 planes, 2 planes and 1 line, 1 plane and 2 lines, or even 3 lines.

In summary, with each addition of a condition, we get:

$$\begin{aligned}
ax+by+cz=t & \implies \mathbb{R}^{3} & \implies 3D\\z=f(x,y) & \implies Plane & \implies 2D\\y=g(x,z) & \implies Line & \implies 1D\\x=h(y,z) & \implies Point & \implies 0D
\end{aligned}$$

We have experimented with $\mathbb{R}^{3}$, but the same logic applies in $\mathbb{R}^{2}$ and higher dimensions also.

## Generalizing Across Dimensions

### In $\mathbb{R}^{2}$ space

| Plane(2D) | Line(1D) | Point(0D)|
|:-:|:-:|:-:|
| $x$ | $x$ | $f(y)$ |
| $y$ | $f(x)$ | $g(x)$ |

### In $\mathbb{R}^{3}$ space

| 3D | Plane(2D) | Line(1D) | Point(0D)|
|:-:|:-:|:-:|:-:|
| $x$ | $x$ | $x$ | $f(y,z)$ |
| $y$ | $y$ | $f(x,z)$ | $g(x,z)$ |
| $z$ | $f(x,y)$ | $g(x,y)$ | $h(x,y)$ |

### In $\mathbb{R}^{4}$ space

| 4D | 3D | Plane(2D) | Line(1D) | Point(0D)|
|:-:|:-:|:-:|:-:| :-: |
| $w$ | $w$ | $w$ | $w$ | $f(x,y,z)$ |
| $x$ | $x$ | $x$ | $f(w,y,z)$ | $g(w,y,z)$ |
| $y$ | $y$ | $f(w,x,z)$ | $g(w,x,z)$ | $h(w,x,z)$ |
| $z$ | $f(w,x,y)$ | $g(w,x,y)$ | $h(w,x,y)$ |$i(w,x,y)$ |

### Another Perspective

Here, we can observe that by adding a dependency, we are reducing one dimension. Another perspective to view this is: 'The number of independent variables represents the number of dimensional object'.

But there is a slight catch here. We don't include our independent variables in our `General` Form. We only write the equations for the dependent variables. They don't address the n-dimensional space the object is in. To tackle this problem, mathematicians formulated `Parametric` form.

The invention happened in the following way. Consider a line in $\mathbb{R}^{3}$. We need 2 equations to represent it in `General` form since there is 1 independent variable and 2 dependent variables. We need to capture the number of independent variables to represent the number of dimensional object and number of equations to represent the number of dimensional space.

So, instead of treating $x$ as an independent variable, let us declare $x$ as dependent on some other independent variable, say $t$, so that it gets an equation of its own.

Then $x$ can be rewritten as:

$$\begin{aligned}
x &= h(t)\\
\therefore x &= at+x_0
\end{aligned}$$

Similarly, $y$ can be rewritten as:

$$\begin{aligned}
y &= f(x,z)\\
&= a_1x+b_1z+c_1\\
&= a_1(at+x_0)+b_1z+c_1\\
&= a_1at+a_1x_0+b_1z+c_1\\
&= (a_1a)t+(a_1x_0+b_1z+c_1)\\
\therefore y &= bt+y_0
\end{aligned}$$

Similarly, $z$ can be rewritten as:

$$\begin{aligned}
z &= g(x,y)\\
&= a_2x+b_2y+c_2\\
&= a_2(at+x_0)+b_2y+c_2\\
&= a_2at+a_2x_0+b_2y+c_2\\
&= (a_2a)t+(a_2x_0+b_2z+c_2)\\
\therefore z &= ct+z_0
\end{aligned}$$

This is the conversion process of `General` form to `Parametric` Form. We know that this process is just the opposite to what we have done in part 1. The advantage of this structure is that just by looking at the set of equations, we can know the m-dimensional object it is representing in the n-dimensional space. Here the number of independent variables is 1 i.e., $t$. So, we are representing a 1-dimensional object i.e., a line. And the number of equations are 3. So, we are representing it in $\mathbb{R}^{3}$.

Take another set of `Parametric` equations for example:

$$\begin{aligned}
v&=7t_1+t_2+3t_3+4\\w&=t_1+2t_2+3t_3+5\\x&=6t_1+7t_2+8t_3+9\\y&=t_2+2t_3+3\\z&=t_1+t_2+t_3
\end{aligned}$$

The number of independent variables is 3. (Note: Some equations might not explicitly use all parameters, but always consider the maximum number of independent variables involved.). And the number of equations are 5. So, the set is representing a 3-dimensional object in 5-dimensional space.

## Conclusion

In summary, in parametric form:
* The **number of independent variables** indicates the **dimension of the object**.
* The **number of equations** indicates the **dimension of the space the object lives in**.

### In $\mathbb{R}^{2}$ space

| Plane(2D) | Line(1D) | Point(0D)|
|:-:|:-:|:-:|
| $f(t_1,t_2)$ | $f(t)$ | $c_1$ |
| $g(t_1,t_2)$ | $g(t)$ | $c_2$ |

### In $\mathbb{R}^{3}$ space

| 3D | Plane(2D) | Line(1D) | Point(0D)|
|:-:|:-:|:-:|:-:|
| $f(t_1,t_2,t_3)$ | $f(t_1,t_2)$ | $f(t)$ | $c_1$ |
| $g(t_1,t_2,t_3)$ | $g(t_1,t_2)$ | $g(t)$ | $c_2$ |
| $h(t_1,t_2,t_3)$ | $h(t_1,t_2)$ | $h(t)$ | $c_3$ |

### In $\mathbb{R}^{4}$ space

| 4D | 3D | Plane(2D) | Line(1D) | Point(0D)|
|:-:|:-:|:-:|:-:| :-: |
| $f(t_1,t_2,t_3,t_4)$ | $f(t_1,t_2,t_3)$ | $f(t_1,t_2)$ | $f(t)$ | $c_1$ |
| $g(t_1,t_2,t_3,t_4)$ | $g(t_1,t_2,t_3)$ | $g(t_1,t_2)$ | $g(t)$ | $c_1$ |
| $h(t_1,t_2,t_3,t_4)$ | $h(t_1,t_2,t_3)$ | $h(t_1,t_2)$ | $h(t)$ | $c_2$ |
| $i(t_1,t_2,t_3,t_4)$ | $i(t_1,t_2,t_3)$ | $i(t_1,t_2)$ | $i(t)$ |$c_3$ |