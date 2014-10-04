Interview Questions with Algorithmic tasks
=========


This chapter will help you to get answers on typical interview questions for **all type of developers**.
This is **Algorithmic questions** that you will hear on your next interview.
Be prepared for this type of questions in advance, because it's not easy questions and you need to understand it, not only read answers.


Questions list
---------

#### Create `sqrt` function

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
