# MATLAB Foundations

## 1. Syntax Basics & Code Structure

### Suppressing Output
Ending any statement with a semicolon (`;`) prevents MATLAB from printing the result directly to the Command Window.
```matlab
a = 5;     % Suppresses output
b = 10     % Displays result in Command Window immediately
```

### Comments & Code Sections
Comments explain code logic and are ignored during execution.

* **Single-line Comment:** Use `%`.
  ```matlab
  % This is a single-line comment
  ```
* **Multi-line Comment:** Use `%{` and `%}`. Ensure both markers are on their own standalone lines.
  ```matlab
  %{
  This is a multi-line comment block.
  It spans across multiple lines.
  %}
  ```
* **Code Blocks / Sections:** Use double percent signs (`%%`). This creates foldable sections that can be executed independently (`Ctrl + Enter`).
  ```matlab
  %% Block 1: Variable Definition
  a = 2;
  b = 3;
  disp(a + b);

  %% Block 2: Additional Calculations
  c = 6;
  d = 7;
  disp(c + d);
  ```

---

## 2. Variables & Data Types

### Variable Initialization
MATLAB does **not** require explicit variable type declarations. Assigning a value creates the variable dynamically.

```matlab
x = 42;             % Defaults to 64-bit double
name = 'MATLAB';    % 16-bit character array
```

### Naming Rules & Conventions
1. Must start with a letter (e.g., `var1`, `my_val`).
2. Can contain letters, numbers, and underscores (`_`).
3. **Case-Sensitive:** `num`, `Num`, and `NUM` are distinct variables.

### Reserved / Built-in Constants
Avoid overwriting built-in constants with custom variable names: 

| Constant      | Description                                                              | Example Output       |
| :------------ | :----------------------------------------------------------------------- | :------------------- |
| `ans`         | Stores the result of the last unassigned expression                      | `2 + 3` => `ans = 5` |
| `pi`          | Mathematical constant $\pi \approx 3.14159$                              | `3.1416`             |
| `i`, `j`      | Imaginary unit $\sqrt{-1}$ (can be used as loop variables if reassigned) | `0.0000 + 1.0000i`   |
| `Inf`, `-Inf` | Positive / Negative Infinity (e.g., division by zero)                    | `1 / 0` => `Inf`     |
| `NaN`         | "Not a Number" (undefined numerical operations)                          | `0 / 0` => `NaN`     |

### Common Data Types

* **64-bit double** (default numerical type for decimal/integer values)
* **16-bit char** (character arrays written in single quotes `'text'`)
* **Vectors & Matrices** (multi-dimensional numerical arrays)
* **Complex numbers** (e.g., `z = (2+1i)*(1+3i)`)
* **Symbolic objects** (used for algebraic manipulation)
* **Integers** (8-bit, 16-bit, 32-bit, 64-bit signed/unsigned)

---

## 3. Vector & Matrix Operations

MATLAB (Matrix Laboratory) treats almost all variables as arrays.

### Creating Vectors & Matrices

```matlab
% Row Vector (elements separated by spaces or commas)
row_vec = [1, 2, 3];

% Column Vector (elements separated by semicolons)
col_vec = [1; 2; 3];

% 2D Matrix
A = [1 2 3; 4 5 6; 7 8 9];
```

### Dimensions & Sizing

* **`size(A)`**: Returns `[rows, columns]` of matrix `A`.
* **`length(v)`**: Returns the maximum dimension length (total length for 1D vectors).

```matlab
A = [1 2 3; 4 5 6];
s = size(A);     % Returns [2, 3]
l = length(A);   % Returns 3
```

### Array Concatenation
Combine existing matrices along rows or columns:

```matlab
a = [1 2];
b = [3 4];

% Horizontal concatenation (column count increases)
c_horiz = [a, b]; % Result: [1 2 3 4]

% Vertical concatenation (row count increases - dimensions MUST match)
c_vert = [a; b];  % Result: [1 2; 3 4]
```

### Implicit Expansion
When performing operations between vectors of non-matching dimensions (like a $1 \times 3$ and a $3 \times 1$), MATLAB automatically expands dimensions:

```matlab
A = [1 2 3];    % 1 x 3
B = [1; 2; 3];  % 3 x 1
E = A + B;      % Expands both to 3 x 3 resulting matrix
```

### Matrix Transposition & Conjugation

* **Transposition with Conjugation (`'`):** Transposes dimensions and negates the imaginary parts of complex numbers.
* **Non-Conjugate Transposition (`.'`):** Transposes dimensions without affecting imaginary parts.
* **Built-in Function:** `transpose(A)`

```matlab
z = [1+2i 3-4i];
z_conj_trans = z'    % Result: [1-2i; 3+4i]
z_trans      = z.'   % Result: [1+2i; 3-4i]

% For purely real numbers, z' and z.' produce identical output.
```

---

## 4. Built-in Mathematical Functions

All mathematical functions operate element-wise when applied to arrays.

| Category              | Function   |
| :-------------------- | :--------- |
| **Exponential & Log** | `exp(x)`   |
|                       | `log(x)`   |
|                       | `log10(x)` |
| **Rounding**          | `round(x)` |
|                       | `floor(x)` |
|                       | `ceil(x)`  |
| **Trigonometry**      | `cos(x)`   |
|                       | `atan(x)`  |
| **Complex Math**      | `abs(z)`   |
|                       | `angle(z)` |

---

## 5. Statistical & Summary Functions

Applied to a 2D matrix `A`, functions like `sum()`, `mean()`, `max()`, and `min()` process data **column-by-column**:

```matlab
A = [1 5; 3 2];

s = sum(A);    % Returns row vector of column sums: [4 7]
m = mean(A);   % Returns column-wise averages: [2 3.5]

% Finding minimum and maximum values with their index locations
[val, idx] = max(A); % val contains max value per column, idx contains row index
[val_min, idx_min] = min(A);

% Sorting arrays
sorted_A = sort(A, 'ascend'); % Sorts each column in ascending order
sorted_A = sort(A, 'descend'); % Sorts each column in descending order
```

---

## 6. Text Handling & Conversion

### Output Display (`disp`)
Displays strings or variable contents in the Command Window without displaying the variable name.

```matlab
disp('Hello World');

% Combining strings with numeric variables using num2str()
val = 42;
disp(['The result is: ', num2str(val)]);
```

---

## 7. Date, Time & System Commands

### Workspace & Directory Utility Commands

```matlab
what        % Displays MATLAB-specific files (.m, .mat) in current folder
who         % Lists all currently defined variables in memory
whos        % Displays detailed list of variables (name, size, bytes, class)
```

### Saving & Loading Workspaces

```matlab
save my_data               % Saves all workspace variables to 'my_data.mat'
save selected_data a b c    % Saves only variables 'a', 'b', and 'c'
clear                       % Removes all variables from active memory
load my_data                % Restores saved variables into memory
```

### Date & Time

```matlab
c = clock;                  % Returns current time vector: [YYYY MM DD hh mm ss]
str = datestr(clock);       % Formats clock vector into readable date/time string
```

### Help System

```matlab
help sin                    % Displays quick documentation in Command Window
doc sin                     % Opens full help manual in separate window
docsearch sin trigonometric % Searches official documentation by keywords
```

---

## 8. Working with M-File Scripts

A script is a text file containing a sequence of MATLAB commands. Scripts are saved with the extension `.m`.

### Creating & Running Scripts
* Create or edit a script directly from the Command Window:
  ```matlab
  edit MatlabDay1
  ```
* **Variable Scope:** All variables created or modified inside a script remain active in the base workspace after execution finishes.
* Execute a script by typing its file name (without `.m`) into the Command Window.

---

## 9. Basic Data Visualization

Plotting data using simple bar charts and adding annotations:

```matlab
% Sample Data
temperatures = [22, 25, 28, 24, 21];

% Generate Bar Chart
figure;
bar(temperatures);

% Add Labels and Formatting
xlabel('Day of Week');
ylabel('Temperature (°C)');
title('Weekly Temperature Variance');
grid on;
```