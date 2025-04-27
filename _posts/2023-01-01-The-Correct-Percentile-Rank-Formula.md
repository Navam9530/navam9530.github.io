---
description: The Formula given to calculate the Percentile Rank is Incorrect everywhere!
category: Discoveries
math: True
---

> Refresh the page once if the math doesn't get rendered properly!
{: .prompt-info }

If you have ever studied Descriptive Statistics, you would have come across Percentiles and Percentile Ranks. The formula for calculating Percentile Rank using given Percentile is given by:

$$Rank = Percentile \cdot (n+1)$$

where $n$ is 'Total number of Data Samples'.

But the correct formula is:

$$Rank = (n \cdot Percentile) + 1$$

The derivation for the same is provided below:

We know that,

$$Percentile = \frac{Number \ of \ values \ less \ than \ X}{Total \ number \ of \ values}$$

In other words,

$$Percentile = \frac{Number \ of \ values \ existing \ before \ Rank}{Total \ number \ of \ values}$$

And we also know that,

$$Number \ of \ values \ existing \ before \ Rank = Rank - 1$$

This is the point that has been missed by many people that we can write $Number \ of \ values \ less \ than \ X$ in terms of the $Rank$. This is why we skip the $2^\text{nd}$ Rank if two individuals are tied at $1^\text{st}$ Rank, in order to preserve the property!

By substituting in the formula, we get,


$$\begin{aligned}
Percentile &= \frac{Rank-1}{n}\\
& \\
\Rightarrow Rank-1 &= n \cdot Percentile \\
& \\
\therefore Rank &= (n \cdot Percentile) + 1
\end{aligned}$$
