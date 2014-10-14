Interview Questions for Python developer
=========


This chapter will help you to get answers on typical interview questions for **Python developers**.


Questions list
---------


#### What is `GIL`

`GIL` *(Global Interpreter Lock)* is a mutex that prevents multiple native threads from executing Python bytecodes at once. This lock is necessary mainly because CPython's memory management is not thread-safe.

- [Global Interpreter Lock](https://wiki.python.org/moin/GlobalInterpreterLock)

#### What types of data is used in python?

Python provides some built-in data types: `dict`, `list`, `set`, `frozenset` and `tuple`.

In **Python 2.x** we have `str` class that used to hold *binary data and 8-bit text*, and the `unicode` class to handle *Unicode text*.

In **Python 3.x** we have `str` class that used to hold *Unicode strings*, and the `bytes` class is used to hold *binary data*.

- [Python Data Types](https://docs.python.org/3/library/datatypes.html)

#### What is `mutable` and `immutable` types?

`Immutable` *(can't be changed in place, only replaced to new value)*: numbers, strings and tuples.

`Mutable`: dictionaries and lists.

#### What difference between `tuple` and `list`

**Tuple** is immutable data type, and **list** is mutable *(see notes below)*.

Example of tuple: `t = (1, 'a', True)` and list: `l = [1, 'a', True]`

#### What is `set`?

`sets` is unordered collections of unique elements.

- [sets](https://docs.python.org/2/library/sets.html) basic info *(deprecated in python 2.6)*
- [set](https://docs.python.org/2.7/library/stdtypes.html#set) type

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

### Good to know

 - [Porting Python 2 Code to Python 3](https://docs.python.org/3/howto/pyporting.html) - helps you to prepare your Python 2.x code to port on Python 3.x
