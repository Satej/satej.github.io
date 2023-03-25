---
layout: post
title:  "Python for differential calculus"
date:   2023-03-25 00:00:00 +0000
categories: python differential calculus
---
Many would have known about using differential calculus in Maths. How do we use it with Python? Well, sympy and scipy can help us here.

Sympy is used to create symbols for our x, y variables while Scipy helps with the differential bit.

These can be installed using below command:
```sh
pip install sympy scipy
```

Next, import them:
```python
from sympy import *
from scipy.misc import derivative
```

Create a symbol and use it to create an equation:
```python
x = Symbol('x')
Fx = 7*x**3+x**2+1
```

Using scipy differentiate it:

```python
Derivative(Fx,x).doit()
```

To create a derivative at a point:
```python
def f(x):
    return 7*x**3+x**2+1
derivative(f,1.0)

def f(x):
    return 7*x**3+x**2+1
derivative(f,1.0)
```

An example of Partial Derivatives:

```python
x, y, z = symbols('x, y, z', real=True)
f = x**2 + y**3 + z**4 + 5*x*y*z
f
```

Create derivative with respect to each variable:
```python
for var in [x, y, z]:
    print(" f_" + str(var) + "=", f.diff(var))
```

Hope it helps and you explore more. Please do share! :)