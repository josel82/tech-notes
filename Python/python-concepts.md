## Conditional expressions

```bash
x if coondition else y
```

## Comprehensions

### List comprehension

```bash
squares = [n * n for n in [1, 2, 3]]
# Output: [1, 4, 9]
```

Adding Logic (The "If" Statement)

```bash
numbers = [1, 2, 3, 4, 5, 6]
# Square only the even numbers
even_squares = [n * n for n in numbers if n % 2 == 0]

print(even_squares) # Output: [4, 16, 36]
```

### Dictionary comprehension

```bash
squares = {n: n**2 for n in range(3)}  

print(squares) #{0: 0, 1: 1, 2: 4}
```

### Set comprehension

```bash
myset = {n for n in [1, 2, 2, 3]} 

print(myset) #{1, 2, 3}
```

## Lambda Functions

syntax

$lambda \text{ arguments} : \text{expression}$

```bash
add_ten = lambda x : x + 10

print(add_ten(5)) # Output: 15
```

### Using with `filter()`

`filter()` takes a list and a rule, then keeps only the items that match the rule.

```bash
numbers = [1, 2, 3, 4, 5, 6]
# Keep only even numbers
evens = list(filter(lambda x: x % 2 == 0, numbers))

print(evens) # Output: [2, 4, 6]
```

### Using with `map()`

`map()` applies a function to every item in a list.

Python

```bash
numbers = [1, 2, 3, 4]
# Double every number
doubled = list(map(lambda x: x * 2, numbers))

print(doubled) # Output: [2, 4, 6, 8]
```


# Slicing sintax
source: [https://stackoverflow.com/questions/509211/how-slicing-in-python-works#509295](https://stackoverflow.com/questions/509211/how-slicing-in-python-works#509295)
The syntax is:
```python
a[start:stop]  # items start through stop-1
a[start:]      # items start through the rest of the array
a[:stop]       # items from the beginning through stop-1
a[:]           # a copy of the whole array
```

There is also the `step` value, which can be used with any of the above:
```python
a[start:stop:step] # start through not past stop, by step
```

The key point to remember is that the `:stop` value represents the first value that is _not_ in the selected slice. So, the difference between `stop` and `start` is the number of elements selected (if `step` is 1, the default).

The other feature is that `start` or `stop` may be a _negative_ number, which means it counts from the end of the array instead of the beginning. So:
```python
a[-1]    # last item in the array
a[-2:]   # last two items in the array
a[:-2]   # everything except the last two items
```

Similarly, `step` may be a negative number:
```python
a[::-1]    # all items in the array, reversed
a[1::-1]   # the first two items, reversed
a[:-3:-1]  # the last two items, reversed
a[-3::-1]  # everything except the last two items, reversed
```
Python is kind to the programmer if there are fewer items than you ask for. For example, if you ask for `a[:-2]` and `a` only contains one element, you get an empty list instead of an error. Sometimes you would prefer the error, so you have to be aware that this may happen.

### Relationship with the `slice` object

A [`slice` object](https://www.w3schools.com/python/ref_func_slice.asp) can represent a slicing operation, i.e.:
```python
a[start:stop:step]
```

is equivalent to:
```python
a[slice(start, stop, step)]
```

Slice objects also behave slightly differently depending on the number of arguments, similar to `range()`, i.e. both `slice(stop)` and `slice(start, stop[, step])` are supported. To skip specifying a given argument, one might use `None`, so that e.g. `a[start:]` is equivalent to `a[slice(start, None)]` or `a[::-1]` is equivalent to `a[slice(None, None, -1)]`.

While the `:`-based notation is very helpful for simple slicing, the explicit use of `slice()` objects simplifies the programmatic generation of slicing.