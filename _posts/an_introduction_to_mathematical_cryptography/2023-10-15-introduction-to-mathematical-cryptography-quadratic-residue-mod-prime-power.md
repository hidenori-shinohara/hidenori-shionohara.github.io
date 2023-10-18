---
layout: post
title:  "An Introduction to Mathematical Cryptography: Quadratic Residue Mod Prime Powers"
date:   2023-10-15
author: Hidenori
---

Exercise 1.34(a) and 1.35 in _An Introduction to Mathematical Cryptography_.

These exercises are based on a special case of [Hensel's Lemma](https://en.wikipedia.org/wiki/Hensel's_lemma), and we prove a slightly stronger statement than Hensel's Lemma.

Let an odd prime $p$ and $1 <= b <= p - 1$.
Then we will prove the following statements in order:

1. $x^2 \equiv b \pmod{p}$ has either no solutions or exactly two solutions.
1. If $x^2 \equiv b \pmod{p}$ has a solution, we can lift that solution to find a solution to $x^2 \equiv b \pmod{p^e}$ for any $e \in \mathbb{N}$.
1. $x^2 \equiv b \pmod{p^e}$ has exactly the same number of solutions for every $e \in \mathbb{N}$.

# Statement 1: $x^2 \equiv b \pmod{p}$ has either no solutions or exactly two solutions

If it has no solution, we are done.
Suppose it has a solution $0 < \alpha < p$.
Then it is obvious that $p - \alpha$ is a solution also.
Thus if there is at least one solution, there are at least two solutions.
Let $0 < \alpha, \alpha' < p$ be solutions to $x^2 \equiv b \pmod{p}$.
Then $\alpha^2 - \alpha'^2 \equiv 0 \pmod{p}$, so $p \mid \alpha + \alpha'$ or $p \mid \alpha - \alpha'$.
Since $0 < \alpha, \alpha' < p$, $2 \leq \alpha + \alpha' < 2p$ and $-p < \alpha - \alpha' < p$.
Therefore, $\alpha + \alpha' = p$ or $\alpha - \alpha' = 0$.
Hence, $\alpha' = \alpha$ or $\alpha' = p - \alpha$.

This implies that if there is a solution, there is exactly two solutions.

# Lemma 2: If $x^2 \equiv b \pmod{p}$ has a solution, we can lift that solution to find a solution to $x^2 \equiv b \pmod{p^e}$ for any $e \in \mathbb{N}$.

Let $b$ be chosen such that $x^2 \equiv b \pmod p$ has a solution $\alpha$.

For every positive integer $e$, let $P(e)$ be the statement that there exists a $\beta$ such that

- $\beta^2 \equiv b \pmod{p^e}$, and
- $\alpha \equiv \beta \pmod p$.

$P(1)$ is obviously true.
We assume that $P(e)$ is true for some $e \in \mathbb{N}$ and we will prove that $P(e + 1)$ is true.

Let $\beta$ be given such that $\beta^2 \equiv b \pmod{p^e}$ and $\alpha \equiv \beta \pmod p$.
This means that $\beta^2 = mp^e + b$ and $\beta = np + \alpha$ for some $m, n \in \mathbb{Z}$.

Let $\gamma = lp^e + \beta$ where $l = \frac{-m}{2\alpha}$.
Note that $\gcd(\alpha, p) = \gcd(2, p) = 1$, so the inverse of $2\alpha$ exists.

$$
\begin{align*}
    \gamma^2
        &= l^2p^{2e} + 2l\beta p^e + \beta^2 \\
        &\equiv 2l\beta p^e + \beta^2 \\
        &\equiv 2l(np + \alpha)p^e + mp^e + b \\
        &\equiv 2l\alpha p^e + mp^e + b \\
        &\equiv (2l\alpha + m)p^e + b \\
        &\equiv (-m + m)p^e + b \\
        &\equiv b & \pmod{p^{e + 1}}.
\end{align*}
$$

Furthermore, $\gamma \equiv \beta \equiv \alpha \pmod p$.
Therefore, $P(e + 1)$ is true, and by mathematical induction, the statement is true for any positive integer.

We will quicky discuss how to come up with $\gamma = lp^e + \beta$.
The first realization is that $\gamma \equiv \beta \pmod{p^e}$.
Since $\gamma^2 \equiv b \pmod{p^{e + 1}}$, $\gamma^2 = kp^{e + 1} + b$.
Therefore, $\gamma^2 \equiv b \pmod{p^e}$.
Then $\gamma = lp^e + \beta$.
By solving $\gamma^2 = (lp^e + \beta)^2 \equiv b \pmod{p^{e + 1}}$ for $l$, we obtain the formula for $\gamma$.

# Lemma 3: $x^2 \equiv b \pmod{p^e}$ has exactly the same number of solutions for every $e \in \mathbb{N}$.

It suffices to show that, for any given $e \geq 2$, $x^2 \equiv b \pmod{p^e}$ has the same number of solutions as $x^2 \equiv b \pmod{p}$.

Suppose $x^2 \equiv b \pmod{p}$ has no solutions.
Suppose that $x^2 \equiv b \pmod{p^e}$ has a solution $\beta$ for some $e$.
Then $\beta^2 = kp^e + b$ for some $k \in \mathbb{Z}$, so $\beta^2 \equiv p \cdot kp^{e - 1} + b \equiv b \pmod{p}$.
In other words, $\beta$ is a solution to $x^2 \equiv b \pmod{p}$.
This is a contradiction, so $x^2 \equiv b \pmod{p^e}$ cannot have a solution for any $e$.

Suppose $x^2 \equiv b \pmod{p}$ has at least one solutions.
By Lemma 1, it must have exactly two solutions $\alpha_1, \alpha_2$.
We will prove by induction that for every $e \geq 1$, $x^2 \equiv b \pmod{p^e}$ has two solutions.
If $e = 1$, we are done.
Suppose $x^2 \equiv b \pmod{p^e}$ has two solutions for some $e \in \mathbb{N}$.
By Lemma 2, we know $x^2 \equiv b \pmod{p^{e + 1}}$ has two distinct solutions $\gamma_1, \gamma_2$ such that $\gamma_i \equiv \alpha_i \pmod{p}$ for $i = 1, 2$.
As discussed in Lemma 2, any solutions to $x^2 \equiv b \pmod{p^{e + 1}}$ are solutions to $x^2 \equiv b \pmod{p^e}$.

TODO: I think that this is a good problem but it's poorly written. I need to figure out a good series of lemmans that I can prove.

Okay, I think the following series of lemmas work.
Let $p$ be an odd prime and an integer $1 \leq b \leq p - 1$ be given.
Let $S_e = \\{ 1 \leq x \leq p^e - 1 \mid x^2 \equiv b \pmod{p^e} \\}$ be the set of solutions for $x^2 \equiv b \pmod{p^e}$.

1. We claim $\abs{S_1} \in \\{ 0, 2 \\}$.
1. $\forall e \in \mathbb{N}$, there exists an injection $F_e: S_{e + 1} \rightarrow S_e$.
1. $\forall e \in \mathbb{N}$, there exists an injection $G_e: S_{e} \rightarrow S_{e + 1}$.
1. $\forall e \in \mathbb{N}$, $\abs{S_e} = \abs{S_{e + 1}}$.
1. $\forall e$, there exists $H_e: S_1 \rightarrow S_e$ such that $H_e(\alpha) \in S_{e}$ and $H_e(\alpha) \equiv \alpha$ for each $\alpha \in S_1$.

TODO: actually solve these

