---
description: Derivation of the square of summation formula!
category: Discoveries
math: True
---

> Refresh the page once if the math doesn't get rendered properly!
{: .prompt-info }

Ever faced a summation that was squared and needed to expand it? Or got the need to send the square inside the summation? I had, while deriving [Bessel's Correction](https://navam9530.github.io/posts/Bessel's-Correction/) formula. Here's the derivation for expanding the square of a summation:

$$\begin{aligned}
\left( \sum_{i=1}^{n} a_i \right)^2
&= (a_1+a_2+a_3+ \dots +a_{n-1}+a_n)^2 \\
&= (a_1+a_2+a_3+ \dots +a_{n-1}+a_n) \cdot (a_1+a_2+a_3+ \dots +a_{n-1}+a_n) \\
& \\
&= \left(
\begin{aligned}
    & a_1 && \cdot && (a_1 &&+ a_2 &&+ a_3 &&+ \dots &&+ a_{n-1} &&+ a_n) + \\
    & a_2 && \cdot && (a_1 &&+ a_2 &&+ a_3 &&+ \dots &&+ a_{n-1} &&+ a_n) + \\
    & a_3 && \cdot && (a_1 &&+ a_2 &&+ a_3 &&+ \dots &&+ a_{n-1} &&+ a_n) + \\
    & && && && && \vdots \\
    & a_{n-1} && \cdot && (a_1 &&+ a_2 &&+ a_3 &&+ \dots &&+ a_{n-1} &&+ a_n) + \\
    & a_n && \cdot && (a_1 &&+ a_2 &&+ a_3 &&+ \dots &&+ a_{n-1} &&+ a_n)
\end{aligned}
\right) \\
& \\
&= \left(
\begin{aligned}
    & a_1^2 &&+ a_1a_2 &&+ a_1a_3 &&+ \dots &&+ a_1a_{n-1} &&+ a_1a_n+ \\
    & a_2a_1 &&+ a_2^2 &&+ a_2a_3 &&+ \dots &&+ a_2a_{n-1} &&+ a_2a_n+ \\
    & a_3a_1 &&+ a_3a_2 &&+ a_3^2 &&+ \dots &&+ a_3a_{n-1} &&+ a_3a_n+ \\
    & && && && \vdots \\
    & a_{n-1}a_1 &&+ a_{n-1}a_2 &&+ a_{n-1}a_3 &&+ \dots &&+ a_{n-1}^2 &&+ a_{n-1}a_n+ \\
    & a_na_1 &&+ a_na_2 &&+ a_na_3 &&+ \dots &&+ a_na_{n-1} &&+ a_n^2
\end{aligned}
\right) \\
& \\
&= \left(
\begin{aligned}
    & (a_1^2 + a_2^2 + a_3^2 + \dots + a_{n-1}^2 + a_n^2) &+ 2a_1(a_2 + a_3 + \dots + a_{n-1} + a_n) \\
    & &+ 2a_2(a_3 + \dots + a_{n-1} + a_n) \\
    & && \!\!\!\!\!\!\!\!\!\!\!\!\!\!\!\!\! \vdots \\
    & &+ 2a_{n-1}(a_n)
\end{aligned}
\right) \\
& \\
&= \sum_{i=1}^na_i^2 + 2a_1 \sum_{j=2}^na_j + 2a_2 \sum_{j=3}^na_j + \dots + 2a_{n-1} \sum_{j=n}^na_j \\
& \\
\therefore \left( \sum_{i=1}^{n} a_i \right)^2 &= \sum_{i=1}^na_i^2 + 2 \sum_{i=1}^{n-1} \sum_{j=i+1}^na_ia_j
\end{aligned}$$
