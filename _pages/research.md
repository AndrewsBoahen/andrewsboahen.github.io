---
layout: single
title: "Research"
permalink: /research/
author_profile: true
---


## Research Overview
My research sits at the intersection of $\color{blue}{\text{statistical theory,}}$ $\color{blue}{\text{probabilistic computation,}}$ and $\color{blue}{\text{scientific inference}}$. I enjoy developing principled frameworks for reasoning under uncertainty in complex, high-dimensional systems. 

Specifically, my research spans the topics of **Uncertainty quantification, Bayesian inverse problems, Monte carlo inference, Active learning** and **Optimization under uncertainty** with application areas from computer experiments and engineering sciences to digital twins and mission-critical physical systems.

 **Keywords:** <small> $\color{green}{\text{Bayesian statistics}}$ · $\color{green}{\text{Monte Carlo methods}}$ · $\color{green}{\text{Inverse problems}}$ · $\color{green}{\text{Gaussian & Deep Gaussian processes}}$ · $\color{green}{\text{Stochastic optimisation}}$ · $\color{green}{\text{Scientific ML}}$ <small>

## Bayesian inverse problems
$\color{blue}{\text{Inverse problems ask:}}$ given observations $y = \mathcal{G}(u) + \varepsilon$, can we recover the unknown field or parameter $u$? The forward operator $\mathcal{G}$ is typically a differential equation or physical model, making direct inversion ill-posed in the [Hadamard sense](https://www.statisticshowto.com/well-posed-ill/).
 
The Bayesian formulation regularises this naturally: by placing a prior $\pi_0(u)$ over the unknown and conditioning on data, the posterior
 
$$\pi(u \mid y) \propto \mathcal{L}(y \mid u)\, \pi_0(u)$$
 
encodes full uncertainty over plausible reconstructions. My work focuses on developping scalable computational methods for characterising this posterior and frequentist approaches to this problem with uncertainty guarantees.

<!--**function-space settings**, where $u$ lives in an infinite-dimensional Hilbert or Banach space, exploiting structure in the forward operator to make inference tractable.-->
 
**Topics:** Computer Model Calibration  · Tikhonov–Bayes connections · [pCN algorithms](https://en.wikipedia.org/wiki/Preconditioned_Crank–Nicolson_algorithm) · [posterior consistency](https://andrewcharlesjones.github.io/journal/posterior-consistency.html)

## Uncertainty quantification 
Complex computational models, from climate simulators to structural solvers, propagate uncertainty in a way that is rarely tractable analytically. UQ provides the mathematical toolkit to characterise how input uncertainty $p(x)$ maps to output variability $p(y)$ through a black-box or grey-box model $y = f(x)$.
 
My research addresses both:
- $\color{blue}{\text{Forward propagation}}$ — using surrogate modelling (typically GPs but trying to learn more about polynomial chaos expansions and neural networks nowadays) to push distributions through expensive simulators.
- $\color{blue}{\text{Sensitivity analysis}}$ — via Sobol' indices and variance decompositions to identify which inputs drive output uncertainty, formally expressed as
$$S_i = \frac{\mathbb{V}[\mathbb{E}[Y \mid X_i]]}{\mathbb{V}[Y]}$$
 
I am particularly interested in settings where $f$ is expensive to evaluate, coupling emulator construction with rigorous statistical estimation of uncertainty measures and their confidence intervals.
 
**Topics:** Gaussian Process (and their variants) emulation · Sobol' indices · error propagation · conformal prediction

## Bayesian Optimization Optimization under uncertainty
When the objective $f: \mathcal{X} \to \mathbb{R}$ is expensive, noisy, or lacks a known gradient, classical optimisation methods are inapplicable. Bayesian optimisation (BO) maintains a probabilistic surrogate (typically a GP, $f \sim \mathcal{GP}(\mu, k)$), and sequentially queries points that maximise an acquisition function balancing exploration and exploitation, such as expected improvement
 
$$\mathrm{EI}(x) = \mathbb{E}\!\left[\max(f(x) - f^*, 0)\right].$$
 
Beyond standard BO, I am interested in **optimisation under uncertainty**, where the objective itself involves an expectation over stochastic inputs:
 
$$\min_{x \in \mathcal{X}}\; \mathbb{E}_{\xi}\!\left[F(x, \xi)\right]$$
 
requiring joint surrogate models over both decision and environmental variables. Applications span experiment design, hyperparameter tuning, and robust engineering design.
 
**Topics:** Sequential design · acquisition functions · [Thompson sampling](https://web.stanford.edu/~bvr/pubs/TS_Tutorial.pdf) · batch BO · 
<!--multi-fidelity methods-->
 
## Active learning
*Experimental design · Information theory · Surrogates*
 
Active learning addresses the data-efficiency problem: given a budget of $N$ labelled observations, which queries $x_1, \ldots, x_N \in \mathcal{X}$ should be selected to maximise learning? The Bayesian framing connects directly to optimal experimental design — choosing experiments to maximise expected information gain
 
$$\mathbb{E}\!\left[D_{\mathrm{KL}}\!\left(\pi(\theta \mid y)\;\|\;\pi(\theta)\right)\right].$$
 
I develop query strategies for scientific and engineering applications where evaluations are costly, including batch-sequential designs, pool-based and stream-based settings, and model-misspecification-robust criteria. A recurring theme is the interplay between the surrogate model's epistemic uncertainty and the practical cost of queries, particularly in settings with structured input spaces or physics-based constraints.
 
**Topics:** optimal experimental design · information gain · query strategies · pool-based learning · batch design

## Monte carlo inference
*Sampling · Markov chains · Particle methods*
 
Monte Carlo methods form the computational backbone of Bayesian inference: when the posterior $\pi(\theta \mid y)$ is analytically intractable, we approximate expectations
 
$$\mathbb{E}_\pi[h(\theta)] \approx \frac{1}{N}\sum_{i=1}^{N} h(\theta^{(i)}), \quad \theta^{(i)} \sim \pi$$
 
using samples. My research spans classical MCMC (Metropolis–Hastings, HMC, Langevin dynamics), sequential Monte Carlo and particle filters, and more recent gradient-informed and geometry-aware samplers.
 
A central focus is on **convergence guarantees** — bounding the total variation or Wasserstein distance between the chain's marginal and its target — and on scalability to high-dimensional posteriors arising in inverse problems and latent variable models. I also work on variance reduction techniques including control variates and importance sampling to improve estimator efficiency beyond what sample size alone can achieve.
 
**Topics:** MCMC · Hamiltonian Monte Carlo · SMC / particle filters · Langevin diffusion · variance reduction · convergence bounds
 
---
 
> These areas are deeply interconnected — Monte Carlo inference underpins Bayesian inverse problems; active learning drives data collection for UQ; Bayesian optimisation uses the same GP machinery as uncertainty propagation.
