# Procedural Programming

## What is Procedural Programming?

Procedural programming is a programming paradigm that uses a linear or top-down approach. It is based on the concept of procedure calls, where procedures (also known as routines, subroutines, or functions) are a set of instructions that perform a specific task.

## Key Principles of Procedural Programming

1. **Modularity**: Code is divided into smaller, manageable sections called procedures or functions.
2. **Sequence**: Instructions are executed in a specific order, typically from top to bottom.
3. **Iteration**: Repeating a set of instructions using loops (e.g., `for`, `while`).
4. **Selection**: Making decisions using conditional statements (e.g., `if`, `switch`).

## Example of Procedural Programming

Here is a simple example in Python that demonstrates procedural programming by calculating the factorial of a number:

```python
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n - 1)

def main():
    number = int(input("Enter a number: "))
    result = factorial(number)
    print(f"The factorial of {number} is {result}")

if __name__ == "__main__":
    main()
```

In this example:
- The `factorial` function is a procedure that calculates the factorial of a number.
- The `main` function handles user input and output.
- The program execution starts from the `main` function, demonstrating the top-down approach.