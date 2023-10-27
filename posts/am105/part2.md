---
layout: post
title: "ODE and PDE, Basics II"
date: 2021-01-28
progress: 100%
permalink: /am105/part2/
comments: true
---
[Content](https://minhuanli.github.io/notes/)
* listnotshown
{:toc}

### 1. Separable Differential Equations

Set $$x$$ as the independent variable and $$y$$ is a function of $$x$$, we can generally write the first-order differential equation in the following form:

$$
M(x, y)+N(x, y) \frac{d y}{d x}=0\tag{1}
$$

where $$M$$ and $$N$$ are two functions of $$x$$ and $$y$$. Let's say, when $$M$$ is a function of $$x$$ and $$N$$ is the function of $$y$$ only, equation (1) becomes:

$$
M(x)dx + N(y)dy = 0 \tag{2}
$$

<p class='bluebox'>
Not quite easy actually, details here:

$$
\begin{aligned}
M(x)dx + N(y)dy &= 0 \\[2ex]
\implies \frac{d H_1(x)}{dx}dx + \frac{dN(y)}{dy}dy &= 0 \\
\implies dH_1(x) + dH_2(y) &= 0 \\
\implies d(H_1(x) + H_2(y)) &= 0 \\
\implies H_1(x) + H_2(y) &= c
\end{aligned}
$$
</p>

This can be easily integrated to solution:



$$
H_{1}(x)+H_{2}(y)=c \tag{3}
$$

where $$H_{1}(x) = \int M(x) dx$$ and $$H_{2}(y) = \int N(y) dy$$. The constant $$c$$ is determined by the initial value.

<p class='redbox'>
An example, we want to solve the following first-order differential equation:

$$
\frac{d y}{d x}=\frac{x^{2}}{1-y^{2}}
$$

which is apparently separable.<br>

<i class="contrast">Solution:</i><br>

Rewrite it in the form of equation (2):

$$
-x^{2}dx+\left(1-y^{2}\right)dy=0
$$

So:

$$
H_{1}(x) = \int (-x^2) dx = -\frac{1}{3}x^3 + c_1 \\ H_{2}(y) = \int (1-y^2) dy = y-\frac{1}{3}y^3 + c_2
$$

We have:

$$
-\frac{1}{3}x^3 + y - \frac{1}{3}y^3 = c
$$

Constant is determined by some boudnary condistions

</p>


### 2. Existence and Uniqueness Theorem

<p class='bluebox'>
For a <i style="font-weight: bold;">first-order linear equation</i>, as long as functions \(p\) and \(g\) are <i class='contrast'>continuous</i> on an open interval \(I, \alpha< t < \beta\) with \(t=t_0\) inside, there exists a <i class='contrast'>unique</i> function \(y=\phi(t)\) satisfies:

$$y'+p(t)y=g(t)$$

for each \(t\) in \(I\), and also satisfies initial condition \(phi(t_0) = y_0\) when an arbitary initial value \(y_0\) is given. 
</p>

<p class='bluebox'>
For a <i style="font-weight: bold;">first-order non-linear equation</i>, as long as functions \(f\) and \(\partial f/\partial y\) are <i class='contrast'>continuous</i> in some open rectangle \( \alpha< t < \beta, \gamma < y < \delta\) with \( (t_0,y_0) \) inside, there exists a <i class='contrast'>unique</i> function \(y=\phi(t)\) in some interval \( t_{0}-h< t < t_{0}+h \){% sidenote 'illu' 'say, a small interval around initial point \(t=t_0\)' %} containing \(\alpha < t < \beta\) satisfies:

$$y' = f(t,y), \quad \text{with } \phi(t_0) = y_0$$

</p>

One note here: breaking of the conditions in the above two theorems does not mean there is no solutions, there could possibally be multiple solutions{% sidenote '1' 'See B&D Book, Chap 2.4, Example 2, Page 53.' %}.

[Next](https://minhuanli.github.io/notes/am105/part3/)
