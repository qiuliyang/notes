---
layout: post
title: "ODE and PDE, Numerical Approximations II"
date: 2021-02-12
progress: 100%
permalink: /am105/part4/
comments: true
---
[Content](https://minhuanli.github.io/notes/)

* listnotshown
{:toc}

### 1. Improved Euler Method

As we know before, local truncation error is of $$O(h^2)$$ for normal Euler Method. However, we can't simply decrease the step size $$h$$ to reduce the local truncation error, because of the rounding error and limited computational resources. So we need some other approximate approaches to give good results even if the step size is not small enough. They actually all center around how to approximate the integration (slope).

First is the improved Euler method, given the ODE in form:

$$
\frac{d y}{d t}=f(t, y), \quad y(t_0) = y_0\tag{1}
$$

We use the average of the two endpoints of the definite integral instead of the left endpoint:

$$
\begin{aligned}
y_{n+1} &=y_{n}+\frac{f\left(t_{n}, y_{n}\right)+f\left(t_{n+1}, y_{n+1}\right)}{2} h \\
y_{n+1}=y_{n}+& \frac{f\left(t_{n}, y_{n}\right)+f\left(t_{n}+h, y_{n}+h f\left(t_{n}, y_{n}\right)\right)}{2} h \\
y_{n+1} &=y_{n}+\frac{f_{n}+f\left(t_{n}+h, y_{n}+h f_{n}\right)}{2} h
\end{aligned} \tag{2}
$$  

The local truncation error is of order $$O(h^3)$$, on orde magnitude smaller than normal Euler method.

### 2. Runge-Kutta Method

The Euler formula and improved Euler formula are part of what is called the Runge-Kutta class of methods. This method is now called classic fourth-order four-square Runge-Kutta method. This method can be summarized for equation (1), as:


$$
y_{n+1}=y_{n}+h\left(\frac{k_{n 1}+2 k_{n 2}+2 k_{n 3}+k_{n 4}}{6}\right) \tag{3}
$$

where

$$
\begin{aligned}
k_{n 1} &=f\left(t_{n}, y_{n}\right) \\
k_{n 2} &=f\left(t_{n}+\frac{1}{2} h, y_{n}+\frac{1}{2} h k_{n 1}\right) \\
k_{n 3} &=f\left(t_{n}+\frac{1}{2} h, y_{n}+\frac{1}{2} h k_{n 2}\right) \\
k_{n 4} &=f\left(t_{n}+h, y_{n}+h k_{n 3}\right)
\end{aligned} \tag{4}
$$

The local truncation error is of order $$O(h^5)$$, much smaller.


<p class='redbox'>
The comparison of improved Euler method and Runge-Kutta method to approximate the solution for:

$$y^{\prime}=1-t+4 y, \quad y(0)=1$$

<img class='center' src='https://raw.githubusercontent.com/minhuanli/imagehost/master/img/Screen%20Shot%202021-02-12%20at%205.19.34%20PM.png' width="100%"> 


Note also that the Runge-Kutta method with \(h = 0.2\), or 40 evaluations of \(f\), produces a value at \(t = 2\) with an error of \(1.40%\), which is only slightly greater than the error in the improved Euler method with \(h = 0.025\), or 160 evaluations of \(f\). Thus we see again that a more accurate algorithm is more efficient; it produces better results with similar effort, or similar results with less effort.
</p>