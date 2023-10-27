---
layout: post
title: "Hamiltonian Monte Carlo"
date: 2021-06-05
progress: 100%
permalink: /stat/HMC/
comments: true
---

Hamiltonian monte carlo is a physics-inspired sampling algorithm. This is a note based on Harvard AM207 course{% sidenote '1' '20 Fall, taught by Weiwei Pan' %} about the HMC motivation and algorithm.

* listnotshown
{: toc}

### <i class='contrast'>Motivation</i>

When we are dealing with sampling from target distribution $$\pi(q)$$ in a complex model, naive Metropolic-Hastings MCMC might be inefficient as most proposed new samplers might be rejected. Hamiltonian Monte Carlo, perhaps, is the least complicated algorithm to fix such issues.

In statistical physics, system energy $$U(q)$$ can be related to the probability $$\pi(q)$$ with Gibbs distribution (or Boltzmann distribution):

$$
\pi(q)=\frac{1}{Z} \exp \left\{-\frac{U(q)}{T}\right\}, \quad T \text { is a constant } \tag{1}
$$

where $$Z$$ is the normalizing constant of the exponential part{% sidenote '2' '"partition function" in physics field' %}. The Gibbs distribution has a physical interpretation: $$\pi(q)$$ is the likelihood of being in state $$q$$ given the energy $$U(q)$$ of state $$q$$ and the temperature $$T$$. For now, we set $$T=1$$. 

Using the same relationship, we can turn a probability distribution into an energy function:

$$
U(q)=-\log \pi(q) \tag{2}
$$

Such energy form can thus define a Hamiltonian system, which we can use as a dynamic rule to propose new states.  

<p class='redbox'>
<i style="font-weight: bold">Hamiltomian system</i><br>
A physical properties of system with position \(q(t)\) and momentum \(p(t)\) is described by a function \(H(q, p)\) called the Hamiltonian. We will always choose a Hamiltonian that decomposes as the sum of potential and kinetic energy as follows:

$$
\underbrace{H(q, p)}_{\text {total }}=\underbrace{U(q(t))}_{\text {potential }}+\underbrace{K(p(t))}_{\text {kinetic }}
$$

How the system \((q, p)\) changes over time is described by the partial derivatives of \(H\) :

$$\frac{d q}{d t}=\underbrace{\frac{\partial H}{\partial p}}_{\text {function of } t}, \quad \frac{d p}{d t}=\underbrace{-\frac{\partial H}{\partial q}}_{\text {function of } t}$$

The time-reversal symmetry and Liouville's theorem in Hamiltonian system corresponds to the reversibility and volume preserving properties used to endorsing the correctness of HMC sampler.
</p>

### <i class='contrast'>HMC with exact integration</i>

Let $$\pi(q)$$ be our target distribution with $$q \in \mathbb{R}^{D}$$. We turn $$\pi$$ into an energy function $$U(q)$$ by $$U(q)=-\log (\pi(q))$$. We choose a kinetic energy function $$K(p) .$$ We fix $$t=T$$.

$$\;$$ I. Start with a random $$q^{(0)} \in \mathbb{R}^{D}$$

$$\;$$ II. Repeat:

1. (**kick-off**) sample a random momentum from the Gibbs distribution of $$K(p)$$, i.e. $$p^{(\text {current })} \sim \frac{1}{Z} \exp \{-K(p)\}$$.

2. (**simulate movment**) simulate Hamiltonian motion for a time interval of length $$T$$, i.e. start at $$\left(q^{(\text {current })}, p^{(\text {current })}\right)$$ and find $$\left(q^{(\text {time } T)}, p^{(\text {time } T)}\right)$$. You need to integrate $$\frac{d q}{d t}=\frac{\partial H}{\partial p}, \frac{d p}{d t}=-\frac{\partial H}{\partial q} !$$

3. accept $$q^{(\text {current })}$$ as a new sample: $$q^{(\text {current })} \leftarrow q^{(\text {time } T)}$$.

<p class='greenbox'>
<i style='font-weight: bold'>Note</i>: 
Generally, MD simulation can also be viewed as a HMC sampler.
</p>

### <i class='contrast'>HMC with the leap frog Integrator</i>

The analytical integration in the above II.2 step is intractable, so we have to use some approximation methods like discretizing the time period $$[0, T]$$ into $$L$$ chunks each with length $$\epsilon$$. But as the approximation (especially for long time $$T$$) is not accurate, to ensure the correctness of the sampling, we need to **add a Metropolis-Hastings step** so that we can potentially reject the sample from the approximation.

Let $$\pi(q)$$ be our target distribution with $$q \in \mathbb{R}^{D}$$. We turn $$\pi$$ into an energy function $$U(q)$$ by $$U(q)=-\log (\pi(q)) .$$ We choose a kinetic energy function $$K(p)$$.

$$\; $$ I. start with a random $$q^{(0)} \in \mathbb{R}^{D}$$

$$\; $$ II. repeat:

$$\quad$$1. (**kick-off**) sample a random momentum from the Gibbs distribution of $$K(p)$$, i.e. $$p^{(\text {current })} \sim \frac{1}{Z} \exp (-K(p))$$

$$\quad$$2. (**simulate movement**) simulate Hamiltonian motion for $$L$$ steps each with time interval $$\epsilon$$, using the leap-frog integrator:

$$\qquad \quad$$ a. Repeat for $$\mathrm{T}-1$$ times{% sidenote '3' 'for $$p^{(\text {step } 0)}=p^{(\text {current })}, q^{(\text {step } 0)}=q^{(\text {current })}$$' %}:

$$\qquad \quad \quad$$ i. $$p^{(\text {step } t+1 / 2)} \leftarrow p^{(\text {step } t)}-\epsilon / 2 \frac{\partial U}{\partial a}\left(q^{(\text {step } t)}\right)$${% sidenote '4' 'half-step update for momentum' %}

$$\qquad \quad \quad$$ ii. $$q^{(\text {step } t+1)} \leftarrow q^{(\text {step } t)}+\epsilon \frac{\partial K}{\partial p}\left(p^{(\text {step } t)}\right)$${% sidenote '5' 'full-step update for position' %}

$$\qquad \quad \quad$$ iii. $$p^{(\text {step } t+1)} \leftarrow p^{(\text {step } t+1 / 2)}-\epsilon / 2 \frac{\partial U}{\partial q}\left(q^{(\text {step } t+1)}\right)$${% sidenote '6' 'half-step update for momentum' %}

$$\qquad \quad$$ b. (**reverse momentum**) $$p^{(\text {step } T)} \leftarrow-p^{(\text {step } T)}$$

$$\quad$$3. (**correction for error**) implement Metropolis-Hasting accept mechanism:

$$\qquad \quad$$ a. compute $$\alpha=\min \left(1, \exp \left\{-\Delta H\right\}\right)$${% sidenote '7' '$$\Delta H = H\left(q^{(\text {step } T)}, p^{(\text {step } T)}\right)-H\left(q^{(\text {current })}, p^{(\text {current })}\right)$$' %}

$$\qquad \quad$$ b. sample $$U \sim U(0,1)$$, if $$U \leq \alpha$$ then accept, else keep old sample.