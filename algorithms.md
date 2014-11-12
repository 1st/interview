Interview Questions with Algorithmic tasks
=========


This chapter will help you to get answers on typical interview questions for **all type of developers**.
This is **Algorithmic questions** that you will hear on your next interview.
Be prepared for this type of questions in advance, because it's not easy questions and you need to understand it, not only read answers.


Questions list
---------

#### Create `sqrt` function

```python
code here
```

#### Find substring positon

```python
# general language-independent implementation
def find_substr(string, substr):
    for i in range(0, len(string)):
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
    for i in range(0, len(string)):
        if substr == string[i:i + len(substr)]:
            return True
    return False
```

#### Create function that return all string permutations

Given string and we need to return all permutations of this string.


```python
def permute_string(original_string):
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
