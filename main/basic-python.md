% Basic Python

[Back](index.md)

## Numpy
NumPy is the fundamental package for scientific computing with Python. It contains among other things:

* A powerful $N$-dimensional array object.
* Sophisticated (broadcasting) functions.
* Tools for integrating C/C++ and Fortran code.
* Useful linear algebra, Fourier transform, and random number capabilities.

Besides its obvious scientific uses, NumPy can also be used as an efficient multi-dimensional container of generic data. Arbitrary data-types can be defined. This allows NumPy to seamlessly and speedily integrate with a wide variety of databases.

The official site is [http://www.numpy.org](http://www.numpy.org).

You can find more about numpy in the [jupyter site](https://nbviewer.org/github/sbustamante/ComputationalMethods/blob/master/material/scientific-libraries.ipynb).

### Supported methods for lists
```python
x.append   x.count    x.extend   x.index    x.insert   x.pop      x.remove   x.reverse  x.sort
```

### Supported methods for Numpy arrays

```python
x.T             x.clip          x.dot           x.item          x.prod          x.setfield      x.take
x.all           x.compress      x.dtype         x.itemset       x.ptp           x.setflags      x.tofile
x.any           x.conj          x.dump          x.itemsize      x.put           x.shape         x.tolist
x.argmax        x.conjugate     x.dumps         x.max           x.ravel         x.size          x.tostring
x.argmin        x.copy          x.fill          x.mean          x.real          x.sort          x.trace
x.argsort       x.ctypes        x.flags         x.min           x.repeat        x.squeeze       x.transpose
x.astype        x.cumprod       x.flat          x.nbytes        x.reshape       x.std           x.var
x.base          x.cumsum        x.flatten       x.ndim          x.resize        x.strides       x.view
x.byteswap      x.data          x.getfield      x.newbyteorder  x.round         x.sum           
x.choose        x.diagonal      x.imag          x.nonzero       x.searchsorted  x.swapaxes
```

Unlike usual lists, Numpyu arrays acts such as matrix elements of $\mathbb{R}^n\times\mathbb{R}^n$. For instance, you can see the difference between the following operations:

```python
#Operator + for lists is overloaded for concatenating 
x1 = [1,2,3]
x2 = [3,2,1]
print(x1+x2)
```
This leads to:

```python
[1, 2, 3, 3, 2, 1]
```

Now, with NumpyArrays, we obtain the following:

```python
import numpy as np
#Operator + for numpy arrays is overloaded for adding
x1 = np.array([1,2,3])
x2 = np.array([3,2,1])
print(x1+x2)
```

Output:

```python
[4 4 4]
```

Notice that operator `+` acts such as acts the sum in a $\mathbb{R}$ field.

## SciPy
SciPy is a collection of mathematical algorithms and convenience functions built on the Numpy extension of Python. It adds significant power to the interactive Python session by providing the user with high-level commands and classes for manipulating and visualizing data. With SciPy an interactive Python session becomes a data-processing and system-prototyping environment rivaling sytems such as MATLAB, IDL, Octave, R-Lab, and SciLab.

Some of the packages included with SciPy are:

* Special functions (`scipy.special`)
* Integration (`scipy.integrate`)
* Optimization (`scipy.optimize`)
* Interpolation (`scipy.interpolate`)
* Fourier Transforms (`scipy.fftpack`)
* Signal Processing (`scipy.signal`)
* Linear Algebra (`scipy.linalg`)
* Each of these packages must be imported separately.

Each of these packages must be imported separately.

For a most extensive exposition about SciPy, see the [jupyter site](https://nbviewer.org/github/sbustamante/ComputationalMethods/blob/master/material/scientific-libraries.ipynb), and its official page in [http://www.scipy.org](http://www.scipy.org).

The integrate package then includes the next functions:

```python
integ.Tester        integ.fixed_quad    integ.odepack       integ.quadrature    integ.test          
integ.complex_ode   integ.newton_cotes  integ.quad          integ.romb          integ.tplquad       
integ.cumtrapz      integ.ode           integ.quad_explain  integ.romberg       integ.trapz         
integ.dblquad       integ.odeint        integ.quadpack      integ.simps         integ.vode  
```

Almost each of the numerical methods that will be covered during the course can be found in SciPy.

## `matplotlib` library

### Stating subfigures

To plotting subfigures with `matplotlib`, we may write the following init code:
```python
import matplotlib.pyplot as plt

#-----
#Define here functions to plot
#-----

fig = plt.figure()
ax = fig.add_subplot(111) #Plot a subfigure in 1 row, 1 column and labeled as 1.
```

If we check the type of element created, then we obtain:

```python
type(fig) #<class 'matplotlib.figure.Figure'>
type(ax) #<class 'matplotlib.axes._subplots.AxesSubplot'>
```

But it is more simple if we write:

```python
fig, ax = plt.subplots(nrows = a, ncols = b)
```

which will to create a set of  subfigures ordered in `a` rows and `b` columns.

### Sharing ticks and axis labels

Writing the loop

```python
for ax in axs.flat:
    ax.label_outer()
```

subfigures will share labels, and writing the loop

```python
for ax in fig.get_axes():
    ax.label_outer()
```

subfigures will share x-ticks and y-ticks.

But is more simple if only writing the argument `sharex=True` or `sharey=True` into `plt.subplots` argument.

Another way to share axes among specific subplots pair, we write: `ax[a,b].sharex(ax[n,m])`

### Subplots adjustment

To adjust properly each subplot, we can modify the code as follow:

```python
fig = plt.figure()
gs = fig.add_gridspec(2, 2, hspace=0, wspace=0)
(ax1, ax2), (ax3, ax4) = gs.subplots(sharex='col', sharey='row')
```

### Polar axes

In order to stablish the plane as polar, we must add to `plt.subplots` argument the following option 
```pyhton
subplot_kw=dict(projection='polar')
```

## Basic Activity

I solved the basic activity proposed in the [reference repository](https://github.com/sbustamante/ComputationalMethods/blob/master/material/Basic_exercises.ipynb). The full solution is in the notebook: [solution](ipynb/basic-activity-solution.ipynb).

---
[Back](index.md)
