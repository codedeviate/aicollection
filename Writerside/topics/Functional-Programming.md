# Functional Programming

## What is Functional Programming?

Functional programming is a programming paradigm that treats computation as the evaluation of mathematical functions and avoids changing state and mutable data. It emphasizes the use of pure functions, immutability, and higher-order functions.

## Key Principles of Functional Programming

1. **Pure Functions**: Functions that always produce the same output for the same input and have no side effects.
2. **Immutability**: Data cannot be changed once created. Instead, new data structures are created with the updated values.
3. **First-Class Functions**: Functions are treated as first-class citizens, meaning they can be assigned to variables, passed as arguments, and returned from other functions.
4. **Higher-Order Functions**: Functions that take other functions as arguments or return them as results.
5. **Function Composition**: Combining simple functions to build more complex ones.

## Example of Functional Programming

Here is a simple example in Python that demonstrates functional programming by calculating the sum of squares of a list of numbers:

```python
# Pure function to square a number
def square(x):
    return x * x

# Pure function to sum two numbers
def add(x, y):
    return x + y

# Higher-order function to apply a function to each element of a list
def map_function(func, lst):
    return [func(x) for x in lst]

# Higher-order function to reduce a list to a single value using a binary function
def reduce_function(func, lst, initial):
    result = initial
    for x in lst:
        result = func(result, x)
    return result

# List of numbers
numbers = [1, 2, 3, 4, 5]

# Calculate the sum of squares
squares = map_function(square, numbers)
sum_of_squares = reduce_function(add, squares, 0)

print(sum_of_squares)  # Output: 55
```

In this example:
- **Pure Functions**: `square` and `add` are pure functions.
- **Higher-Order Functions**: `map_function` and `reduce_function` are higher-order functions.
- **Immutability**: The original list `numbers` is not modified.