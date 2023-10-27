---
layout: post
title: "Gaussain Related Intergration Trick"
date: 2021-01-27
progress: 20%
permalink: /funmath/gaussian/
comments: true
---

Some math tricks related to gaussain intergrations.

* listnotshown
{:toc}

### <i class='contrast'>Saddle point integration</i>

Target integration function: $$I= \int dx \exp{[N\phi(x)]}$$, $$N$$ is large. we can expand $$\phi(x)$$ at its maximum point{% sidenote 'id1' "$$\phi'(x_{max})=0$$" %}:

$$\begin{aligned} I &= \int dx \exp{[N\phi(x_{max})-N\frac{1}{2}\phi''(x_{max})(x-x_{max})^2]} \\ &= e^{N\phi(x_{max})}\cdot\underbrace{\int dx \exp{[-N\frac{1}{2}\phi''(x_{max})(x-x_{max})^2]}}_{\text{gaussian integration}} \\ &= e^{N\phi(x_{max})}\sqrt{\frac{2\pi}{N\phi''(x_{max})}} \end{aligned}$$

<p class="bluebox">
One important application of saddle point integration is Stirling Approximation. We have the \(\Gamma\) function form{% sidenote 'gammanote' 'This can be achieved by differentiate the equation \(\int_{0}^{\infty} d x e^{-\alpha x}=\frac{1}{\alpha}\) for \(N\) times with respect to \(\alpha\) and set \(\alpha=1\)' %}:

$$N!=\int_{0}^{\infty} d x x^{N+1} e^{-x}$$

Try yourself with saddle point integration trick to prove that:

$$\log N !=N \log N-N+\frac{1}{2} \log (2 \pi N)$$

</p>


### <i class='contrast'>Linearize term</i>

This trick appears in the replica trick to solve the Gardner's capacity:

$$
e^{-\frac{q}{2}(\sum_au_a)^2} = \int \frac{dt}{\sqrt{2\pi}}e^{-t^2/2+it\sqrt{q}\sum_{a=1}^nu_a} 
$$