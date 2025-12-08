## Table of Contents
- [Dunder](#Dunder)
- [Mutable vs Immutable](#mutable-vs-immutable)
- [List Comprehensions](#List-Comprehensions)
- [Function Argument & Parameter Types](#function-argument--parameter-types)
- [if _name_ == "__main__"](#if-name--main)
- [Global Interpreter Lock (GIL)](#global-interpreter-lock-gil)
- [Decorators](#Decorators)

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

## Decorators

### Video explanations
- overview: [video](https://www.youtube.com/watch?v=3tyaO-OE0K0)
- specific python decorators: [video](https://www.youtube.com/watch?v=3_P-dxrNCq8)

### Explanation

At its core, a Python decorator is a design pattern that allows you to modify or enhance the behavior of a function or class without permanently changing its source code.

1. The Core Concept: Functions are Objects
To understand decorators, you first need to accept one truth about Python: Functions are first-class objects. This means:

- 🧮You can assign functions to variables.
- 🧮You can pass functions as arguments to other functions.
- 🧮You can define functions inside other functions.

2. The Anatomy of a Decorator
- A decorator is simply a function that takes another function as an input, adds some functionality, and returns a new function.

Syntactic sugar with @ symbol, an example:

```python
import time

def timer_decorator(func):
    # *args and **kwargs let the wrapper accept any arguments the original function needs
    def wrapper(*args, **kwargs):
        start_time = time.time()
        
        # Run the actual function and capture the return value, if any
        result = func(*args, **kwargs)
        
        end_time = time.time()
        print(f"Function '{func.__name__}' took {end_time - start_time:.4f} seconds to run.")
        
        # Return the original function's return value
        return result
    
    return wrapper

@timer_decorator
def heavy_calculation():
    # Simulate a slow process
    time.sleep(1)
    print("Calculation complete!")

@timer_decorator
def heavy_calc_with_params(sleep_time):
    time.sleep(sleep_time)
    print(f"Slept for {sleep_time} seconds.)

heavy_calculation()
heavy_calc_with_params
```

### Best Practice: Using functools.wraps

When you wrap a function, the new function (the wrapper) replaces the original. This means you lose the original function's metadata (like its name and docstring).

To fix this, Python provides a tool called wraps. You should almost always use it when writing decorators.

Example:
```python
from functools import wraps

def my_decorator(func):
    @wraps(func)  # This preserves the metadata of the original 'func'
    def wrapper(*args, **kwargs):
        """This is the wrapper function"""
        return func(*args, **kwargs)
    return wrapper

@my_decorator
def greet():
    """Prints a greeting."""
    print("Hi!")

# Without @wraps, this would print "wrapper". 
# With @wraps, it correctly prints "greet".
print(greet.__name__)
```
### Passing parameters to decorators

To do so, we need to add one more layer of nesting.

Think of this as a Decorator Factory. Instead of the decorator itself, you are writing a function that builds and returns the decorator based on the settings you provide.

Structure: you will need three functions nested inside each other:
- 🏭 The Factory (Outer): Accepts the arguments (e.g., times=3).
- 💟 The Decorator (Middle): Accepts the function to be decorated.
- 🍬 The Wrapper (Inner): Accepts the inputs (*args) for the actual function logic.

### Code Example
Let's build a decorator that repeats a function call a specific number of times.

```python
import functools

# Layer 1: The Factory (accepts your settings)
def repeat(num_times):
    
    # Layer 2: The Actual Decorator (accepts the function)
    def decorator_repeat(func):
        
        @functools.wraps(func)
        # Layer 3: The Wrapper (accepts the function's arguments)
        def wrapper(*args, **kwargs):
            print(f"--- Repeating {num_times} times ---")
            for _ in range(num_times):
                result = func(*args, **kwargs)
            return result
        
        return wrapper
    
    return decorator_repeat

# Usage
@repeat(num_times=3)
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")
```

Output:
```plaintext
--- Repeating 3 times ---
Hello, Alice!
Hello, Alice!
Hello, Alice!
```

### Practical example to restrict role-based access
```python
current_user = {"username": "guest", "role": "viewer"}

# factory that accepts the params
def requires_role(required_role):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            if current_user["role"] != required_role:
                print(f"⛔ ACCESS DENIED: User needs '{required_role}' role.")
                return None
            return func(*args, **kwargs)
        return wrapper
    return decorator

@requires_role("admin")
def delete_database():
    print("Database deleted!")

# Try to run it as a 'viewer'
delete_database()
```
Output:
```plaintext
⛔ ACCESS DENIED: User needs 'admin' role.
```

### Applying decorators to class
Applying decorators to a class works on the same principle as functions, but the "target" is different.

Instead of wrapping a function to modify its logic, a Class Decorator wraps the entire class definition. It receives the class object as input, modifies it (or registers it), and returns it.

This is commonly used for:

- Registration: Automatically adding classes to a list (e.g., registering plugins).
- Enforcing Standards: Adding specific methods or attributes to every class.
- Design Patterns: Implementing patterns like Singleton (ensuring a class only has one instance).

**The Structure**
The syntax looks exactly the same, but you place the @ symbol above the class keyword.

```python
@my_class_decorator
class MyClass:
    pass
```

Equivalent to
```python
class MyClass:
    pass

MyClass = my_class_decorator(MyClass)
```

### Example 1: Adding method to all classes

```python
import datetime

def add_timestamp(cls):
    # Add a new attribute to the class
    cls.creation_time = datetime.datetime.now()
    
    # Add a new method to the class
    def print_info(self):
        print(f"Class: {cls.__name__}, Created at: {cls.creation_time}")
    
    # Attach the method to the class
    cls.print_info = print_info
    
    # Return the modified class
    return cls

@add_timestamp
class User:
    def __init__(self, name):
        self.name = name

@add_timestamp
class Product:
    def __init__(self, price):
        self.price = price

# Usage
u = User("Alice")
u.print_info()  # This method was added by the decorator!

p = Product(100)
p.print_info()
```

### Example 2: adding singleton method

A Singleton is a class that allows only one instance of itself to ever exist. This is useful for things like Database Connections or Configuration Managers.

We can write a decorator that intercepts the creation of a new instance and checks: "Do I already have an instance of this? If yes, return that one. If no, create a new one."

```python
def singleton(cls):
    instances = {} # Dictionary to store the single instance
    
    def wrapper(*args, **kwargs):
        if cls not in instances:
            # If the instance doesn't exist, create it and save it
            instances[cls] = cls(*args, **kwargs)
        # Return the stored instance
        return instances[cls]
    
    return wrapper

@singleton
class DatabaseConnection:
    def __init__(self):
        print("Loading database...")

# First call: Creates the object
db1 = DatabaseConnection() 

# Second call: Returns the EXISTING object (does not print "Loading...")
db2 = DatabaseConnection()

print(f"Are db1 and db2 the exact same object? {db1 is db2}")
```

### Common built-in decorators for python classes

1. `@property`: The "Smart" Attribute
In many languages (like Java), you are taught to write explicit "Getters" and "Setters" (e.g., get_score(), set_score()). This ensures that if you change the internal logic later, you don't break code that uses the class.

In Python, we prefer accessing attributes directly (e.g., `obj.score`), but this risks breaking things if we need to add validation later.

`@property` gives you the best of both worlds: You get the clean syntax of attribute access (`obj.score`), but the backend logic of a function.

The Scenario: A Grade Tracker
We want to ensure a student's score is never below 0 or above 100 -- validation logic.

```python
class Student:
    def __init__(self, name, score):
        self.name = name
        self._score = score  # The underscore suggests "private" use

    @property
    def score(self):
        """This is the 'getter' logic"""
        return self._score

    @score.setter
    def score(self, new_value):
        """This is the 'setter' logic with validation"""
        if 0 <= new_value <= 100:
            self._score = new_value
            print(f"Score updated to {new_value}")
        else:
            print("Error: Score must be between 0 and 100")

# Usage
s = Student("Alice", 85)

# 1. Accessing looks like a variable, but calls the @property method
print(s.score)  # Output: 85

# 2. Assigning looks like a variable, but calls the @score.setter method
s.score = 95    # Output: Score updated to 95
s.score = 200   # Output: Error: Score must be between 0 and 100
```

2. `@dataclass`: The Boilerplate Killer
Introduced in Python 3.7, `@dataclass` is a lifesaver.

When you write a class just to hold data (like a struct), you usually have to write a boring __init__ method, and often a __repr__ method so it prints nicely. `@dataclass` writes these for you automatically.

### Example

Without dataclass:
```python
class InventoryItem:
    def __init__(self, name: str, unit_price: float, quantity_on_hand: int = 0):
        self.name = name
        self.unit_price = unit_price
        self.quantity_on_hand = quantity_on_hand
        
    def __repr__(self):
        return f"InventoryItem(name='{self.name}', unit_price={self.unit_price}, quantity_on_hand={self.quantity_on_hand})"

item = InventoryItem("Widget", 3.50, 10)
print(item)
```

With dataclass:
```python
from dataclasses import dataclass

@dataclass
class InventoryItem:
    name: str
    unit_price: float
    quantity_on_hand: int = 0 

item = InventoryItem("Widget", 3.50, 10)

# Automatic nice printing (__repr__)
print(item) 

# Automatic equality check (__eq__)
item2 = InventoryItem("Widget", 3.50, 10)
print(item == item2) # True (regular classes would return False here!)
```

**Key Features** of `@dataclass`:
- Auto-generated __init__: You just list the variables and types.
- Auto-generated __repr__: It prints a readable string representation immediately.
- Auto-generated __eq__: You can compare two objects with == based on their data, not their memory address.

3. `@classmethod`: The "Alternative Constructor"

To understand `@staticmethod` and `@classmethod`, you have to look at what the method accepts as its first argument.

- Instance Method (Standard): Receives self (the specific object).
- Class Method: Receives cls (the class definition itself).
- Static Method: Receives nothing (neither self nor cls).

A class method is bound to the class, not the object. It cannot modify specific object data (like `self.name`), but it can modify class state or call the class constructor.

Its most common use is as a _Factory_ to create objects in different ways. Especially so when inheritance is present, the derived classes will not break if the parent class has hardcoded any functionality that could be a class method. 

### Scenario: You have a Pizza class. The standard way to make one is by listing ingredients. But you want a shortcut to make a "Margherita" without typing the ingredients every time.

```python
class Pizza:
    def __init__(self, ingredients):
        self.ingredients = ingredients

    def __repr__(self):
        return f"Pizza({self.ingredients})"

    @classmethod
    def margherita(cls):
        # cls is 'Pizza'. This line is the same as calling Pizza(['cheese', 'tomatoes'])
        return cls(['cheese', 'tomatoes'])

    @classmethod
    def prosciutto(cls):
        return cls(['cheese', 'tomatoes', 'ham'])

# 1. Standard way
my_pizza = Pizza(['cheese', 'olives'])

# 2. Factory way (using @classmethod)
lunch = Pizza.margherita() 
dinner = Pizza.prosciutto()

print(lunch)
```
Output:
```plaintext
Pizza(['cheese', 'tomatoes'])
```

4. `@staticmethod`: The "Utility" Function

A static method is just a plain function that happens to live inside a class. It knows nothing about the class or the instance.

You use it when a function logically belongs to a class (for organization), but it doesn't need to access any data inside the class.

### Scenario: You want a utility to check if a pizza size is valid (e.g., only 12, 14, or 16 inches are allowed). This logic doesn't require an existing pizza object to work.

```python
class Pizza:
    def __init__(self, radius, ingredients):
        self.radius = radius
        self.ingredients = ingredients

    @staticmethod
    def circle_area(r):
        # Pure math. Doesn't need 'self' or 'cls'.
        return 3.14 * (r ** 2)

    def area(self):
        # This IS an instance method, because it uses self.radius
        return Pizza.circle_area(self.radius)

# You can call the static method without ever creating a Pizza object
print(Pizza.circle_area(10))  # Output: 314.0
```

Key Distinction: You could put circle_area outside the class as a global function. However, putting it inside Pizza with @staticmethod keeps your code organized. It tells other programmers: "This math is related to Pizzas."

***
### Side-by-side comparison for instance methods, class methods, static methods

```python
class Demo:
    # 1. Instance Method
    def regular_method(self):
        print(f"I know about this specific object: {self}")

    # 2. Class Method
    @classmethod
    def class_method(cls):
        print(f"I know about the class definition: {cls}")

    # 3. Static Method
    @staticmethod
    def static_method():
        print("I know nothing about the object or the class. I'm just a function.")

d = Demo()

d.regular_method() # Passes 'd' implicitly as 'self'
d.class_method()   # Passes 'Demo' implicitly as 'cls'
d.static_method()  # Passes nothing
```
***
