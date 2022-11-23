---
sidebar_position: 2
---
# Stack

Stack: last in first out. 

Note stack is more like a way of operation rather than data structure.

## Example
Let's using [this leetcode question](https://leetcode.com/problems/valid-parentheses/) as an example.

### Subproblem - level 1
The question asks us if **all** brackets are either closed or opened correctly:
```python
def solution(s):
    for bracket in s:
        if not check_valid(bracket):
            return False
    return True
```
### Subproblem - level 2: `check_valid(bracket)`
There are two cases for the bracket: if the bracket is an open bracket, then we should check if it got closed properly; otherwise we check if it got opened correctly:
```python
def solution(s):
    open_brackets=['(','[','{']

    for bracket in s:
        if bracket in open_brackets:
            if not check_closed(bracket):
                return False
        else:
            if not check_opened(bracket):
                return False
    
    return True
```

### Subproblem - level 3: `check_closed()` and `check_opened()`
#### `check_closed()`
We need to check whether an open bracket got closed properly, that being said, we need a corresponding closed bracket. So we need something to store all the open brackets and when the **corresponding** closed bracket appears, we delete this open bracket. And if we have nothing left after iterating all the brackets, then all the open brackets are closed properly, otherwise we return False.

Also note the word "corresponding" above, that means a mapping for us:
```python
my_map = {')':'(',']':'[','}':'{'}
open_brackets_stored = []
```
#### `check_opened()`
We need to check whether a closed bracket got opened properly, that being said, there should be a corresponding open bracket before it and no un-paired open bracket should stand betwween them. And that is simply check whether the last element in the `open_brackets_stored` is the corresponding open bracket.

```python
def solution(s):
    open_brackets=['(','[','{']
    my_map = {')':'(',']':'[','}':'{'}
    open_brackets_stored = []

    for bracket in s:
        if bracket in open_brackets:
            open_brackets_stored.append(bracket)
        else:
            if len(open_brackets_stored)==0 or open_brackets_stored[-1] != my_map[bracket]:
                return False
            open_brackets_stored.pop()
    
    return len(open_brackets_stored) == 0
```