# 2D Plotting in MATLAB
## 1. Basic Syntax
In MATLAB, any two vectors of equal length can be plotted using the `plot()` command.
```matlab
x = ...
y = ...

plot(x,y)
```
here, `x` is plotted on the horizontal axis, `y` is plotted on the vertical axis.
Further customisation can be done by adding subsequent arguments within the `plot()` command.
## 2. Adding Labels, Title and Grid
Both the axes of a plot can be labelled as follows,
```matlab
xlabel('This is x label')
ylabel('This is y label')
title('This is the title of plot')
grid on % adds grid to the plot

xlim([m n]); %sets limit on x axis from m to n
ylim([p q]); %sets limit on y axis from p to q
```
## 3. Line colour, width, and Markers
In MATLAB, shorthand strings within the `plot()` command sets the plot line's colour, width and datapoint marker's shape and colour.
- **Plot Colour** : `r` (red), `g` (green), `b` (blue), `k` (black), `m` (magenta)
- **Custom Plot Colour** : syntax  `'color',[r g b]` (the array is RGB vector triplet)
- **Line Styles**  : `-` (solid), `--` (dashed), `:` (dotted), `-.` (dash-dot)
- **Line Width** : syntax `'LineWidth',2` 
- **Markers** : `o` (letter o in lowercase - circle), `*` (asterisk), `s` (square), `.` (dot)
- **Marker Size** : syntax `'MarkerSize',10`
- **Marker Edge Colour** : syntax `'MarkerEdgeColor','k'` (sets edge colour to k i.e. black)
- **Marker Face Colour** : syntax `'MarkerFaceColor','r'` (sets face colour to r i.e. red)

For example,
```matlab
plot(x,y,'s--','LineWidth',2,...
	'color',[1 0 0],...
	'MarkerSize', 10,...
	'MarkerEdgeColor','k',...
	'MarkerFaceColor','r')
```

## 4. Axis commands
The following commands can be used to change the scaling of axes in a plot,
- `axis square` - makes the axes look like a square box
- `axis equal` - makes x and y axes scales the same
- `axis tight` - fits axes to data
```matlab
plot(x,y)
axis equal
```
## 5. Figure command
It is a best practice to begin any plotting with the `figure` command. It guarantees that the following plots open in a new plot window rather than opening on past active window.
## 6. Legend
Used to add a guide / label for multiple datasets plotted in a same plot. By default, it assigns labels in the order of plotting unless explicitly mentioned. 
```matlab
legend('1st degree Curve Fitting','3rd degree Curve Fitting',...
	'Location','northwest')
% assigns the two labels and positions the legend box in the northwest corner of the plot.
```
## 7. Multiple Plots
The `hold on` and `hold off` command is used to plot multiple vectors in one single plot figure, without overwriting the previous one.
For example,
```matlab
y1 = sin(x);
y2 = cos(x);

figure
plot(x, y1, 'b-', 'LineWidth', 2);
hold on;  % Keeps the current plot active
plot(x, y2, 'r--', 'LineWidth', 2);
hold off; % Release the hold
```
## 8. Subplots
To display multiple plots within a window in grid format, `subplot()` is used.
Syntax - `subplot(x,y,z)`

Here,
- `x` is the count of rows
- `y` is the count of columns
- `z` is the active plot index
```matlab
figure
subplot(1,2,1)
% activates the 1st plot of a grid having
% 1 row and 2 columns
plot(......)

subplot(1,2,2)
% activates the 2nd plot of a grid having
% 1 row and 2 columns
plot(......)
```
Each subplot can have its own dataset, labels, titles, axis.
## 9. Logarithmic Plots
MATLAB allows to make either or both axes of a plot to be logarithmic in nature. However for that to work, the vector to be used on the logarithmic axis must be logarithmically spaced as well. 

Thus, `x = logspace(p,q,r)` instead of `x = linspace(p,q,r)`.

Here, `x` has `r` points logarithmically spaced from ${}10^p{}$ to ${}10^q{}$ 

The following commands can be used -

| Command         | Description                                   |
| --------------- | --------------------------------------------- |
| `semilogx(...)` | Logarithmic along x axis, linear along y axis |
| `semilogy(...)` | Logarithmic along y axis, linear along x axis |
| `loglog(...)`   | Logarithmic along both axis                   |

NOTE, arguments to be passed to the above three commands are same as that of `plot()`.
## 10. Visualising a matrix
**`reshape()`**

Used to reshape (or change the order of) an existing matrix to a new order.
```matlab
m = reshape(A,p,q);
% A is the existing matrix
% p x q is the new order, p rows and q columns
```

**`imagesc()`**

Used to display a matrix as a colour-scaled image, mapping the minimum value to the first colour in colourmap and the maximum value to the last colour in colourmap while mapping the rest accordingly.
```matlab
imagesc(m);
% m is the given matrix
```

**`colorbar`**

Used to display a vertical colour bar to the right of current axes or plot.
*Note - it is colorbar, not colourbar, no U present*

**`colormap()`**

Used to set the colourmap of the current figure. Usual arguments are as follows - 
```matlab
colormap(gray)
colormap(cool)
colormap(hot)
```
[More info on colormap](https://in.mathworks.com/help/matlab/ref/colormap.html)

**Parula** is the default colormap introduced in version R2014b.
## 11. Specialised Plotting Functions

| Command      | Description                                           |
| ------------ | ----------------------------------------------------- |
| `bar()`      | For bar graphs                                        |
| `stairs()`   | For piecewise constant functions                      |
| `polar()`    | For polar plot                                        |
| `meshgrid()` | To create 2D coordinate matrices for grid based plots |
| `quiver()`   | For plotting 2D velocity or direction vectors on grid |

### Fill
The `fill()` command is used to plot filled 2D polygons from vertex coordinate vectors.
```matlab
fill([0 1 0.5], [0 0 1], 'r', 'FaceAlpha', 0.5)
% creates polygons joining the points
% (0,0), (1,0), and (0.5,1)
```
`FaceAlpha` is used to set the transparency, and varies from 0 (transparent) to 1 (opaque).

# 3D Plotting in MATLAB
## 1. Line Plot
The `plot3()` command is used to plot line plots in three dimensions.
```matlab
x = ...
y = ...
z = ...

plot3(x,y,z,...)
```
## 2. Surface Plots
The `surf()` command creates 3D coloured surface plots with solid face over a grid. It puts vertices at specified points in space x,y,z and connects all the vertices to make a surface.
```matlab
[X, Y] = meshgrid(-2:0.1:2, -2:0.1:2);
Z = X.^2 + Y.^2; % defining the vertical Z

figure
surf(X, Y, Z);
shading interp
```
Options for shading in `surf()`
- `shading faceted` - default, shows black mesh lines, assigns a single colour to each grid cell
- `shading flat` - removes grid lines, assigns a single colour to each grid cell
- `shading interp` - removes grid lines, smoothly interpolates colour across faces and edges, gives a continuous look
