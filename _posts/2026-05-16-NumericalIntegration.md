---
layout: single
title: 'Numerical Quadrature: A Simple Tool Behind Complex Scientific Models'
collection: posts
permalink: /posts/2026-05-16-QuadratureMethods/
date: 2026-05-16
tags: [Numerical Integration, uncertainty quantification, applications in nuclear physics, Approximation techniques]
mermaid: true
---

Numerical integration is one of those mathematical tools that appears almost everywhere in scientific computing. Whether we are estimating expectations, quantifying uncertainty, calibrating computer models, or solving inverse problems, we frequently encounter integrals that cannot be evaluated analytically.

A general integral takes the form

$$
I=\int_a^b f(x)\,dx.
$$

**Numerical quadrature** approximates this integral using a weighted sum of function evaluations:

$$
I\approx \sum_{i=1}^{N}w_i f(x_i),
$$

where \\(x_i\\) are quadrature nodes and \\(w_i\\) are corresponding weights.

The underlying idea is simple: rather than evaluating a potentially complicated integral directly, we approximate it using carefully selected points.

## Common Quadrature Methods

Several classical approaches are widely used in numerical analysis.

- **Trapezoidal rule:** Approximates the integrand using piecewise linear functions. It is straightforward and effective for sufficiently smooth functions.
- **Simpson's rule:** Uses piecewise quadratic approximations and often achieves greater accuracy for smooth integrands.
- **Gaussian quadrature:** Selects nodes and weights to maximize polynomial exactness. For example, an \\(N\\)-point Gauss–Legendre rule integrates polynomials of degree up to \\(2N-1\\) exactly.
- **Monte Carlo integration:** Uses random samples to approximate integrals, making it particularly useful for high-dimensional problems.

The choice of method depends on the smoothness of the integrand, dimensionality, computational cost, and desired accuracy.

## Application: Computing Nuclear Reaction Rates

Consider a simplified nuclear reaction involving two particles. In nuclear astrophysics, reaction rates often depend on averaging an energy-dependent reaction cross section over a distribution of particle energies.

For particles following a Maxwell–Boltzmann distribution, the thermally averaged reaction rate can be written as

$$
\langle \sigma v\rangle =
\sqrt{\frac{8}{\pi\mu}}
\frac{1}{(k_BT)^{3/2}}
\int_0^\infty
\sigma(E)E
\exp\left(-\frac{E}{k_BT}\right)dE,
$$

where:

- \\(\sigma(E)\\) is the reaction cross section at energy \\(E\\),
- \\(\mu\\) is the reduced mass of the reacting particles,
- \\(k_B\\) is Boltzmann's constant,
- \\(T\\) is the temperature.

The integral combines information about the nuclear interaction with the thermal distribution of particle energies.

In practice, the cross section may be available only through expensive numerical simulations or experimental measurements. Consequently, evaluating the reaction rate becomes a numerical integration problem.

For example, after truncating the integral at a sufficiently large energy \\(E_{\max}\\), Gaussian quadrature gives

$$
\langle \sigma v\rangle
\approx
C(T)\sum_{i=1}^{N}
w_i\sigma(E_i)E_i
\exp\left(-\frac{E_i}{k_BT}\right),
$$

where

$$
C(T)=\sqrt{\frac{8}{\pi\mu}}(k_BT)^{-3/2},
$$

and the quadrature nodes and weights are defined on \\([0,E_{\max}]\\).

This provides an efficient way to estimate reaction rates without evaluating the cross section at every possible energy.

## Connection to Statistical Learning and Uncertainty Quantification

What makes quadrature particularly interesting to me is its connection to statistical learning and computer experiments.

Suppose the cross section \\(\sigma(E)\\) is computationally expensive to evaluate. Instead of repeatedly running the underlying physics simulation, we can construct a Gaussian process surrogate:

$$
\sigma(E)\mid \mathcal D
\sim \mathcal{GP}\big(m(E),k(E,E')\big).
$$

We can then estimate the reaction rate by integrating the surrogate's posterior mean:

$$
\mathbb E[I\mid\mathcal D]
=
\int_0^\infty m(E)q(E)\,dE,
$$

where \\(q(E)\\) represents the appropriate energy-dependent weighting function.

More importantly, we can quantify uncertainty in the integral:

$$
\operatorname{Var}(I\mid\mathcal D)
=
\int_0^\infty\int_0^\infty
k(E,E')q(E)q(E')\,dE\,dE'.
$$

These expressions illustrate an important connection between **Gaussian processes, numerical integration, and uncertainty quantification**.

The problem is no longer simply about approximating an integral. It also involves determining how uncertain that approximation is and deciding where additional simulations would be most informative.

This leads naturally to Bayesian quadrature, active learning, and sequential experimental design.

## Why This Matters for My Research

In my research on computer model calibration, Gaussian processes, and sequential design, numerical integration appears in several forms:

1. **Bayesian inference:** Computing posterior expectations and integrating over uncertain model parameters.
2. **Model calibration:** Evaluating integrated discrepancy measures between computer simulations and physical observations.
3. **Uncertainty quantification:** Integrating predictive covariance functions to measure overall uncertainty.
4. **Sequential design:** Selecting new simulation or experimental inputs that reduce integrated predictive uncertainty.

For instance, integrated mean squared prediction error (IMSPE) criteria are closely related to numerical integration:

$$
\operatorname{IMSPE}(\mathcal D)
=
\int_{\mathcal X}
\operatorname{Var}\big(f(x)\mid\mathcal D\big)\,dx.
$$

When this integral cannot be evaluated analytically, quadrature provides a practical approximation.

The same mathematical principles that help approximate nuclear reaction rates can therefore be used to determine where to run the next expensive computer simulation.

## Final Thoughts

Numerical quadrature is much more than a collection of integration formulas. It is an essential computational tool connecting numerical analysis, statistical inference, and scientific modeling.

Applications in nuclear physics illustrate how a seemingly simple integral can encode complex physical phenomena. When combined with Gaussian process surrogates and sequential design, quadrature becomes even more powerful: it allows us not only to approximate quantities of scientific interest but also to quantify uncertainty and allocate computational resources intelligently.

This intersection of numerical computation, statistical learning, and uncertainty quantification is central to many of the problems I enjoy studying.
