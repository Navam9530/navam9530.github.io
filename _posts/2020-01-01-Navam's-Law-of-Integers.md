---
description: A Theory on Integers!
category: Inventions
math: True
---

> Refresh the page once if the math doesn't get rendered properly!
{: .prompt-info }

## Definition

`The product of the sum of x & y and the number of integers in between x & y is twice the sum of the integers in between x & y.`

$$(x+y)m = 2\sum n$$

where:
* $x < y$ and $x, y \in \mathbb{Z}$
* $m \Rightarrow$ Number of integers in between $x$ & $y$ (excluded both)
* $\Sigma n \Rightarrow$ Sum of all integers in between $x$ & $y$ (excluded both)

## Proof

$$\sum n = n_1+n_2+\dots+n_m$$

We know that,

$$
n_1 = x+1 \implies a \\
n_2 = y-1 \implies l
$$

We also know that,

$$
S_n = \frac{n}{2}(a+l) \\
\ \\
\Rightarrow \sum n = \frac{m}{2}(x+1+y-1) \\
\ \\
\therefore (x+y)m = 2\sum n
$$

## Another Version

We know that the number of integers in between $x$ and $y$ is one less than the difference of $y$ and $x$.

$$\Rightarrow m = (y-x)-1$$

Navam's Law of Integers can be rewritten as:

$$\begin{aligned}
(y-x-1)(x+y) &= 2\sum n \\
& \\
(y-x)(y+x)-(x+y) &= 2\sum n \\
& \\
y^2-x^2-(x+y) &= 2 \sum n \\
& \\
\therefore y^2-x^2 &= x+y+2\sum n
\end{aligned}$$