Interview Questions with Algorithmic tasks
=========


This chapter will help you to get answers on typical interview questions for **all type of developers**.
This is **Algorithmic questions** that you will hear on your next interview.
Be prepared for this type of questions in advance, because it's not easy questions and you need to understand it, not only read answers.

**I've created a [mini book about algorithms](https://github.com/1st/algorithms/) to help you be prepared to the algorithmic questions.**


Questions list
---------

#### How to calculate function complexity?

Read [Complexity function](http://en.wikipedia.org/wiki/Complexity_function) and [Big O notation](http://en.wikipedia.org/wiki/Big_O_notation).


#### Create `sqrt` function

```python
code here
```

#### Find substring positon

```python
# general language-independent implementation
def find_substr(string, substr):
    """Check if string contains substring.

    >>> find_substr('', '')
    True
    >>> find_substr('', 'a')
    False
    >>> find_substr('a', '')
    True
    >>> find_substr('a', 'a')
    True
    >>> find_substr('a', 'aa')
    False
    >>> find_substr('aa', 'a')
    True
    >>> find_substr('abc', 'abc')
    True
    >>> find_substr('abcd', 'abc')
    True
    >>> find_substr('ababc', 'abc')
    True
    >>> find_substr('ababcd', 'abc')
    True
    >>> find_substr('abcabc', 'abcd')
    False
    """
    for i in range(0, len(string) - len(substr) + 1):
        for j in range(0, len(substr)):
            if substr[j] != string[i + j]:
                break
        else:
            return True
    return False
```

```python
# pythonic implementation with string slice
def find_substr(string, substr):
    return any(substr == string[i:i + len(substr)] for i in range(len(string) - len(substr) + 1))
```

#### Create function that return all string permutations

Given string and we need to return all permutations of this string.


```python
def permute_string(original_string):
    """
    >>> permute_string('')
    []
    >>> permute_string('a')
    ['a']
    >>> permute_string('ab')
    ['ab', 'ba']
    >>> permute_string('abc')
    ['abc', 'bac', 'bca', 'acb', 'cab', 'cba']
    """
    results = []
    
    if len(original_string) == 0:
        return results

    ch = original_string[0]
    substrings = permute_string(original_string[1:])

    if not substrings:
        results.append(ch)

    for substring in substrings:
        for index in range(len(substring) + 1):
            tmp_str = substring[0:index] + ch + substring[index:]
            results.append(tmp_str)
        
    return results
```
