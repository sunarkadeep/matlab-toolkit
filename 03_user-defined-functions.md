## 1. File Naming & Structure Rules

In MATLAB, **the `.m` file name dictates how the function is called** from the Command Window or other scripts—not the internal function name written inside the header.

### Example: `sample_function.m`

```matlab
function [output1, output2] = mainfunction(input1, input2)
    % Primary function block (accessible externally)
    % Commands go here...
    output1 = input1 + input2;
    output2 = another_function(input1);
end

function output3 = another_function(input3)
    % Local helper function (only accessible inside sample_function.m)
    output3 = input3 * 2;
end
```

### Key Takeaways on Scope & Naming

- **External Calls Use the Filename:** You must call `sample_function(input1, input2)`. Calling `mainfunction(input1, input2)` will result in an error because MATLAB ignores the internal header name in favor of the file name. _(Best practice: Always match the primary function name to the `.m` file name)._
    
- **Primary vs. Local Functions:** Only the **first** function in the file (`mainfunction`) can be called from outside. Any subsequent functions (`another_function`) are local and can only be invoked by functions within that same file.
    

## 2. Output Declaration Syntax

To return data back to the caller, output variables must be declared right after the `function` keyword:

- **No Outputs:** `function my_func(in1)`
    
- **Single Output:** Square brackets are optional -> `function out1 = my_func(in1)`
    
- **Multiple Outputs:** Square brackets are required -> `function [out1, out2] = my_func(in1)`
    

## 3. Calling Functions & Handling Outputs

MATLAB assigns returned values using **positional mapping** (based strictly on order, not variable names).

### Standard Multi-Output Call

```matlab
[var1, var2] = sample_function(10, 20);
% output1 is stored in var1
% output2 is stored in var2
```

### Partial Output Capture (Positional Trap)

If you only request one output variable, MATLAB always assigns the **first** output (`output1`), regardless of what you name your variable:

```matlab
[var2] = sample_function(10, 20);
% WARNING: Stores output1 into var2 (output2 is discarded)
```

### Skipping Unwanted Outputs (`~`)

To ignore earlier outputs and capture a specific later output, use the tilde (`~`) placeholder:

```matlab
[~, var2] = sample_function(10, 20);
% output1 is ignored
% output2 is stored in var2
```
### `nargin` command
Returns the number of input arguments passed to a function during a specific call. Datatype is double.
```matlab
function mainfunction(a,b)
	switch nargin
	case 1
		disp('Only one argument passed');
	case 2
		disp('Two arguments passed');
end
```
