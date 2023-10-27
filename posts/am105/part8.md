---
layout: post
title: "ODE and PDE, Critial Points and Linearization"
date: 2021-06-01
progress: 100%
permalink: /am105/part8/
comments: true
---
[Content](https://minhuanli.github.io/notes/)

This Note borrowed a lot from section notes by Lan.

* listnotshown
{:toc}

### <i class='contrast'>Classification of Critial Points</i>

Consider the two-dimensional system of first-order linear homogeneous equations with constant coefficients. Such a system has the form:

$$
\frac{d \mathbf{x}}{d t}=\mathbf{A x}
$$

where $$\mathbf{A}$$ is a $$2 \times 2$$ matrix and $$\mathbf{x}$$ is a $$2 \times 1$$ vector. By substituting $$\mathbf{x}(t)=\boldsymbol{\xi} e^{r t}$$ into the above system, we obtain:

$$
(\mathbf{A}-r \mathbf{I}) \boldsymbol{\xi}=\mathbf{0}
$$

We thus know that $$r$$ and $$\boldsymbol{\xi}$$ are an eigenvalue-eigenvector pair of the coefficient matrix $$\mathbf{A}$$. The eigenvalues $$r$$ are the roots of the polynomial equation:

$$
\operatorname{det}(\mathbf{A}-r \mathbf{I})=0
$$

and the eigenvectors $$\boldsymbol{\xi}$$ can then be determined from the equation $$(\mathbf{A}-r \mathbf{I}) \boldsymbol{\xi}=\mathbf{0}$$ up to some multiplicative constant.

The **<i class='contrast'>critical points</i>** (or equilibrium solutions) of the system are points $$\mathbf{x}$$ where:

$$
\frac{d \mathbf{x}}{d t}=\mathbf{A} \mathbf{x}=\mathbf{0}
$$

Assume $$\det \mathbf{A} \ne 0$$,it follows that $$\mathbf{x}=\mathbf{0}$$ is the only critical point of the system. The nature of the eigenvalues of $$\mathbf{A}$$ allows us to characterize the differential equation according to the geometric pattern formed by its trajectories in a phase portrait.

I. Suppose the eigenvalues of $$\mathbf{A}$$ are real and distinct, with $$r_{1} \neq r_{2} \in \mathbb{R} .$$ The origin $$\mathbf{x}=\mathbf{0}$$ can be classified as follows: 

- If $$r_{1}, r_{2}>0$$, the origin $$\mathbf{x}=\mathbf{0}$$ is an **unstable node**

- If $$r_{1}, r_{2}<0$$, the origin $$\mathbf{x}=\mathbf{0}$$ is an **asymptotically stable node**.

- If $$r_{1}$$ and $$r_{2}$$ have opposite signs, the origin $$\mathbf{x}=\mathbf{0}$$ is an **unstable saddle**.


II. Suppose the eigenvalues of $$\mathbf{A}$$ are complex, with $$r_{1,2}=\lambda \pm i \mu .$$ The origin $$\mathbf{x}=\mathbf{0}$$ can be classified as follows:

- If $$\lambda>0$$, the origin $$\mathbf{x}=\mathbf{0}$$ is an **unstable spiral**.

- If $$\lambda<0$$, the origin the origin $$\mathbf{x}=\mathbf{0}$$ is an **asymptotically stable spiral**.

- If $$\lambda=0$$, the origin $$\mathbf{x}=\mathbf{0}$$ is a **stable center**.

III. Suppose the eigenvalues of $$\mathbf{A}$$ are equal, with $$r_{1}=r_{2}=r$$. The origin $$\mathbf{x}=\mathbf{0}$$ can be classified as follows:

- If $$r>0$$, the origin $$\mathbf{x}=\mathbf{0}$$ is a **unstable improper node**.

- If $$r<0$$, the origin $$\mathbf{x}=\mathbf{0}$$ is a **stable improper node**.

### <i class='contrast'>Autonomous System</i>

We are concerned with systems of two simultaneous differential equations of the form:

$$
\begin{array}{l}
\frac{d x}{d t}=F(x, y) \\
\frac{d y}{d t}=G(x, y)
\end{array}
$$

**<i class='contrast'>Autonomous</i>** means : The functions $$F$$ and $$G$$ in the above system do not depend on the independent variable $$t$$, but only on the dependent variables $$x$$ and $$y .$$ 

We can rewrite the system into:

$$
\frac{d \mathbf{x}}{d t}=\mathbf{f}(\mathbf{x}), \quad \mathbf{x}\left(t_{0}\right)=\mathbf{x}^{0}
$$

where $$\mathbf{x}=(x, y)^{T}, \mathbf{f}(\mathbf{x})=(F(x, y), G(x, y))^{T},$$ and $$\mathbf{x}^{0}=\left(x_{0}, y_{0}\right)^{T}$$

<p class='bluebox'>
<i style="font-weight: bold">Existence and Uniqueness Theorem</i><br>

Assume that the functions \(F\) and \(G\) are continuous and have continuous partial derivatives in some domain \(D\) of the \(x y\) -plane. If \(\left(x_{0}, y_{0}\right)\) is a point in this domain, then there exists a unique solution \(x=x(t), y=y(t)\) of the system satisfying the initial conditions \(x\left(t_{0}\right)=x_{0}, y\left(t_{0}\right)=y_{0} ;\) this solution is defined in some time interval \(I\) that contains the point \(t_0\)
</p>

The points, if any, where $$\mathbf{f}(\mathbf{x})=\mathbf{0}$$ are called critical points of the autonomous system. At such points, $$\mathbf{x}^{\prime}=\mathbf{0}$$, so critical points correspond to constant, or equilibrium, solutions of the system of differential equations. We can characterize the stability of these critical points to understand the behavior of the autonomous system.

### <i class='contrast'>Local Linearization</i>

Consider the general autonomous nonlinear system:

$$
\begin{array}{l}
\frac{d x}{d t}=F(x, y) \\
\frac{d y}{d t}=G(x, y)
\end{array}
$$

To find the critical points $$\left(x^{*}, y^{*}\right)$$ of the above system, we find points $$\left(x^{*}, y^{*}\right)$$ such that $$x^{\prime}=$$ $$F\left(x^{*}, y^{*}\right)=0$$ and $$y^{\prime}=G\left(x^{*}, y^{*}\right)=0$$ simultaneously.

To classify the stability of these critical points, we examine the behavior of small pertubations $$u(t)$$ and $$v(t)$$ around $$x^{*}$$ and $$y^{*}$$, respectively. Let:

$$
\begin{array}{l}
x=x^{*}+u(t) \\
y=y^{*}+v(t)
\end{array}
$$

Plugging in $$(x, y)=\left(x^{*}+u(t), y^{*}+v(t)\right)$$ into the above system, we have

$$
\begin{array}{l}
\frac{d x}{d t}=\frac{d}{d t}\left(x^{*}+u(t)\right)=\frac{d x^{*}}{d t}+\frac{d u}{d t}=F\left(x^{*}+u(t), y^{*}+v(t)\right) \\
\frac{d y}{d t}=\frac{d}{d t}\left(y^{*}+v(t)\right)=\frac{d y^{*}}{d t}+\frac{d v}{d t}=G\left(x^{*}+u(t), y^{*}+v(t)\right)
\end{array}
$$

since $$\frac{d x^{*}}{d t}=0$$ and $$F\left(x^{*}, y^{*}\right)=0$$, and we ignore smaller order terms in the Taylor Series expansion.

Similarly we have:

$$
\begin{aligned}
\frac{d y^{*}}{d t}+\frac{d v}{d t}=& G\left(x^{*}, y^{*}\right)+G_{x}\left(x^{*}, y^{*}\right) u+G_{y}\left(x^{*}, y^{*}\right) v+\ldots \\
& \frac{d v}{d t} \approx G_{x}\left(x^{*}, y^{*}\right) u+G_{y}\left(x^{*}, y^{*}\right) v
\end{aligned}
$$

So we have:

$$
\begin{array}{l}
\frac{d u}{d t} \approx F_{x}\left(x^{*}, y^{*}\right) u+F_{y}\left(x^{*}, y^{*}\right) v \\
\frac{d v}{d t} \approx G_{x}\left(x^{*}, y^{*}\right) u+G_{y}\left(x^{*}, y^{*}\right) v
\end{array}
$$

Rewrite into <u>a homegeneous linear system</u>:

$$
\mathbf{u}^{\prime}=\left(\begin{array}{ll}
F_{x}\left(x^{*}, y^{*}\right) & F_{y}\left(x^{*}, y^{*}\right) \\
G_{x}\left(x^{*}, y^{*}\right) & G_{y}\left(x^{*}, y^{*}\right)
\end{array}\right) \mathbf{u}
$$

So we classification the critical points $$(x^*,y^*)$$ based on the Jacobian matrix:

$$
\mathbf{J}=\mathbf{J}[F, G](x, y)=\left(\begin{array}{ll}
F_{x}\left(x^{*}, y^{*}\right) & F_{y}\left(x^{*}, y^{*}\right) \\
G_{x}\left(x^{*}, y^{*}\right) & G_{y}\left(x^{*}, y^{*}\right)
\end{array}\right)
$$

Say the eigenvalues of $$\mathbf{J}$$ are $$r_1,r_2$${% sidenote '1' 'Table 9.3.1 of Boyce & DiPrima' %}:

<img class='center' src="https://raw.githubusercontent.com/minhuanli/imagehost/master/img/image-20210305164529044.png" width="90%">