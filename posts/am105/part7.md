---
layout: post
title: "ODE and PDE, Systems of ODEs"
date: 2021-04-11
progress: 100%
permalink: /am105/part7/
comments: true
---
[Content](https://minhuanli.github.io/notes/)

* listnotshown
{:toc}


### 1. Systems of first-order linear equations

Equations of higher order can always be transformed into systems of first order equations. To transform an arbitray $$n^{th}$$ order equation:

$$
y^{(n)}=F\left(t, y, y^{\prime}, \ldots, y^{(n-1)}\right)\tag{1}
$$

into a system of $$n$$ first-order differential equations by introducing the variables $$x_{1}, x_{2}, \ldots, x_{n}$$ defined by:

$$
x_{1}=y, x_{2}=y^{\prime}, x_{3}=y^{\prime \prime}, \ldots, x_{n}=y^{(n-1)} \tag{2}
$$

It follows immediately that:

$$
\begin{array}{c}
x_{1}^{\prime}=x_{2} \\
x_{2}^{\prime}=x_{3} \\
\vdots\\
x_{n-1}^{\prime}=x_{n} \\
x_{n}^{\prime}=F\left(t, x_{1}, x_{2}, \ldots, x_{n}\right) 
\end{array} \tag{3}$$

A more general case of such n first-order **linear** differential equation has the form:

$$
\begin{aligned}
x_{1}^{\prime} &=p_{11}(t) x_{1}+\cdots+p_{1 n}(t) x_{n}+g_{1}(t), \\
x_{2}^{\prime} &=p_{21}(t) x_{1}+\cdots+p_{2 n}(t) x_{n}+g_{2}(t), \\
&\vdots \\
x_{n}^{\prime} &=p_{n 1}(t) x_{1}+\cdots+p_{n n}(t) x_{n}+g_{n}(t) .
\end{aligned} \tag{4}
$$

If each of the functions $$g_{1}(t), \ldots, g_{n}(t)$$ is zero for all $$t$$ in the interval $$I$$, then the system
(4) is said to be <i class='contrast'>homogeneous</i>; otherwise, it is <i class='contrast'>nonhomogeneous</i>.

A homogeneous first-order linear system can be further expressed in a matrice form:

$$
\mathbf{x}^{\prime}=\mathbf{A x} \tag{5}$$

### 2. Homogeneous Linear System with Constant Coefficients
The general solution to $$\mathbf{x}^{\prime}=\mathbf{A x}$$ is $$\mathbf{x} = \mathbf{\xi}e^{rt}$$, where $$r$$ is an eigenvalue and $$\boldsymbol{\xi}$$ an associated eigenvector of the coefficient matrix $$\mathbf{A}$$.

- **Real and different eigenvalues**

If the $$n$$ eigenvalues of matrix $$\mathbf{A}$$ are all real and different. Thus, associated with each eigenvalue $$r_{i}$$ is a real eigenvector $$\boldsymbol{\xi}^{(i)}$$, and the $$n$$ eigenvectors $$\boldsymbol{\xi}^{(1)}, \ldots, \boldsymbol{\xi}^{(n)}$$ are linearly independent. The corresponding general solution of the differential system equation (5) is:

$$
\mathbf{x}=c_{1} \boldsymbol{\xi}^{(1)} e^{r_{1} t}+\cdots+c_{n} \boldsymbol{\xi}^{(n)} e^{r_{n} t} \tag{6}
$$

- **Complex-valued eigenvalues**

Suppose that there is one pair of complex conjugate eigenvalues of $$\mathbf{A}$$, $$r_{1}=\lambda+i \mu$$ and $$r_{2}=\lambda-i \mu .$$ Then the corresponding eigenvectors $$\boldsymbol{\xi}^{(1)}$$ and $$\boldsymbol{\xi}^{(2)}$$ are also complex conjugates. Let us write $$\boldsymbol{\xi}^{(1)}=\mathbf{a}+i \mathbf{b}$$, where $$\mathbf{a}$$ and $$\mathbf{b}$$ are real; then we can write: $$\mathbf{x}^{(1)}(t)=\mathbf{u}(t)+i \mathbf{v}(t)$$, where:

$$
\begin{array}{l}
\mathbf{u}(t)=e^{\lambda t}(\mathbf{a} \cos (\mu t)-\mathbf{b} \sin (\mu t)) \\
\mathbf{v}(t)=e^{\lambda t}(\mathbf{a} \sin (\mu t)+\mathbf{b} \cos (\mu t))
\end{array}
$$

Assume all other eigenvalues $$r_3,\dots,r_n$$ are real and distinct, then the general solution is:

$$
\mathbf{x}=c_{1} \mathbf{u}(t)+c_{2} \mathbf{v}(t)+c_{3} \boldsymbol{\xi}^{(3)} e^{r_{3} t}+\cdots+c_{n} \boldsymbol{\xi}^{(n)} e^{r_{n} t} \tag{7}
$$

- **Repeated eigenvalues**

When the matrix $$\mathbf{A}$$ has a repeated eigenvalue, say that $$r=\rho$$ is an $$m$$-fold eigenvalue. In this event, there are two possibilities: either there are $$m$$ linearly independent eigenvectors corresponding to the eigenvalue $$\rho$$, or else, there are fewer than $$m$$ linearly independent eigenvectors.

In the first case, it makes no difference that the eigenvalue $$r = \rho$$ is repeated as the distinct case, still has the general solution like equation (6).

In the second case, if the matrix $$\mathbf{A}$$ is not Hermitian{% sidenote '1' 'for example $$\mathbf{A}= 
\left(\begin{array}{rr}
1 & -1 \\
1 & 3
\end{array}\right)
$$' %}, then there may be fewer than $$m$$ idependent eigenvevtors corresponding to the eigenvalue $$\rho$$. We have dealt with similar situations for linear equation [here](../part5/#4-constant-coefficients-homogeneous-odes). 

Suppose that $$r=\rho$$ is a <i class='contrast'>double</i> eigenvalue of $$\mathbf{A}$$, but that there is only one corresponding eigenvector $$\boldsymbol{\xi} .$$ Then one solution is:

$$
\mathbf{x}^{(1)}(t)=\boldsymbol{\xi} e^{\rho t}
$$

We need to find a second solution:

$$
\mathbf{x}^{(2)}(t)=\boldsymbol{\xi} t e^{\rho t}+\boldsymbol{\eta} e^{\rho t}
$$

where $$\eta$${% sidenote '2' 'The vector $$\eta$$ is called a generalized eigenvector of the matrix $$\mathbf{A}$$ corresponding to the eigenvalue $$\rho$$.' %} is determined from:

$$
(\mathbf{A}-\rho \mathbf{I}) \boldsymbol{\eta}=\boldsymbol{\xi}
$$






