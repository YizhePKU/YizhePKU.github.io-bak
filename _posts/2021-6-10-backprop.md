# Doing Backprop by Hand

The essential reference:

* [CS231n notes on backprop](http://cs231n.github.io/optimization-2/) for visualizing the **gradient flow**, and the method of **staged computation**
* [matrix calculus notes](http://web.stanford.edu/class/cs224n/readings/gradient-notes.pdf) for **vectorizing** the computation

Useful identities:

1. If $z=Wx$, then $\frac{\partial z}{\partial x}=W$. If $z=xW$, then $\frac{\partial z}{\partial x}=W^T$.
2. If $z=Wx$ and $\delta=\frac{\partial J}{\partial z}$, then $\delta \frac{\partial z}{\partial W}=\delta^T x^T$. Doesn't works without $\delta$; $\frac{\partial J}{\partial z}$ would be a 3-dimensional tensor.
3. If $z=f(x)$ where $z$ and $x$ are vectors and $f$ is a scalar function(applied with broadcast), then $\frac{\partial z}{\partial x}=diag(f'(x))$. Useful for activation functions like ReLU.
4. If $J=CrossEntropy(y,\hat{y})$ and $\hat{y}=Softmax(\theta)$, then $\frac{\partial J}{\partial \theta}=\hat{y}-y$. It almost feels like CrossEntropy and Softmax cancels out each other.

