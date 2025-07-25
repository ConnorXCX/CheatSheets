# Python Cheat Sheet

_Note: Most examples are sourced from the [official Python docs](https://docs.python.org/3/tutorial/datastructures.html)._

## Contents

#### [Quick Reference](#quick-reference-1)

1. [Quick Reference](#quick-reference-1)

#### [Data Structures](#data-structures-1)

1. [Lists](#lists)
1. [The del Statement](#the-del-statement)
1. [Tuples and Sequences](#tuples-and-sequences)
1. [Sets](#sets)
1. [Dictionaries](#dictionaries)
1. [Lambda Expressions](#lambda-expressions)

## Quick Reference

**List** = `[]`

**Dictionary** = `{key: value}`

**Set** = `set()` if initialized to empty _or_ `{}` with values.

**LIFO** = `.append()`, `.pop()`

**FIFO** = `.append()`, `.popleft()`

## Data Structures

### Lists

```python
fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']

fruits.count('tangerine')
>>> 0
fruits.index('banana')
>>> 3
fruits.index('banana', 4)  # Find next banana starting at position 4
>>> 6

fruits.reverse()
fruits
>>> ['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange']

fruits.append('grape')
fruits
>>> ['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange', 'grape']

fruits.sort()
fruits
>>> ['apple', 'apple', 'banana', 'banana', 'grape', 'kiwi', 'orange', 'pear']

fruits.pop()
>>> 'pear'
```

#### Using Lists as Stacks

```python
stack = [3, 4, 5]

stack.append(6)
stack.append(7)
stack
>>> [3, 4, 5, 6, 7]

stack.pop()
>>> 7
```

#### Using Lists as Queues

```python
from collections import deque

queue = deque(["Eric", "John", "Michael"])

queue.append("Terry")           # Terry arrives
queue.append("Graham")          # Graham arrives
queue.popleft()                 # The first to arrive now leaves
>>> 'Eric'

queue.popleft()                 # The second to arrive now leaves
>>> 'John'
queue                           # Remaining queue in order of arrival
>>> deque(['Michael', 'Terry', 'Graham'])
```

#### List Comprehensions

```python
squares = []

for x in range(10):
    squares.append(x**2)

squares
>>> [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

alternatively with lambda:

```python
squares = list(map(lambda x: x**2, range(10)))
```

or, equivalently:

```python
squares = [x**2 for x in range(10)]
```

---

##### Replacing Nested `for` Loops with List Comprehension Examples

_Note: A list comprehension consists of brackets containing an expression followed by a `for` clause, then zero or more `for` or `if` clauses._

```python
[(x, y) for x in [1,2,3] for y in [3,1,4] if x != y]
>>> [(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]
```

or, equivalently:

```python
combs = []

for x in [1,2,3]:
    for y in [3,1,4]:
        if x != y:
            combs.append((x, y))

combs
>>> [(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]
```

---

##### Other List Comprehension Examples

```python
vec = [-4, -2, 0, 2, 4]

# create a new list with the values doubled
[x*2 for x in vec]
>>> [-8, -4, 0, 4, 8]

# filter the list to exclude negative numbers
[x for x in vec if x >= 0]
>>> [0, 2, 4]

# apply a function to all the elements
[abs(x) for x in vec]
>>> [4, 2, 0, 2, 4]

# call a method on each element
freshfruit = ['  banana', '  loganberry ', 'passion fruit  ']

[weapon.strip() for weapon in freshfruit]
>>> ['banana', 'loganberry', 'passion fruit']

# create a list of 2-tuples like (number, square)
[(x, x**2) for x in range(6)]
>>> [(0, 0), (1, 1), (2, 4), (3, 9), (4, 16), (5, 25)]

# the tuple must be parenthesized, otherwise an error is raised
[x, x**2 for x in range(6)]
>>>   File "<stdin>", line 1
>>>     [x, x**2 for x in range(6)]
>>>      ^^^^^^^
>>> SyntaxError: did you forget parentheses around the comprehension target?

# flatten a list using a listcomp with two 'for'
vec = [[1,2,3], [4,5,6], [7,8,9]]

[num for elem in vec for num in elem]
>>> [1, 2, 3, 4, 5, 6, 7, 8, 9]

# create a list with complex expressions and nested functions
from math import pi

[str(round(pi, i)) for i in range(1, 6)]
>>> ['3.1', '3.14', '3.142', '3.1416', '3.14159']
```

---

##### Nested List Comprehension

Given the following matrix:

```python
matrix = [
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12],
]
```

A list comprehension to transpose matrix:

```python
[[row[i] for row in matrix] for i in range(4)]
>>> [[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```

or, equivalently:

```python
transposed = []

for i in range(4):
    transposed.append([row[i] for row in matrix])

transposed

>>> [[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```

or, equivalently:

```python
transposed = []

for i in range(4):
    # the following 3 lines implement the nested list comprehension
    transposed_row = []
    for row in matrix:
        transposed_row.append(row[i])
    transposed.append(transposed_row)

transposed

>>> [[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```

### The `del` Statement

_Note: This is a way to remove an item from a list given its index instead of its value. This differs from the `pop()` method which returns a value. The `del` statement can also be used to remove slices from a list or clear the entire list._

```python
a = [-1, 1, 66.25, 333, 333, 1234.5]

del a[0]
a
>>> [1, 66.25, 333, 333, 1234.5]

del a[2:4]
a
>>> [1, 66.25, 1234.5]

del a[:]
a
>>> []

del a  # can also be used to delete entire variables:
```

### Tuples and Sequences

_Note: Lists and strings have many common properties, such as indexing and slicing operations. They are two examples of **sequence** data types._

_Note: A tuple consists of a number of values separated by commas._

```python
t = 12345, 54321, 'hello!'
t[0]

>>> 12345
t
>>> (12345, 54321, 'hello!')

# Tuples may be nested:
u = t, (1, 2, 3, 4, 5)
u
>>> ((12345, 54321, 'hello!'), (1, 2, 3, 4, 5))

# Tuples are immutable:
t[0] = 88888
>>> Traceback (most recent call last):
>>>   File "<stdin>", line 1, in <module>
>>> TypeError: 'tuple' object does not support item assignment

# but they can contain mutable objects:
v = ([1, 2, 3], [3, 2, 1])
v
>>> ([1, 2, 3], [3, 2, 1])
```

### Sets

_Note: Curly braces or the `set()` function can be used to create sets._

_Note: To create an **empty set**, you have to use `set()`, not `{}`; the latter creates an empty dictionary, a data structure discussed in the next section._

```python
basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}

print(basket)                      # show that duplicates have been removed
>>> {'orange', 'banana', 'pear', 'apple'}

'orange' in basket                 # fast membership testing
>>> True

'crabgrass' in basket
>>> False

# Demonstrate set operations on unique letters from two words

a = set('abracadabra')
b = set('alacazam')

a                                  # unique letters in a
>>> {'a', 'r', 'b', 'c', 'd'}

a - b                              # letters in a but not in b
>>> {'r', 'd', 'b'}

a | b                              # letters in a or b or both
>>> {'a', 'c', 'r', 'd', 'b', 'm', 'z', 'l'}

a & b                              # letters in both a and b
>>> {'a', 'c'}

a ^ b                              # letters in a or b but not both
>>> {'r', 'd', 'b', 'm', 'z', 'l'}
```

---

#### Set Comprehensions

_Note: Similar to List Comprehensions, Set Comprehensions are also available._

```python
a = {x for x in 'abracadabra' if x not in 'abc'}
a
>>> {'r', 'd'}
```

### Dictionaries

```python
tel = {'jack': 4098, 'sape': 4139}
tel['guido'] = 4127
tel
>>> {'jack': 4098, 'sape': 4139, 'guido': 4127}

tel['jack']
>>> 4098

del tel['sape']
tel['irv'] = 4127
tel
>>> {'jack': 4098, 'guido': 4127, 'irv': 4127}

list(tel)
>>> ['jack', 'guido', 'irv']

sorted(tel)
>>> ['guido', 'irv', 'jack']

'guido' in tel
>>> True

'jack' not in tel
>>> False
```

The `dict()` constructor builds dictionaries directly from sequences of key-value pairs:

```python
dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])
>>> {'sape': 4139, 'guido': 4127, 'jack': 4098}

```

In addition, dict comprehensions can be used to create dictionaries from arbitrary key and value expressions:

```python
{x: x**2 for x in (2, 4, 6)}
>>> {2: 4, 4: 16, 6: 36}
```

When the keys are simple strings, it is sometimes easier to specify pairs using keyword arguments:

```python
dict(sape=4139, guido=4127, jack=4098)
>>> {'sape': 4139, 'guido': 4127, 'jack': 4098}
```

### Looping Techniques

When looping through dictionaries, the key and corresponding value can be retrieved at the same time using the `items()` method.

```python
knights = {'gallahad': 'the pure', 'robin': 'the brave'}

for k, v in knights.items():
    print(k, v)

>>> gallahad the pure
>>> robin the brave
```

When looping through a sequence, the position index and corresponding value can be retrieved at the same time using the `enumerate()` function.

```python
for i, v in enumerate(['tic', 'tac', 'toe']):
    print(i, v)

>>> 0 tic
>>> 1 tac
>>> 2 toe
```

To loop over two or more sequences at the same time, the entries can be paired with the `zip()` function.

```python
questions = ['name', 'quest', 'favorite color']
answers = ['lancelot', 'the holy grail', 'blue']

for q, a in zip(questions, answers):
    print('What is your {0}?  It is {1}.'.format(q, a))

>>> What is your name? It is lancelot.
>>> What is your quest? It is the holy grail.
>>> What is your favorite color? It is blue.
```

To loop over a sequence in reverse, first specify the sequence in a forward direction and then call the `reversed()` function.

```python
for i in reversed(range(1, 10, 2)):
    print(i)

>>> 9
>>> 7
>>> 5
>>> 3
>>> 1
```

To loop over a sequence in sorted order, use the `sorted()` function which returns a new sorted list while leaving the source unaltered.

```python
basket = ['apple', 'orange', 'apple', 'pear', 'orange', 'banana']

for i in sorted(basket):
    print(i)

>>> apple
>>> apple
>>> banana
>>> orange
>>> orange
>>> pear
```

Using `set()` on a sequence eliminates duplicate elements. The use of `sorted()` in combination with `set()` over a sequence is an idiomatic way to loop over unique elements of the sequence in sorted order.

```python
basket = ['apple', 'orange', 'apple', 'pear', 'orange', 'banana']

for f in sorted(set(basket)):
    print(f)

>>> apple
>>> banana
>>> orange
>>> pear
```

It is sometimes tempting to change a list while you are looping over it; however, it is often simpler and safer to create a new list instead.

```python
import math

raw_data = [56.2, float('NaN'), 51.7, 55.3, 52.5, float('NaN'), 47.8]
filtered_data = []

for value in raw_data:
    if not math.isnan(value):
        filtered_data.append(value)

filtered_data
>>> [56.2, 51.7, 55.3, 52.5, 47.8]
```

### Lambda Expressions

_Note: Example sourced from the [official Python docs](https://docs.python.org/3/tutorial/controlflow.html#lambda-expressions)._

Semantically, Lambda expressions are just syntactic sugar for a normal function definition. Like nested function definitions, lambda functions can reference variables from the containing scope:

```python
def make_incrementor(n):
    return lambda x: x + n

f = make_incrementor(42)

f(0)
>>> 42

f(1)
>>> 43
```

The above example uses a lambda expression to return a function. Another use is to pass a small function as an argument:

```python
pairs = [(1, 'one'), (2, 'two'), (3, 'three'), (4, 'four')]
pairs.sort(key=lambda pair: pair[1])
pairs
>>> [(4, 'four'), (1, 'one'), (3, 'three'), (2, 'two')]
```
