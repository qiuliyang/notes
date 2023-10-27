---
layout: post
title: "ODE and PDE, Numerical Approximations I"
date: 2021-02-03
progress: 100%
permalink: /am105/part3/
comments: true
---
[Content](https://minhuanli.github.io/notes/)

* listnotshown
{:toc}


### 1. Direction Field

Direction fields are valuable tools in studying the solutions of differential equations of the form:

$$
\frac{d y}{d t}=f(t, y)\tag{1}
$$

where $$f$$ is a given function of the two variables $$t$$ and $$y$$, sometimes referred to as the **rate function**. A direction field for equations (1) can be constructed by evaluating $$f$$ at each point of a rectangular grid. At each point of the grid, a short line segment is drawn whose slope is the value of $$f$$ at that point. Each line segment is tangent to the graph of the solution passing through that point. The plots give you a general intuition about what does the solution look like. 

<p class='redbox'>
Like example on B&D book, page 5, the direction field of equation:

$$
\frac{d p}{d t}=\frac{p}{2}-450
$$

<img class='center' src='https://raw.githubusercontent.com/minhuanli/imagehost/master/img/direction_field.png' width="70%"> 
</p>

### 2. Euler's Method

For a first-order IVP given $$f$$ and $$\partial f /\partial y$$ are continuous:

$$
\frac{d y}{d t}=f(t, y), \quad y\left(t_{0}\right)=y_{0} \tag{2}
$$

there are two facts driving the numerical approximations approaches:{% sidenote '1' 'from existence and uniqueness theorem' %}

1. There is a unique solution $$y=\phi(t)$$ in some interval around $$t=t_0$$

2. It is usually not possible to find the $$\phi$$ by symbolic manipulations.

From the diretive fied plotted above, we could imagine that if we have a fine enough grid, it presents a reasonable approximation of the solution, which motivates the Euler's method as numerical approximation to equation (2)'s solution{% sidenote '2' "The formalized approximation here is $$f'(t) = \frac{f(t+\Delta t)-f(t)}{\Delta t}$$. There are many forms of this truncation approximation, with different levels of error." %}:

1. Start from the initial point $$(t_0, y_0)$$

2. Move a small step further $$t_1 = t_0 + \Delta t$$:
   <br>$$y_1 = y_0+f(t_0,y_0)\Delta t$$

3. Iteratively move the point further like above:
    <br>$$y_n = y_{n-1}+f(t_{n-1},y_{n-1})\Delta t$$

Now you have the a bunch of points $$(t_i,y_i), i = 0, \dots,n$$, starting from initial value $$(t_0,y_0)$$. Connect them with segemental lines, then you have one numerical approximation. The local truncation error level is $$O(h^2)$$.

<p class='redbox'>
Example from B&D book section 2.7, example 1, page 78. Use Euler's method to solve:

$$
\frac{d y}{d t}=3-2 t-0.5 y, \quad y(0)=1
$$

Evaluate at five points \((0,0.2,0.4,0.6,0.8,1.0)\):

<img class='center' src="https://raw.githubusercontent.com/minhuanli/imagehost/master/img/Screen%20Shot%202021-02-03%20at%205.16.18%20PM.png" width="70%">

You can see the error gap grows larger as \(t\) increases, because the truncation error is accumulating.
</p>

