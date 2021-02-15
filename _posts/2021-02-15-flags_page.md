---
title: Test Notebook
subtitle: notebooked exported as MD
---

```python
#default_exp flags_page
from nbdev.showdoc import show_doc 
```

# nbdev flags

> list of all flags used in nbdev

nbdev uses special comments, or _flags_, as a markup language that allows you to control various aspects of the documentation, how code is exported to modules, and how code is tested.

## Export flags

Flags for exporting cells to modules.

### #default_exp

Using `#default_exp module_name` specifies that code exported from this notebook will be placed in the destination "*module_name.py*" module.  
Use with dots `.` for submodules and do not include the `.py` extension.

if one specific cell needs to be exported to a different module, just indicate it after #export: `#export special.module`  

* To add something to `__all__` if it's not picked automatically, write an exported cell with something like `#add2all "my_name"`

### #export

Add `#export` for each cell you want to be included in your module and the documentation. When no argument is provided to export, this defaults to the module specified by `#default_exp` as described above. 

a cell marked with `#export` will have its signature added to the documentation.

```python
#export 
class S1():
    def __init__(self, *args, **kwargs):
        pass
```


```python
#export 
class S1():
    def __init__(self, *args, **kwargs):
        pass
```

### #exports

`#exports` just like `#export` but will additionally have the source code added to the documentation.

```python
#exports 
class S2():
    def __init__(self, *args, **kwargs):
        pass
```


```python
#exports 
class S2():
    def __init__(self, *args, **kwargs):
        pass
```

### #exporti

Add `#exporti` for each cell you want exported without it being added to `__all__`, and without it showing up in the docs.

```python
#exporti
class S3():
    def __init__(self, *args, **kwargs):
        pass
```


```python
#exporti
class S3():
    def __init__(self, *args, **kwargs):
        pass
```

## Hide flags

Flags for hiding cells, inputs, or outputs.

### #hide

This flag instructs nbdev to hide the cell when generating the docs.

```python
#hide
print("output")
```


```python
#hide
print("output")
```

    output


### #hide_input

Use `#hide_input` at the top of a cell if you don't want code to be shown in the docs.  
cells containing `#export` or `show_doc` have their code hidden automatically.


```python
#hide_input
print("This is output. Input is hidden using #hide_input")
```

    This is output. Input is hidden using #hide_input


### #hide_output

Use `#hide_output` at the top of a cell if you don't want output to be shown in the docs.  


```python
#hide_output
print("This is input. Output is hidden using #hide_output")
```

    This is input. Output is hidden using #hide_output


## Collapse flags

Flags for having inputs or outputs under a collapsable element. 

### #collapse_input

use `#collapse_input` to include code in the docs under a collapsable element. The collapsable element is closed by default.

Using `#collapse_input open` in a code cell will include your code under a collapsable element that is open by default.


```python
#collapse_input
print("This is output. Input is collapsed using #collapse_input")
```

    This is output. Input is collapsed using #collapse_input


### #collapse_output

use `#collapse_output` to include output in the docs under a collapsable element.


```python
#collapse_output
print("Output is collapsed using #collapse_output")
```

    Output is collapsed using #collapse_output


## Docs flags

### #default_cls_lvl

This defines the default level of classes in the table of contents (TOC).  Use `#default_cls_lvl` followed by a number to se the level (default is 2).


```python
#default_cls_lvl 4
```

above cell changes the level of classes in this notebook to 4. Check TOC at the top of this page.

## Tests flags

Everything that is not an exported cell is considered a test, so you should make sure your notebooks can all run smoothly (and fast) if you want to use this functionality as the CLI. You can mark some cells with special flags (like `#slow`) to make sure they are only executed when you authorize it. Those flags should be configured in your *settings.ini* (separated by a `|` if you have several of them). You can also apply flags to one entire notebook by using the `all` option, e.g. `#all_slow`, in code cells.

If `tst_flags=slow|fastai` in *settings.ini*, you can:

* mark slow tests with `#slow` flag
* mark tests that depend on fastai with the `#fastai` flag.
