# Gaussian functions and their derivatives
  ----
Using NumPy, it is possible to do this exercise without using a single (Python) loop. The normalized Gaussian function with mean µ and standard deviation σ is


$$g(x)=\frac{1}{\sigma\sqrt{2\pi}}\exp{-\left(\frac{(x-\mu)^2}{2\sigma^2}\right)}$$


Write a program to calculate and plot the Gaussian functions with µ = 0 and the three values σ = 0.5, 1, 1.5. Use a grid of 1000 points in the interval −10 ≤ x ≤ 10.
Verify (by direct summation) that the functions are normalized with area 1. Finally, calculate the first derivative of these functions on the same grid using the first-order central difference approximation:

 $$g'(x)\approx\frac{g(x+h)-g(x-h)}{2h}$$
for some suitably chosen, small h.



My solution is shown below. I have used Google Colab to execute the following python code.
### SOLUTION: 
```python
import numpy as np
import matplotlib.pyplot as plt

#Define the variables
mu= 0
s = np.array([0.5,1,1.5])
x, dx = np.linspace(-10,10,1000, retstep=True)     #restep for dx


#Define the gaussian fn
def gaussian(x,s,mu):
  return 1./(s*np.sqrt(2*np.pi)) * np.exp(-0.5*((x-mu)/s)**2)

# transforming x by increasing its dim
x = x[:, np.newaxis]
y = gaussian(x,s,mu)

#Verify that this normalize to 1, direct summation along x axis
int_y= np.sum(gaussian(x,s,mu),axis =0) * dx
print('If these numbers are 1 (or close to it), then the g(x) is normalized:')
print(int_y)

# Numerical differentiation by the first-order central difference formula
h = 1.e-6   # we need some suitably small h
dydx = (gaussian(x+h, s, mu) - gaussian(x-h, s, mu))/2/h    #given in the problem

plt.plot(x, y)
plt.plot(x, dydx)

plt.show()
```
**The plot output of this code is given by "gaussian.png" file in this folder.**



