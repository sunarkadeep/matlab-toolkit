# 1. Symbolic Computing
The `syms` command tells MATLAB to treat variables as algebraic symbols than normal variables. This allows to perform algebraic computation without dealing with floating point numbers and hence be void of rounding errors.

For example,
```matlab
syms x
y = log(x);

syms a b
c = cos(a) + sin(b);
```
### a. Finding roots
The `solve()` command is used to solve a given equation.
```matlab
syms x
f = 2*x^2 + 3*x -2;

roots = solve(f==0,x);
```
# 2. Solving Linear Equations
Say three equations of three variables are given, to solve for them we define two matrices - 
- `A` - the coefficient matrix
- `B` - the constant term matrix

To solve, we use the following - 
```matlab
A = [1 2 3; -1 2 -2; 2 -1 1];
B = [3; -4; 1];

X = A\b %method 1
X = inv(A) * B; %method 2
```
# 3. Differentiation
To find the derivative, the `diff()` function is used.
Syntax - `diff(expression , var, order)` here,
- `var` is the variable wrt which the derivate is required
- `order` is the order of differentiation, e.g. 1,2,3,4; *for 1, no need to specify*
For example,
```matlab
syms x y
f = x^3 + 4*x*y -5*x + 7;

dfx = diff(f,x);
%1st order derivative wrt x 

d2fx = diff(f,x,2);
%2nd order derivative wrt x

dfy = diff(f,y);
%1st order derivative wrt y
```
## a. For discrete domain
```matlab
x = 0:0.01:2*pi;
y = cos(x);

dydx = diff(y)./diff(x);
```
## b. `diff( )` on matrix
`diff()` can operate on matrices as well - 
```matlab
A = [ ... ] % A is a nxm matrix
dA = diff(A,X,Y);
```
Here,
- `X` is the order of difference
- `Y` is the dimension of operation - 1 for row, 2 for column, as followed in MATLAB.
# 4. Integration
To find the integral, the `int()` function is used.
Syntax - `int(expression , var, a, b)` here,
- `var` is the variable wrt which the derivate is required
- `a` and `b` are lower & upper limits respectively for definite integration; *optional*

For example,
```matlab
syms x
f = 3*x^2 + 2*x;

Fi = int(f,x) %indefinite integration
Fd = int(f,x,0,3); %definite integration
```
## a. Other scenarios of integration
**Function declared using @(var)**
```matlab
f = @(x) sin(x);
result = integral(f,0,pi);
```
**Approximate area under curve formed by discrete data points**
```matlab
x = linspace(0,2,50);
y = x.^2;

result = trapz(x,y);
```
**Adaptive Simson's quadrature**
```matlab
q = quad( @(x) sin(x).*x, 0, pi);
```


