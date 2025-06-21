## Bitwise operators

| Operators | Sign | Language |
| :--- | :--- | :--- |
| AND | & | Python, C, Java |
| OR | \| | Python, C, Java |
| XOR | ^ | Python, C, Java |
| Negation/complement | ~ | Python, C, Java |
| Left shift | << | Python, C, Java |
| Right shift | >> | Python, C, Java |
| Unsigned Right Shift | >>> | Java |

**Masking**
- Making the number unsigned: creates a mask and set all bits to 1, then AND [e.g. `mask = (1 << 32) - 1` in python or directly `0xFFFFFFFFL`]

**Tricks with logical operators**
- XOR: can find out a unique numbre in an array where all other elements appear twice (or even frequency)
- 

## Mathematical functions

(might need some imports)
| Functions | Java | C | Python |
| :--- | :--- | :--- | :--- |
| Absolute | overloaded `Math.abs()` for different numeric types | <stdlib.h> --> `abs(int)`, <math.h> --> `fabs(double)` | `abs(x)` | 
| ceiling |`ceil(double x)` | `ceil(x)` | `ceil(x)`|
| floor |`floor(x)` | `floor(x)`| `floor(x)` | 
| square root |`sqrt(x)` | `sqrt(x)`| `sqrt(x)`| 
| cube root | `cbrt(x)` | `cbrt(x)`| in power function |
| value x raised to power y |`pow(double x, double y)` | `pow(x, y)`| `pow(x, y)` | 
| exponential |`exp(x)` | `exp(x)` | `exp(x)` |
| modulo | `%` | `fmod(x, y)` x / y or `%` | `fmod(x, y)` or `%`|
| logarithm |`log(x)`, `log10(x)`  | `log(x)`, `log10(x)` | `log(x)`, `log10(x)` |
| cosine |`cos(x)` | `cos(x)` | `cos(x)` | 
| sine | `sin(x)` | `sin(x)`| `sin(x)` | 
| tan | `tan(x)` | `tan(x)` | `tan(x)` |
| max | `max(x)` | none |`max(x)` |
| min | `min(x)` | none | `min(x)` |
| greater than macros | none | `isgreater(x, y)` macros | none |
| less than marocs | none | `isless(x, y)` macros | none |
| predefined infinity representation | `Double.POSITIVE_INFINITY`/`Double.NEGATIVE_INFINITY`  or `Integer.MAX_VALUE` | `HUGE_VAL`, `HUGE_VALF`, `HUGE_VALL` macros | `float('inf')`/`float('-inf')`|

## Chacters
| Java | C | Python |
| :--- | :--- | :--- |
| implicit conversion to ascii: `int acsii = 'a';` |  implicit conversion to ascii: `int acsii = 'a';` | `ord(char)` |

Syntactic sugar:
- in C: you can do `int i = 0; s[i] != '\0'; i++` in a for loop for simplicity of accessing a string.

## varargs

| Java | C | Python |
| :--- | :--- | :--- |
| `int...nums` | <stdarg.h>, `int count, ...` | `*args`, `**kwargs` |
| array, must be last param | need <stdarg.h> va_list, va_start, va_arg, va_end | positional args as tuple and kw args as dict

## Dynamic memory allocation in C

| consideration | `malloc()` | `calloc()` |
| :--- | :--- | :--- |
| key difference | does not initialize any memory | initializes the memory with 0 |
| syntax | `malloc(size_t size)` | `calloc(int n, size_t size)` |
| function | allocated contiguous memory on the heap at runtime | same |
| behaviour when allocation failed | returns a NULL pointer | same |
| caveat | should use `free(ptr)` to deallocate memory (release dynamically allocated mem back to the OS) to prevent memory leaks | same |
| other considerations | `realloc()`, dangling pointers, and fragmentation | same |


## Macros in C

Macros are a feature of the preprocessor that can define reusable code snippets or constants. Defined using `#define`
**Use cases**
- Define constants
```c
#define PI 3.14159
#define MAX_SIZE 100
...
float area = PI * radius * radius;
```
- Function-like Macros: expanded inline, which can improve performance may lead to debugging challenges.
```c
#define SQAURE(x) ((x) * (x))
#define MAX(a, b) ((a) > (b) ? (a) : (b))
...
int result = SQUARE(5); // expands to 5 * 5
int maxVal = MAX(10, 20); // expands to the expression
```
- conditional compilation
```c
#ifdef DEBUG
  #define LOG(msg) printf("DEBUG: %s\n", msg)
#else
  #define LOG(msg)
#endif
```
- undefining macros: remove a macro definition by:
```c
#undef PI
```
