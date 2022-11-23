---
sidebar_position: 1
---

# Dictionary
Dictionary, also called mapping. It maps the **key** to the **values**. So, whenever one needs to map something to another thing, consider using dictionary.

## Example 1
Let's using [this leetcode question](https://leetcode.com/problems/roman-to-integer/) as an example.

### Subproblem - level 1
Find the corresponding values for each Roman letters and sum these values together.
```python
def solution(s):
    sum = 0

    for character in s:
        sum += value(character)

    return sum
```

### Subproblem - level 2
Now the problem become how to write the `value()` function. We find out that we either add the value or minus the value for each Roman Letter.
```python
def solution(s):
    sum = 0

    for character in s:
        if(SOME CONDITION):
            sum -= value_2(character)
        else:
            sum += value_2(character)

    return sum
```

### Subproblem - level 3
Now we have two questions: one is what's `SOME CONDITION` above and how to write `value_2(character)`.

#### `SOME CONDITION`

Well, one could hard code the condition has following:
```python
def solution(s):
    sum = 0

    for i in range(len(s)):
        condition = False
        character = s[i]
        if(i != len(s) - 1):
            next_character = s[i+1]
            if character == 'I' and next_character in ['V','X'] or character == 'X' and next_character in ['L','C'] or
            character == 'C' and next_character in ['D','M']:
                condition = True
        if(condition):
            sum -= value_2(character)
        else:
            sum += value_2(character)

    return sum
```
Or, one could find the pattern such that we minus the value from the sum if and only if the value of this character is smaller than the next one:
```python
def solution(s):
    sum = 0

    for i in range(len(s)):
        condition = False
        character = s[i]
        if(i != len(s) - 1):
            next_character = s[i+1]
            if(value_2(character) < value_2(next_character)):
                condition = True
        if(condition):
            sum -= value_2(character)
        else:
            sum += value_2(character)

    return sum
```

#### `value_2(character)`
Now we just need to create a mapping between the Roman letters and integer value:
```python
my_dictionary={'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000}
```
And then we are able to make `value_2(character)` as a getter of dictionary:
```python
value_2(character) = my_dictionary[character]
```
And after solving this problem, all problems are solved and we are done for this question:
```python
def solution(s):
    sum = 0
    my_dictionary={'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000}

    for i in range(len(s)):
        condition = False
        character = s[i]
        if(i != len(s) - 1):
            next_character = s[i+1]
            if(my_dictionary[character] < my_dictionary[next_character]):
                condition = True
        if(condition):
            sum -= my_dictionary[character]
        else:
            sum += my_dictionary[character]

    return sum
```