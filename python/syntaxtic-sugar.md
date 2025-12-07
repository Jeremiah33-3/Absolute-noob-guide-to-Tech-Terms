## Table of Contents
- [Dunder](#Dunder)
- [Mutable vs Immutable](#mutable-vs-immutable)
- [List Comprehensions](#List-Comprehensions)
- [Function Argument & Parameter Types]
- [if _name_ == "__main__"]
- [Global Interpreter Lock (GIL)]

***
_powered by gemini_
***

## Dunder 
(double underscore) or Magic methods

### Video Explanation

- [tutorial](https://www.youtube.com/watch?v=qqp6QN20CpE) by Tech With Tim

### Definition
Special methods that start and end with double underscores. Known as magic methods because they allow your objects to behave like Python's _built-in types_ (like integers, lists, or strings). They are the "hooks" that let you customize how your objects interact with standard Python syntax.

### The Core Concept: Operator Overloading
When you use a standard operator (like +) or a built-in function (like len()) on a Python object, Python essentially says, "I will look for a specific dunder method inside this object to handle this action."
- When you write `a + b`, Python calls a.__add__(b).
- When you write `len(a)`, Python calls a.__len__().
- When you write `print(a)`, Python calls a.__str__().

### Common Categories of Dunder Methods
Here are the most important dunder methods you will use in day-to-day programming.

1. Initialization and Representation
These methods control how an object is created and how it looks when printed.

__init__(self, ...): The constructor. It initializes the object's attributes when you create a new instance.

__str__(self): Returns a user-friendly string representation. This is what shows up when you call print(object).

__repr__(self): Returns a "official" string representation, mostly used for debugging by developers.

2. Arithmetic Operators
These allow your custom objects to do math.

__add__(self, other): Handles the + operator.

__sub__(self, other): Handles the - operator.

__mul__(self, other): Handles the * operator.

3. Comparison
These allow you to sort objects or check if they are equal.

__eq__(self, other): Handles equality ==.

__lt__(self, other): Handles "less than" <.

4. Length and Indexing
These allow your object to act like a list or container.

__len__(self): Returns the length when len() is called.

__getitem__(self, index): Allows you to access items using square brackets, like obj[1].

### Quick Reference Table
| Syntax / Function | Dunder Method |
| :--- | :--- |
| obj() | __call__ |
| x + y  | __add__ |
| x - y | __sub__ |
| x == y | __eq__ |
| str(x) or print(x) | __str__ |
| len(x) | __len__ |
| x[index] | __getitem__ |
| for i in x: | __iter__ |

# Important python concepts

Credits: [video tutorial](https://www.youtube.com/watch?v=mMv6OSuitWw)

## Mutable vs Immutable 

This concept dictates how Python handles variables in memory. It answers the question: Can I change the internal state of this object after I create it?

**Immutable (Cannot Change)**: When you "modify" these, Python actually creates a brand new object in memory and points the variable to it.
- Examples: int, float, bool, str, tuple.

**Mutable (Can Change)**: You can modify the object in place. The memory address (ID) remains the same.
- Examples: list, dict, set, bytearray.

**Why it matters**: If you pass a mutable object (like a list) into a function and modify it there, it changes the original list outside the function. If you pass an immutable object (like a number), the function cannot change the original.

### Code example
```python
# Immutable: String
s = "Hello"
s[0] = "J"  # TypeError! You cannot change a character inside a string.
s = "Jello" # This works, but it creates a NEW string object.

# Mutable: List
my_list = [1, 2, 3]
other_list = my_list  # Both point to the same object
other_list.append(4)  
print(my_list) # Output: [1, 2, 3, 4] -> The original changed!
```

## List Comprehensions 

List comprehensions provide a concise, readable way to create lists based on existing lists (or iterables). They are often faster than standard for loops because they are optimized in C.

Syntax: `[expression for item in iterable if condition]`

### Code Example
```python
# The "Old" Way (For Loop)
squares = []
for x in range(10):
    if x % 2 == 0:
        squares.append(x**2)

# The "Pythonic" Way (List Comprehension)
# Reads as: "Give me x squared, for every x in range 10, if x is even."
squares = [x**2 for x in range(10) if x % 2 == 0]
```

## Function Argument & Parameter Types 

Python functions are flexible. It is important to distinguish between Parameters (the variable names defined in the function signature) and Arguments (the actual values passed when calling the function).

- Positional Arguments: Must be passed in the correct order.
- Keyword Arguments: Passed by name (order doesn't matter). (e.g. `epochs=10`)
- Default Parameters: Have a fallback value if no argument is provided.
- `*args` (Variable Positional): Collects extra positional arguments into a tuple.
- `**kwargs` (Variable Keyword): Collects extra keyword arguments into a dictionary.

### Code Example:
```python
def mixed_function(a, b=10, *args, **kwargs):
    print(f"a: {a}, b: {b}")
    print(f"args: {args}")     # Tuple of extra numbers
    print(f"kwargs: {kwargs}") # Dict of extra keywords

# Call:
mixed_function(1, 5, 6, 7, mode="fast", color="blue")

# Output:
# a: 1, b: 5
# args: (6, 7)
# kwargs: {'mode': 'fast', 'color': 'blue'}
```

## if _name_ == "__main__" 

This block is the standard "entry point" guard for Python scripts.
- When you run a file directly: Python sets the special internal variable __name__ to the string "__main__".
- When you import a file as a module: Python sets __name__ to the name of the file (e.g., "my_script").

**Why use it:** It prevents code from executing automatically when you import the file into another script.

### Code example
```python
def do_something():
    print("Function runs")

# Without this check, the print below would run 
# immediately if you imported this file elsewhere.
if __name__ == "__main__":
    print("This only runs if I execute this file directly.")
    do_something()
```

## Global Interpreter Lock (GIL)

The GIL is a _mutex_ (lock) that protects access to Python objects, preventing multiple threads from executing Python bytecodes at once. -> global, only 1 thread executed at a time

**The Key Takeaway**: Even if you run a Python program on a 16-core CPU using multiple threads, only one thread runs at a time.

- CPU-Bound Tasks (Math, Data Processing): The GIL is a bottleneck. Multithreading makes these slower due to context switching overhead. Use multiprocessing instead to bypass the GIL.
- I/O-Bound Tasks (Network requests, File Operations): The GIL is not a problem. While one thread waits for data from the internet, the GIL is released, allowing other threads to run.

| Feature | Threading (Has GIL), | Multiprocessing (No GIL) |
| :--- | :--- | :--- |
| Memory | Shared between threads | Separate (higher overhead) | 
| Best For | I/O (Downloading, API calls) | CPU (Image processing, ML) |
