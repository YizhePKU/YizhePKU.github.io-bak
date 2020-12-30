# Gradient checking: a validation tool

## What is gradient checking?

**Gradient checking is a technique that numerically calculates the gradient of a scalar function with respect to another scalar or vector**. (Whoa, that's a mouthful.)

## Why do we need gradient checking?

Sometimes you need to write your own backward pass and calculate gradient "by hand". Gradient checking can catch many potential errors in your implementation.

## How to perform a gradient check?

Recall the definition of a derivative:

$f'(x) = \frac{f(x+\epsilon) - f(x-\epsilon)}{2 \epsilon}$

It's straightforward to extend it to support vector derivative and implement it with numpy. Here's my implementation.

```python3
# Numerically computer gradient of function f with respect to x.
# f is a scalar function that takes x as input.
# x is an array or a scalar.
def compute_gradient(f, x):
    x = np.array(x)
    dx = np.zeros(x.size)
    for i in range(x.size):
        delta = 1e-5
        ei = one_hot(i, x.size) * delta
        x1 = x + ei
        x2 = x - ei
        dx[i] = (f(x1) - f(x2)) / (2 * delta)
    return np.reshape(dx, x.shape)
```
