# Table of content
- [Bitwise operators](#Bitwise-operators)
- [arrays](#arrays)
- [Mathematical functions](#Mathematical-functions)
- [Characters](#Characters)
- [varargs](#varargs)
- [Datetime](#Datetime)
- [Dynamic memory allocation in C](#Dynamic-memory-allocation-in-C)
- [Macros in C](#Macros-in-C)


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
- AND: can check if a number is a power of 2 -- `n & (n - 1) == 0`
- Tricks for finding the largest power of two less than a given number n:
```c
long largest_pow_two(long n) {
    long p = 1;
    while (p << 1 < n) {
        p <<= 1;
    }
    return p;
}
```

## arrays

| Functionality | Java | C | Python
| :--- | :--- | :--- | :--- |
| **size of array** | `int size = arr.length;`| `int size = sizeof(arr_name) / sizeof(arr_name[0]);` | `size = len(arr)` |
| **size of string** | `int size = str.length;` | `int size = strlen(str);` | `len(str)` |

Notes:
- for C, dynamically allocated multi-dimensional arrays require a separate variable to track its size (cannot simply use `sizeof(arr_name)`, as it returns the size of the pointer only **). For not null-terminated arrays, a while loop might be required:
```c
int get_num_rows(char** grid) {
    int count = 0;
    while (grid[count] != NULL) {
        count++;
    }
    return count;
}
```

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

**Notes**:
- for C, the tricky parts in operations can be assigning the numbers to the correct types -- e.g., large integer might require a type of `long` or `long long`

## Characters
| Java | C | Python |
| :--- | :--- | :--- |
| implicit conversion to ascii: `int acsii = 'a';` |  implicit conversion to ascii: `int acsii = 'a';` | `ord(char)` |
| `char c -> c = Character.toLowerCase(c); c - 'a';` | `char c -> c = tolower(c); c - 'a';` | `index = ord(char) - ord('A')` and `index = ord(char) - ord('a')`|
| `Character.isLetter(char c)` | `isalpha(char c)` <ctype.h> | `c.isalpha()` where c is var name holding the char |
| `+`, `str.concat(str2)`or `StringBuilder` class for better performance | `strcat(char* dest, char* source);` from `<string.h>` | `+`, `+=`, `separator.join(arr_of_str)` |

Syntactic sugar:
- in C: you can do `int i = 0; s[i] != '\0'; i++` in a for loop for simplicity of accessing a string.
- tricks for Casear Cipher
```c
char base = isupper(s[i]) ? 'A' : 'a';
s[i] = (s[i] - base + k) % 26 + base
```

## varargs

| Java | C | Python |
| :--- | :--- | :--- |
| `int...nums` | <stdarg.h>, `int count, ...` | `*args`, `**kwargs` |
| array, must be last param | need <stdarg.h> va_list, va_start, va_arg, va_end | positional args as tuple and kw args as dict

## Datetime

### Python 

`datetime` objects designed for parsing and manipulating with dates and times.

- `strftime` method: format datetime objects into readable strings --> formatter reference [here](https://strftime.org/)
```python
from datetime import datetime

now = datetime.now()
formatted_date = now.strftime("%Y-%m-%d %H:%M:%S")
print(formatted_date)
```

### C

C uses the `struct tm` structure from `<time.h>` to represent date and time

E.g.:
```c
#include <stdio.h>
#include <time.h>

int main() {
    time_t now = time(NULL);
    struct tm *local = localtime(&now);

    printf("Date: %04d-%02d-%02d\n", local->tm_year + 1900, local->tm_mon + 1, local->tm_mday);
    printf("Time: %02d:%02d:%02d\n", local->tm_hour, local->tm_min, local->tm_sec);

    return 0;
}
```

### Java

Java has `java.time.LocalDateTime` and `java.time.format.DateTimeFormatter` for working with dates and times. LocalDateTime is immutable and thread-safe. DateTimeFormatter is used for formatting, similar to Python’s strftime.

E.g.
```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class Main {
    public static void main(String[] args) {
        LocalDateTime now = LocalDateTime.now();
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
        String formattedDate = now.format(formatter);

        System.out.println("Current Date and Time: " + formattedDate);
    }
}
```

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
