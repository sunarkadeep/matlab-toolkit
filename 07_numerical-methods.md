# 1. Anonymous Functions
In MATLAB, to define mathematical functions without needing to create separate `.m` file, anonymous function using the `@` operator is used.

Syntax - `f = @(args) expression`

For example,
```matlab
f = @(x,y) cos(x) + sin(y);

z = f(2,1);
% evaluates the function f at x=2, y=1
% after evaluation, z = 0.4253
```
#### Another approach
The function `inline(var)` can also be used to create similar kind of mathematical functions.
For example,
```matlab
f1 = log(x);
f = inline(f1);
```

# 2. Numerical Differentiation
**Forward Difference**  
$$
f'(x) = \frac{ f(x+h) - f(x) }{ h}
$$

**Backward Difference**
$$
f'(x) = \frac{ f(x) - f(x-h)}{h}
$$

**Central Difference**
$$
f'(x) = \frac{ f(x+h) - f(x-h)}{2h}
$$

For example,
```matlab
f = @(x) x.^3;

x = 2; %point of evaluation
h=0.1; %step size

fwd_diff = (f(x+h) - f(x))/h; %forward difference
bwd_diff = (f(x) - f(x-h))/h; %backward difference
ctr_diff = (f(x+h) - f(x-h))/ (2*h); %central difference
```
# 3. Numerical Integration
## Trapezoidal Rule
Given,
- `f = @(x) expression` - integrand
- `a,b` - lower and upper limits 
- `n` - number of segments

For Example,
```matlab
f = @(x) x.^2;
a = 0;
b = 2;
n = 8;

%derived variables
h = (b-a) / n; 
x = a:h:b;
y = f(x);

result = (h/2) * ( y(1) + ( 2 * sum(y(2:end-1)) ) + y(end) );
```
## Simpson's 1/3rd Rule
Given,
- `f = @(x) expression` - integrand
- `a,b` - lower and upper limits 
- `n` - number of segments

For Example,
```matlab
f = @(x) log(x);
a = 4;
b = 5.2;
n = 6;

h = (b-a) / n;

fi = f(a) + f(b); %stores the value of f at the two limits
odd_sum = 0;
even_sum = 0;

for i = 1:2:n-1
	xi = a + (i*h);
	odd_sum = odd_sum + f(xi);
end

for i = 2:2:n-2
	xi = a + (i*h);
	even_sum = even_sum + f(xi);
end

result = (h/3) * ( fi + 4 * odd_sum + 2 * even_sum);
```

# 4. Solving ODEs
MATLAB provides built in functions like `ode23`, `ode45` to solve ordinary differential equations
- `ode23` is used for integration over small intervals
- `ode45` uses methods like *Runge Kutta Method*

For example,
```matlab
dydt = @(t,y) expression 
%here the expression may or maynot contain one of the arguments, i.e t or y

tspan = [ lower_limit , upper_limit ];
%think of t as the independent variable, y as the dependent variable

y0 = constant;
%initial value of y, i.e. at start

[t,y] = ode45( dydt, tspan, y0 );
```
here, `[t,y]` tells MATLAB to store the outputs in two separate columns, thereby making plotting easier later on.

# 5. Root Finding
## Bisection Method
Given,
- `f` - the function
- `a,b` - lower and upper bounds
- `tol` - maximum tolerance allowed
- `max_i` - maximum iterations allowed

In `bisection_method.m` , the following code exists - 
```matlab
function [roots, i] = bisection_method(f, a, b, tol, max_i)
	
	if f(a) * f(b) >= 0
		%display error
		%f(a) and f(b) must have opposite signs
		error(...);
	end
	
	i = 0;
	
	while (b-a)/2 > tol && i < max_i
		c = (a+b)/2;
		
		%checking if mid point is exact root
		if f(c)==0 
			break;
		end 
		
		if f(a) * f(c) < 0
			b = c;
		else
			a = c;
		end
		i = i+1;
	end
	
	root = (a+b)/2;
	
	if i >= max_i
		%display warning
		%maximum iterations reached without full convergence
		warning(...);
	end
end
```

The above function is called as - 
```matlab
%f, a, b, tol, max_i
[roots, i] = bisection_method(f, a, b, tol, max_i);
```

