# Python Interview Refresh

Use this guide to re-ground yourself in Python language fundamentals, runtime characteristics, and coding exercises that often surface in interviews. Also review the dedicated [Django interview refresh](django.md) for framework-specific questions.

## Quick Refresh
- Explain the Global Interpreter Lock (GIL) and how it affects multithreading in CPython.
- Differentiate between Python’s core built-in data structures and when to use each.
- Contrast mutable and immutable types, especially when discussing function arguments and thread safety.
- Describe how Python handles text (`str`) versus binary (`bytes`) data across versions.

## Interview Prompts

### Global Interpreter Lock (GIL)
`GIL` is a mutex that prevents multiple native threads from executing Python bytecode simultaneously. It simplifies memory management but limits CPU-bound parallelism in CPython. Review mitigation strategies such as multiprocessing, asyncio, or alternative runtimes.  
Read: [Global Interpreter Lock](https://wiki.python.org/moin/GlobalInterpreterLock)

### Core Data Types
- Built-in collections: `dict`, `list`, `set`, `frozenset`, `tuple`.
- Python 3 uses `str` for Unicode text and `bytes` for binary data (contrast with Python 2’s `str`/`unicode` split).  
Read: [Python Data Types](https://docs.python.org/3/library/datatypes.html)

### Mutability
- Immutable examples: numbers, strings, tuples.
- Mutable examples: dictionaries, lists, sets.  
Discuss implications for hashing, thread safety, and default arguments.

### Tuple vs List
Tuples are immutable, lists are mutable. Highlight performance differences, memory usage, and typical use cases (e.g., fixed records vs dynamic collections).

### Sets
Sets are unordered collections of unique elements implemented with hash tables—great for membership checks and deduplication.  
Read: [set](https://docs.python.org/2.7/library/stdtypes.html#set)

### Numeric Precision
Floating-point arithmetic introduces rounding errors (e.g., `0.1 + 0.1 + 0.1 - 0.3`). Demonstrate using `Decimal` for precise calculations.  
Read: [decimal](https://docs.python.org/3/library/decimal.html)

## Code Drills

### Mutable Default Arguments
```python
def append_value(val, items=None):
    if items is None:
        items = []
    items.append(val)
    return items
```
Be ready to explain why the defensive `None` check is necessary and show the buggy version that reuses a shared list.

### Quick Testing with Doctest
```python
def my_range(x, y):
    """
    >>> my_range(3, 3)
    []
    >>> my_range(0, 3)
    [0, 1, 2]
    """
    return list(range(x, y))

if __name__ == "__main__":
    import doctest
    doctest.testmod()
```
Use this to illustrate lightweight verification and emphasize when to prefer pytest or unittest for complex scenarios.

### Inspecting Source
```python
import inspect
from django.core import context_processors

print(inspect.getsource(context_processors.request))
```
Shows how to explore library internals during debugging or interview whiteboarding.

## Deep Dive Later
- [Iterators](https://wiki.python.org/moin/Iterator) and [Generators](https://wiki.python.org/moin/Generators) for lazy evaluation discussions.
- [Porting Python 2 Code to Python 3](https://docs.python.org/3/howto/pyporting.html) if legacy migrations surface.
