# LoL Two-Trick Finder

A simple web tool designed to help League of Legends Top Laners find their optimal secondary champion.

## Live Site
Check out the tool here: [https://max-we.github.io/LoL-Two-Trick-Finder/](https://max-we.github.io/LoL-Two-Trick-Finder/)

## Motivation
Most existing recommendation sites give shaky, hard-to-understand suggestions. This tool uses a simple, transparent method (see below) that has worked well in practice to find a strong secondary champion for top laners.

## How it works
> **Note:** This score is a robust heuristic designed to capture overall matchup coverage. It should not be interpreted as a probability or expected winrate.

### Casual explanation
For each enemy pick, the system looks at how the main and the partner usually perform into that matchup (clearly losing / roughly even / clearly winning), and how often that enemy actually shows up. For that enemy, it keeps the better of the two options (main or partner), weighted by how common the matchup is. Doing this across all enemy champions gives a single score that reflects how well this duo performs into the overall field of opponents.

### Precise explanation
Let enemies be indexed by $i = 1,\dots,N$. For main $m$ and partner $p$, let $\Delta_m(i), \Delta_p(i)$ be their winrate deltas vs enemy $i$, and define ordinal scores $w_m(i), w_p(i) \in \{-1,0,1\}$ via a thresholding map $\text{scale}(\Delta)$.

Let $n_m(i), n_p(i)$ be match counts and
$p_m(i) = n_m(i)/\sum_j n_m(j)$, $p_p(i) = n_p(i)/\sum_j n_p(j)$ the corresponding matchup frequencies.

The weighted scores are
$v_m(i) = w_m(i)\,p_m(i)$, $v_p(i) = w_p(i)\,p_p(i)$, and the coverage score is

$$S(m,p) = \sum_{i=1}^N \max\{v_m(i),\, v_p(i)\},$$

i.e. the sum over enemies of the better of the two weighted outcomes.