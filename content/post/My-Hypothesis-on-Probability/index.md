---
title: My Hypothesis on Probability Theory
description: Gambler's Fallacy vs. Law of Large Numbers!
date: 2024-08-01
categories:
  - Exploration
math: True
---

## Gambler's Fallacy

On the 18th of August, 1913, at Monte Carlo Casino in Monaco, the ball had landed on black for 26 spins of the roulette table. Gamblers placed huge bets on red during those spins and subsequently suffered heavy losses. Everyone at the table had the same assumption in their minds: "So many blacks! Red is due now!".

But the truth is that spinning a wheel is an independent event. That means past events have no impact on future ones. Whether you are tossing a coin, rolling a die, or spinning a wheel, unless they are biased, all of the events mentioned are independent. The probability of those events occurring remains the same for every random trial. To summarize, people often say:

> "The ball has no memory!"

## Law of Large Numbers (LLN)

Imagine flipping a fair coin. You might get 7 heads and 3 tails in your first 10 tosses. That may not look like a 50-50 split, but keep flipping. As you continue, tossing the coin 100, 1000, or even 10000 times, the proportion of heads and tails will start to even out, getting closer to the true probability (50%). This is the essence of the Law of Large Numbers. As the number of independent trials increases, the average outcome tends to converge to the expected value.

This doesn’t mean the system balances out in the short run, getting 10 heads in a row doesn’t guarantee that tails will come next. But over a large number of trials, randomness smooths itself out. Whether you’re tossing a coin, rolling a die, or spinning a roulette wheel, the more trials you run, the closer your results get to the theoretical probabilities. To put it simply:

> "The truth reveals itself in the long run!"

## My Opinion

The probability of the ball landing on red is 50% even after 26 blacks (assuming, for simplicity, that the roulette wheel has no green slots). But what is the probability of the same ball landing on red after 260000000000 blacks? If it is still 50%, then either of the following is true:

1. LLN must be False.
2. Maybe we are not accounting for the 'Cosmic Balance' in our current Probability Theory.

Since the LLN can be proven both theoretically and practically, second case must be the reason.

## My Proposal

In order to account for the Cosmic Balance, I am proposing an addition to our probability theory. I call the modified probability _Navam's Probability_ and refer to the current one as _Bare Probability_ here:

$$\begin{aligned}
\text{Navam's Probability} \ \ \ &= \ \ \ \ \text{Bare Probability} &&+ \ \ \ \ \ \text{Cosmic Balance} \\\\
NP(x) \ \ \ &= \phantom{\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ } P(x) &&+ \ \ న(\overbrace{P(x) - RF(x)}^\text{Urge})\frac{n}{N}
\end{aligned}$$

where:

$$\begin{aligned}
న \ \ \ &\Rightarrow \ \ \text{Navam's Constant} \\\\
RF \ \ \ &\Rightarrow \ \ \text{Relative Frequency} \\\\
n \ \ \ &\Rightarrow \ \ \text{Number of experiments (NoE)} \\\\
N \ \ \ &\Rightarrow \ \ \text{Threshold NoE beyond which the LLN holds}
\end{aligned}$$
