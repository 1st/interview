Interview Questions for Python developer
=========


This chapter will help you to get answers on typical interview questions for **Python developer** role.


Read this first
---------

- What is [Iterators](https://wiki.python.org/moin/Iterator) and [Generators](https://wiki.python.org/moin/Generators)


Questions list
---------


#### What is `GIL`

`GIL` *(Global Interpreter Lock)* is a mutex that prevents multiple native threads from executing Python bytecodes at once. This lock is necessary mainly because CPython's memory management is not thread-safe.

Read: [Global Interpreter Lock](https://wiki.python.org/moin/GlobalInterpreterLock)

#### What types of data is used in python?

Python provides some built-in data types: `dict`, `list`, `set`, `frozenset` and `tuple`.

In **Python 2.x** we have `str` class that used to hold *binary data and 8-bit text*, and the `unicode` class to handle *Unicode text*.

In **Python 3.x** we have `str` class that used to hold *Unicode strings*, and the `bytes` class is used to hold *binary data*.

Read: [Python Data Types](https://docs.python.org/3/library/datatypes.html)

#### What is `mutable` and `immutable` types?

`Immutable` *(can't be changed in place, only replaced to new value)*: numbers, strings and tuples.

`Mutable`: dictionaries and lists.

#### What difference between `tuple` and `list`

**Tuple** is immutable data type, and **list** is mutable *(see notes below)*.

Example of tuple: `t = (1, 'a', True)` and list: `l = [1, 'a', True]`

#### What is `set`?

`sets` is unordered collections of unique elements. In other words - `set` is a hast table that stored similar to keys in `dict` data type.

Read:
- [sets](https://docs.python.org/2/library/sets.html) basic info *(deprecated in python 2.6)*
- [set](https://docs.python.org/2.7/library/stdtypes.html#set) type


#### Floats VS Decimals

Given a code that produces "strange" result:
```python
>>> 0.1 + 0.1 + 0.1 - 0.3
5.551115123125783e-17
```
Please fix it to produce a "correct" result `0.0`.

**Hint:** read about (Decimals)[https://docs.python.org/3/library/decimal.html] in Python.


Coding examples
---------

#### What happens if you modify default value of named argument in function?

```python
>>> def f(val, l=[]):
>>>     l.append(val)
>>>     print l
>>>
>>> f(10)
[10]
>>> f(20)
[10, 20]
>>> # is it unexpected behavior? :-)

>>> # now try with dict
>>> def f(val, d={}):
>>>     d[val] = val
>>>     print d
>>>
>>> f(10)
{10: 10}
>>> f(20)
{10: 10, 20: 20}
>>> # it's also unexpected behavior!
```

As we can see - if you try to modify default value of mutable variable - this variable will change own default value. So, be careful! *It's potential place for bugs!*

#### Write test for function

The easiest way to test function - is to use [doctest](https://docs.python.org/2/library/doctest.html) that built-in in Python.

```python
def my_range(x, y):
    """
    This function return range from X to Y.
    
    >>> my_range(3, 3)
    []
    >>> my_range(0, 1)
    [0]
    >>> my_range(0, 3)
    [0, 1, 2]
    >>> my_range(1, 7)
    [1, 2, 3, 4, 5, 6]
    """
    return list(range(x, y))

# run our tests
if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

#### How to show source code of given function?

We can show source code of function with `inspect` package.

```python
>>> import inspect
>>> from django.core.context_processors import request
>>> print inspect.getsource(request)
def request(request):
    return {'request': request}
```


Good to know
---------

 - [Porting Python 2 Code to Python 3](https://docs.python.org/3/howto/pyporting.html) - helps you to prepare your Python 2.x code to port on Python 3.x
