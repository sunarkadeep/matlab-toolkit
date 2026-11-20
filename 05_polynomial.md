# Polynomials in MATLAB

In MATLAB, a polynomial is represented as **a row vector of coefficients arranged in descending order of their power**.

For example, the polynomial ${}3x^3 + 2x^2 - 5x + 7{}$ is represented as
```matlab
P = [3, 2, -5, 7];
```

If a power is missing in the equation, then use 0 as placeholder value.

For example, the polynomial ${}3x^3 - 5x + 7{}$ is represented as
```matlab
P = [3, 0, -5, 7];
```

## 1. Common Functions
| Function | Syntax              | Description                                                                                                                                                                                      |
| -------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| roots    | `r = roots(P);`     | Finds the roots / zeroes of the polynomial                                                                                                                                                       |
| poly     | `P = poly(r);`      | Finds the polynomial back from the roots                                                                                                                                                         |
| polyval  | `y = polyval(P,x);` | Finds the value of polynomial at x. <br>Here x can be a scalar (single point) or a vector (e.g. `x = [1 2 3]`). <br>Here y is scalar if x is scalar, y is vector of same order if x is a vector. |
| polyder  | `dP = polyder(P);`  | Finds the derivative of the polynomial                                                                                                                                                           |
| polyint  | `iP = polyint(P);`  | Finds the integral of the polynomial                                                                                                                                                             |

## 2. Curve Fitting - polyfit
Say, there are two vectors `x,y` of same length. To find a smooth polynomial curve that best-fits the vector coordinates, use `polyfit` . It uses the [least-squares method](https://en.wikipedia.org/wiki/Least_squares) in MATLAB.

Syntax
```matlab
P = polyfit(x,y,n);
```
where, x and y are the two vectors given and `n` is the degree of fitting polynomial [1 for linear, 2 for quadratic, 3 for cubic etc].
The value of `n` must be less than the number of data points provided or in other words the length of `x,y` vectors.

Here, the output `P` is a row vector polynomial coefficients just like a standard polynomial in MATLAB.

Once the `P` vector is found, `polyval` is used to evaluate the fitted equation over a finer grid of independent (x) values to plot a smooth curve.

Sample program
```matlab
x = [-2 0 3];
y =[0 -1 4];

P = polyfit(x,y,2);
plot(x,y,'o');

hold on

x_ = -3 : 0.01 : 3;

p_ = polyval(P,x_);
plot(x_,p_);
```
## 3. Overfitting and Underfitting
When choosing the degree `n` while fitting a real world noisy data, striking the right balance is crucial. Choosing a low value of `n` fails to capture the true trend, causing Underfitting. Choosing a too high value of `n` causes an overly oscillating trend - Overfitting.


