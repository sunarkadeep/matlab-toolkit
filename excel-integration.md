# Excel in MATLAB
MATLAB provides built-in functions to write and read from Microsoft Excel spreadsheets (`.xls` and `.xlsx`).

## Writing Data
Use the function `xlswrite()`. Syntax is as follows,
```matlab
xlswrite('fileName',randn(10),'sheetName','C6:C15');
```
here,
- `'fileName'` defines the name of the excel file. Not specifying whether its `.xls` or `.xlsx` results in the default `.xls` format.
- `randn(10`) is the content
- `'sheetName'` defines the name of the specific sheet inside of the excel file; if absent in code, then MATLAB writes in the default sheet.
- `'C6:C15'` defines the range where the content is to be written; if absent in code, then MATLAB writes from A1 in the specified sheet.

*Sheet name and Range are Optional*

## Reading Data
Use the function `xlsread()`. Syntax is as follows,
```matlab
[num, txt, raw] = xlsread('fileName.xlsx', 'sheetName', range);
```
here,
- `num` contains only the numeric data 
- `txt` contains only text/strings data
- `raw` contains both numeric and strings data
- specify correctly whether file format of `fileName` is `.xls` or `.xlsx`

*Sheet name and Range are Optional*
