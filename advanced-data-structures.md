# Cell Array
An `array` in MATLAB can contain a single type of data, whereas a `Cell Array` can hold multiple data types. 

## Defining a Cell Array
It is done the same way a normal array is done, just instead of `[ ]` use `{ }` for cell arrays.
For example,
```matlab
myCell = { 'Apple',67,[4 5 6]; 'Orange',logical(0),pi};
```
generates a `2x3` cell in workspace.
## Fetching a Cell Array content
### In Cell format
To get a particular cell element in the form of a `1x1` cell, use `cellName(x,y)` where x is the row number and y is the column number of that specific element.
For example,
```matlab
cellOutput = myCell(1,1);
```
gives a `1x1` cell value which in turn contains the element `'Apple'`.

### In the element's own data type
To get a particular cell element in its own data type, use `cellName{x,y}` where x and y are same as above.
For example,
```matlab
cellOutput = myCell{1,1};
```
gives `'Apple'` as value for `cellOutput` in workspace.

**NOTE the difference in brackets used - parenthesis `()` vs curly braces `{}`**

### Display all cell contents
Use the function `celldisp(cellName)`
For example,
```matlab
celldisp(myCell);
```
## Utility Functions

| Function     | Syntax                      | Description                                                                                                  |
| ------------ | --------------------------- | ------------------------------------------------------------------------------------------------------------ |
| `cellfun()`  | `cellfun(function, myCell)` | Applies the `function` to `myCell` and gives suitable output; examples of function - `@isnumeric, @mean` etc |
| `cell2mat()` | `cell2mat(myCell)`          | converts a cell array to standard array; provided current cell contents are all same data type               |

# Structures
In MATLAB, a structure is a data type that stores data in containers called `fields`. Each field can hold any data type and is referenced by the `fieldName` rather than index number.

## Declaring a structure
### Empty Initialization

```matlab
structName = struct;
%here struct is a keyword used to initiate an empty structure

structName.fieldName1 = 'data1';
structName.fieldName2 = 'data2';
```
### One-line initialization
```matlab
structName = struct('fieldName1','data1','fieldName2','data2');
```
**BOTH the methods create the same struct in workspace**
Empty initialization is preferred for larger structures.

## Accessing structure content
### Read a field value
```matlab
structOutput = structName.fieldName1;
```
### Modify a field value
```matlab
structName.fieldName1 = 'newData';
```
### Add a new field
```matlab
structName.fieldName3 = 'data3';
```
## Structure Arrays
In MATLAB, an array of structure can be created to store multiple rows of data for the same structure.
### Initialization
```matlab
structName(2).fieldName1 = 'secondData1';
structName(2).fieldName2 = 'secondData2';
structName(2).fieldName3 = 'secondData3';
```
this adds the second row of data to the same `structName` which now becomes a `1x2` struct.
### Generalised syntax to access/modify struct arrays
```matlab
structName(index).fieldName
```
## Utility Functions

| Function       | Syntax                                          | Description                                                                                        |
| -------------- | ----------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| `fieldnames()` | `fields = fieldnames(structName)`               | Returns all field names as cell array of strings in`Nx1` order, where `N` is the number of fields. |
| `isfield()`    | `check = isfield(structName, 'fieldName')`      | Checks whether `'fieldName'` exists, returns 1 for true, 0 for false                               |
| `rmfield()`    | `structName = rmfield(structName, 'fieldName')` | Removes the `'fieldName'` from the `structName` structure                                          |
