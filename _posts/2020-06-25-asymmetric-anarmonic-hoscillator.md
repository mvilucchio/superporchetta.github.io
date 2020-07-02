---
layout: article
title: Asymmetrical Non-Harmonic Oscillator
tags: Physics PerturbationTheory
mathjax: true
---

### Introduction ###

It is not easily seen, but one can connect the perturbation theory for a metastable state to its decay rate. In particular, one can calculate the metastable perturbative correction to the energy of a state by using the WKB approximation to evaluate the decay rate to see that the resulting corrections to the energy coincide to the one obtained with straight perturbation theory.

The study will be done on a toy model representative of the false vacuum potentials in QFT. The potential considered is:

$$
V(x)=\frac{1}{2} x^{2}-g \frac{x^{3}}{2} \quad g > 0
$$

This interaction is essentially a harmonic oscillator potential with an odd small perturbation, which order is determined by g. In the limit of $$ x \rightarrow + \infty $$ the cubic potential is greater than the quadratic one, no matter how small g is, so we always have a metastable state.
In the following document, the following analysis is focused on the fundamental state of the harmonics oscillator which energy is 1/2 in atomic units.

![Cubic Potential](/assets/images/posts/black_potential.png)

Since we are interested in a perturbative approach, the energy level we are interested in is very similar to the one of a harmonic oscillator. The condition for using a perturbative approach is such that the maximum of the potential is much greater than the energy level we are considering. The maximum of the potential depends on g.

$$
\frac{1}{2} \ll \frac{2}{27 g^{2}} \quad \implies \quad |g| \ll 0.38
$$

If we were interested in studying the first excited level, we would have a different condition, a third smaller.

### WKB Approach ###

The first approach we can use is considering the perturbative series to the energy. We can express it in terms of a parameter lambda which we can define in terms of g later. In this particular case, we can apply the Cauchy theorem to the complex function and integrate over the discontinuities on the complex plane since for a path of integration to the infinite we the integral vanishes. By looking at the potential for different values of g, we can know where are the branch cuts in the plane. Both for positive and negative g we have a metastable state, but the metastable state vanishes for an imaginary potential, so the cut is for g^2 >0.
Then we transform the integral only over the cut to obtain:

$$
\begin{aligned}
E(z) - E_0 &= \left( E_0 + \sum_{k=1}^{\infty} E_k \lambda^k \right) - E_0 \\
&= \frac{1}{\pi} \int_0^{\infty} d\lambda \frac{\text{Im}\, E(\lambda)}{z - \lambda} = \\
&= \sum_{k=1}^{\infty} \left( \frac{1}{\pi} \int_0^{\infty} d\lambda \frac{\text{Im}\, E(\lambda)}{\lambda^{k+1}} \right) \, z^k
\end{aligned}
$$

The last expression is a usable form to work with since it is a series, and we can evaluate, thanks to the WKB methods, the imaginary part of the energy. The imaginary part of the energy is the opposite of half the decay rate, notice the atomic units here. We need to find the right normalization and to evaluate the penetration factor over the barrier.

$$
\text{Im}\,E(\lambda) = - \frac{\gamma (\lambda)}{2}
$$

The penetration factor can be evaluated asymptotically from its definition. First, we find the roots of the momentum function in the limit of small g, also considering that the energy of the fundamental level is small: $$ \epsilon $$ is two times the energy of the fundamental state. Then we can evaluate the integral of the momentum to the leading order in g. The roots we are interested in are:

$$
\sqrt{\epsilon}+\frac{1}{2} g \epsilon, \quad \frac{1}{g}-g \epsilon
$$

To evaluate the integral, we can split it into two pieces with respect to a point a much greater than the first extreme and much smaller than the second extreme. For the first integral we can neglect the contribute linear in g to the extrema at the leading order, while for the second integral we want to expand in powers of $$ \epsilon $$. Then the integral of the momentum at the leading order in g is:

$$
\int p d x \simeq \frac{4}{15 g^{2}}-\frac{\epsilon}{4}+\frac{\epsilon}{2} \log \left(\frac{g \sqrt{\epsilon}}{8}\right)
$$

Now, in order to normalize the function to the one of a harmonic oscillator insider around zero, we confront the asymptotic behaviour of the AH wave function and the WKB wave function. We find the coefficient to find the decay rate is:

$$
\begin{aligned}
  \frac{\psi_{HO}^{2}(x)}{\psi_{W K B}^{2}(x)} & \underset{x \rightarrow \infty}{\longrightarrow} S_n \\
  S_{n} & \equiv \frac{\sqrt{\pi}}{n !} 2^{-n} e^{-n-\frac{1}{2}}(2 n+1)^{n+\frac{1}{2}}
\end{aligned}
$$

We can notice that this coefficient tends to 1 as the level considered increases. Explicitly to find the decay rate, we have to multiply the inverse of the period by the coefficient $$ S_0 $$ and by the decay rate.

$$
\frac{1}{T} S_{n} D
$$

Now we have found the decay rate so we can find the energy by integrating over $$ \lambda $$ form 0 to $$ \infty $$. Let us not forget these coefficients are the ones only for the even power of g.

$$
\begin{aligned}
  \gamma_{0}^{(0)}(\lambda) &= \frac{4}{\sqrt{\pi}} \frac{1}{\sqrt{\lambda}} e^{-\frac{8}{15 \lambda}} \, (1+\mathcal{O}(\lambda)) \\
  E_{k}^{(0)} &= \sqrt{\frac{15}{2 \pi^{3}}}\left(\frac{15}{8}\right)^{k} \Gamma\left(k+\frac{1}{2} \right) \, \left(1+\mathcal{O}\left(\frac{1}{k}\right)\right)
\end{aligned}
$$

To calculate the first 200 terms by the WKB approach, I implemented a numerical algorithm with a exaggerate arithmetic precision: it used 2000 terms.

### Numerical Confront ###

In order to check the validity of this method, we can calculate the same perturbative therms by a standard perturbative approach. For computational reasons, it is useful to apply perturbation theory to wave functions modulated by a gaussian integral, the asymptotic behaviour of the AH wave functions. The actual eigenfunction of the Schroedinger equation can be written, perturbatively:

$$
\psi(x)=B(x) e^{-x^{2} / 2}
$$

with:

$$
\begin{aligned}
B(x) &= \sum_{k=0}^{\infty} g^{k} B_{k}(x)\\
B_{k}(x) &= \sum_{j=0}^{3 k} A_{k, j} x^{j} \\
2 E &= \sum_{k=0}^{\infty} \varepsilon_{k} g^{k} \quad \varepsilon_{0}=1
\end{aligned}
$$

Now it is just a matter of implementing the method in a fast symbolic algorithm; otherwise, for high enough terms, it will reach the limits of the numerical arithmetic. In the end, the corrections to the energy should look like:

$$
\begin{aligned}
\delta E_{0}=&-\frac{11}{32} g^{2}-\frac{465}{512} g^{4} \\
&- \frac{39709}{8192}g^6 - \frac{19250805}{524288}g^8 - \ldots
\end{aligned}
$$

We can confront the asymptotic behaviour of the tho methods and check if they coincide.

![Confront between the two methods.](/assets/images/posts/black_perturbative_coeff_confront.png)

![Division between the coefficients](/assets/images/posts/black_perturbative_coeff_rapport.png)

Thankfully they coincide! We can see from the second graph that the two corrections tend to the same value as the perturbative order increase. Form the second graph; we can also evaluate the first-order correction of the perturbative term in 1/k. The correction could be calculated by doing a numerical fit of which the final result is:

$$
E_{k}^{(0)}=\sqrt{\frac{15}{2 \pi^{3}}}\left(\frac{15}{8}\right)^{k} \Gamma\left(k+\frac{1}{2}\right)\left(1-\frac{\delta_{0}}{k}\right) \quad \delta_{0} \simeq 1.408
$$

### Conclusions ###

Calculation the correction with the WKB approach is much more computationally efficient even though this approach still lacks the corrections to the energy on higher orders in 1/k.
