---
layout: post
title: "ODE and PDE, Homogeneous ODEs"
date: 2021-02-13
progress: 100%
permalink: /am105/part5/
comments: true
---
[Content](https://minhuanli.github.io/notes/)

* listnotshown
{:toc}

### 1. General 

A general form of second order **Linear** ODE:

$$
y^{\prime \prime}+p(t) y^{\prime}+q(t) y=g(t)\tag{1}
$$

If we have $$g(t)=0$$, it is a subset of the odes, called **Homogeneous**, such that:

$$
y^{\prime \prime}+p(t) y^{\prime}+q(t) y=0\tag{2}
$$

### 2. Principle of Superpositions

Given $$y^{\prime \prime}+p(t) y^{\prime}+q(t) y=0$$, if $$y_1$$ and $$y_2$$ are two solutions of the equation. We have that:

$$y=c_{1} y_{1}(t)+c_{2} y_{2}(t) \tag{3}$$

is also a solution for any values of the constants.

Because the derivative operators are linear operators, and the equation itself is Linear. 

### 3. Wronskian Determinant

Given that equation (3) with arbitary constants $$c_1, c_2$$ are also the solution for equation (2), we can ask a question: *if all solutions are included in equation (3)?*

This can be answered with help of Wronskian determinant of $$y_1$$ and $$y_2$$ at some point $$t_0$$:

$$
W=\left|\begin{array}{ll}
y_{1}\left(t_{0}\right) & y_{2}\left(t_{0}\right) \\
y_{1}^{\prime}\left(t_{0}\right) & y_{2}^{\prime}\left(t_{0}\right)
\end{array}\right|=y_{1}\left(t_{0}\right) y_{2}^{\prime}\left(t_{0}\right)-y_{1}^{\prime}\left(t_{0}\right) y_{2}\left(t_{0}\right)\tag{4}
$$

If and only if there is a point $$t_0$$ in the interval where $$W$$ is **not zero**, we can say all solutions are included in the above equation (3) {% sidenote '1' 'think it as independent bases in 2d spaces' %}


### 4. Constant Coefficients Homogeneous ODEs

Given an equaion in form: 

$$
a y^{\prime \prime}+b y^{\prime}+c y=0 \tag{5}
$$

Let $$r_1$$ and $$r_2$$ be the roots of the cooresponding characteristic equation:

$$
a r^{2}+b r+c=0 \tag{6}
$$

It falls into three types:


1. $$r_1$$ and $$r_2$$ are real and not equal{% sidenote '2' 'positive discriminant' %}, the general solution of equation (5) is:

    $$
    y=c_{1} e^{r_{1} t}+c_{2} e^{r_{2} t}\tag{7}
    $$

2. $$r_1$$ and $$r_2$$ are complex numbers{% sidenote '3' 'negative discriminant' %}, the general solution of equation (5) is:
    
    $$
    y=c_{1} e^{\lambda t} \cos (\mu t)+c_{2} e^{\lambda t} \sin (\mu t)\tag{8}
    $$

3. $$r_1=r_2$$ {% sidenote '4' 'zero discriminant' %}, the general solution is:

    $$
    y=c_{1} e^{r_{1} t}+c_{2} t e^{r_{1} t}\tag{9}
    $$


