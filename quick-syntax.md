# Table of content
- [Bitwise operators](#Bitwise-operators)
- [arrays](#arrays)
- [Mathematical functions](#Mathematical-functions)
- [Utility functions](#Utility-functions)
- [Characters](#Characters)
- [varargs](#varargs)
- [Datetime](#Datetime)
- [Dynamic memory allocation in C](#Dynamic-memory-allocation-in-C)
- [Macros in C](#Macros-in-C)
- [OOP](#OOP)
- [Hashmap in C](#Hashmap-in-C)
- [I/O](#IO)


# Helpful videos/websites
## Python
- syntax: https://youtu.be/PNSIWjWAA7o?si=nacxDxVpamx0kuOr
- dunder methods: https://youtu.be/qqp6QN20CpE?si=aoe-H98YQXU6p9a0
- python OOP: https://youtu.be/rLyYb7BFgQI?si=pUZCxa2yWjYePZf6
- python good habits: https://youtu.be/I72uD8ED73U?si=xUljs0CPcnEGRdvb


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
- n + x = n ^ x: no carry forward, "0 ^ 1" = "0 + 1", thus count number of zeros in n (in binary representation), then 2^zero_bits = the number of possible values x can take

## arrays

| Functionality | Java | C | Python
| :--- | :--- | :--- | :--- |
| **size of array** | `int size = arr.length;`| `int size = sizeof(arr_name) / sizeof(arr_name[0]);` | `size = len(arr)` |
| **size of string** | `int size = str.length;` | `int size = strlen(str);` | `len(str)` |
| **declaration** | `int[] nums;` | `int numbers[5];` or pointer `int* nums;` | `nums = []/[...]` |
| **initialisation** | `int[] nums = new int[5];` or `int[] nums = {1, 2, 3, 4, 5}` | `int numbers[] = {1, 2, 3, 4, 5};` | `nums = []/[...]` |

### Copying
| Language   | Assignment (`arr2 = arr1`)      | Manual Loop                 | Built-in Copy Function(s)                      | Notes                                              |
| ---------- | ------------------------------- | --------------------------- | ---------------------------------------------- | -------------------------------------------------- |
| **Java**   | Copies reference (not contents) | `for` loop                  | `Arrays.copyOf`, `System.arraycopy`            | Arrays are objects; must copy element-wise         |
| **C**      | N/A (arrays decay to pointers)  | `for` loop                  | `memcpy`                                       | Must know element count; no bounds checking        |
| **Python** | Copies reference (not contents) | `for` loop or comprehension | Slicing (`arr1[:]`), `list(arr1)`, `copy.copy` | Shallow vs deep copy matters for nested structures |

#### Codes
##### Java
1. Assignment (arr2 = arr1)
- Behaviour: Both variables refer to the same array object in memory. Any change to one affects the other.
- Result: No new array is created; just another reference to the same object.
- Difference: Fast (just pointer copy) but not a content copy — risky if you want independent arrays.

2. Manual loop

- Behaviour: Iterates over elements and assigns them one by one to a newly created array.
- Result: Creates an independent array with identical contents.
- Difference: Works for any type, easy to understand, but slower for large arrays compared to native methods.

3. System.arraycopy

- Behaviour: Native method that efficiently copies elements from one array to another.
- Result: Independent array (contents copied). Works for partial ranges too.
- Difference: Very fast (uses native memory copy under the hood) but both arrays must have compatible types.

4. Arrays.copyOf

- Behaviour: Creates a new array and copies specified number of elements.
- Result: Independent array; can also change size (padding with default values if larger).
- Difference: Higher-level convenience wrapper, slightly less efficient than System.arraycopy.

```java
// Using a loop
int[] arr1 = {1, 2, 3};
int[] arr2 = new int[arr1.length];
for (int i = 0; i < arr1.length; i++) {
    arr2[i] = arr1[i];
}

// Using Arrays.copyOf
import java.util.Arrays;
int[] arr2 = Arrays.copyOf(arr1, arr1.length);

// Using System.arraycopy
System.arraycopy(arr1, 0, arr2, 0, arr1.length);
```

##### C

1. Assignment
- Behaviour: Not possible for whole arrays directly (e.g., arr2 = arr1; is invalid for arrays). Arrays decay to pointers, so copying requires manual work.
- Result: You cannot duplicate contents without an explicit loop or function call.
- Difference: Only possible if using pointers and allocating memory, but that copies pointers, not contents.

2. Manual loop
- Behaviour: Copies each element individually.
- Result: Independent copy with identical contents.
- Difference: Safe, clear, but slower for large blocks compared to memcpy.

3. memcpy
- Behaviour: Performs a raw memory copy from source to destination.
- Result: Independent copy with identical bytes.
- Difference: Very fast, but dangerous — requires knowing the exact byte size and assumes memory regions don’t overlap. Not type-safe.

```c
#include <stdio.h>
#include <string.h>

int main() {
    int arr1[] = {1, 2, 3};
    int arr2[3];

    // Using a loop
    for (int i = 0; i < 3; i++) {
        arr2[i] = arr1[i];
    }

    // Using memcpy
    memcpy(arr2, arr1, sizeof(arr1));

    return 0;
}
```

##### Python

1. Assignment (arr2 = arr1)
- Behaviour: Both names point to the same list object.
- Result: No new list created; modifying one modifies the other.
- Difference: Simple, fast, but not independent — changes propagate.

2. Manual loop / list comprehension
- Behaviour: Iterates over elements and builds a new list.
- Result: Independent shallow copy of the list.
- Difference: Flexible (can transform elements while copying) but slower than slicing for large lists.

3. Slicing (arr1[:])
- Behaviour: Creates a new list by copying all elements.
- Result: Independent shallow copy.
- Difference: Idiomatic, concise, and efficient for shallow copies.

4. list(arr1)
- Behaviour: Passes the iterable to list() constructor to make a new list.
- Result: Independent shallow copy.
- Difference: Similar to slicing, but works for any iterable.

5. copy.copy and copy.deepcopy
- Behaviour: copy.copy makes a shallow copy (new container, same references for nested objects).
copy.deepcopy recursively copies all nested objects.
- Result: Shallow copy keeps nested references; deep copy makes everything independent.
- Difference: Deep copy is safer for nested mutable structures but slower and uses more memory.

```python
# Using slicing
arr1 = [1, 2, 3]
arr2 = arr1[:]  # shallow copy

# Using list()
arr2 = list(arr1)

# Using copy module
import copy
arr2 = copy.copy(arr1)       # shallow copy
arr2_deep = copy.deepcopy(arr1)  # deep copy if nested
```

### Notes
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
- 2D array declaration in C:
```c
int array[2][3] = {
    {1, 2, 3},
    {4, 5, 6}
};
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

## Utility functions

### Filtering

1. Python: `filter()` construct an iterator (`filter` object) from elements of an iterable for which a function returns true.
    - `filter(function, iterable)`
    -  If the function returns `True` for an element, that element is included in the resulting `filter` object. If the function returns `False`, the element is excluded.
    -  The `filter()` function returns a `filter` object, which is an iterator. This object yields only the elements from the input iterable for which the function returned `True`. To get a usable collection like a list or tuple, you typically convert the filter object using `list()` or `tuple()`.

2. Java: using `stream`
```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class FilterExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
        List<Integer> filtered = numbers.stream()
                                        .filter(n -> n % 2 == 0)
                                        .collect(Collectors.toList());
        System.out.println(filtered);  // Output: [2, 4, 6]
    }
}
```
3. C: manual filtering, use a function to do that

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

## OOP

### Ways to create a struct instance in C
1. Static Allocation
You can declare and initialize a struct instance directly in your code.

```c
#include <stdio.h>

struct Point {
    int x;
    int y;
};

int main() {
    struct Point p1 = {10, 20}; // Static allocation with initialization
    printf("Point: (%d, %d)\n", p1.x, p1.y);
    return 0;
}
```
**Problem**: a stack-allocated object that will go out of scope once the function ends if allocating in the function.

2. Dynamic Allocation
Using malloc (from <stdlib.h>) to allocate memory for a struct dynamically.

```c
#include <stdio.h>
#include <stdlib.h>

struct Point {
    int x;
    int y;
};

int main() {
    struct Point *p2 = (struct Point *)malloc(sizeof(struct Point));
    if (p2 != NULL) {
        p2->x = 30;
        p2->y = 40; // Access members using `->`
        printf("Point: (%d, %d)\n", p2->x, p2->y);
        free(p2); // Free allocated memory
    }
    return 0;
}
```

most directly,
```c
SinglyLinkedListNode* new_curr = malloc(sizeof(SinglyLinkedListNode));
new_curr->data = data;
new_curr->next = llist;
```

Consideration: with `malloc`, comes `free` (if not in use anymore)

3. Using a Function
Create and return a struct instance from a function.

```c
#include <stdio.h>

struct Point {
    int x;
    int y;
};

struct Point createPoint(int x, int y) {
    struct Point p;
    p.x = x;
    p.y = y;
    return p;
}

int main() {
    struct Point p3 = createPoint(50, 60);
    printf("Point: (%d, %d)\n", p3.x, p3.y);
    return 0;
}
```
4. Tricks of struct
```c
SinglyLinkedListNode* mergeLists(SinglyLinkedListNode* head1, SinglyLinkedListNode* head2) {
    // Dummy node to simplify edge cases
    SinglyLinkedListNode dummy;
    SinglyLinkedListNode* tail = &dummy;
    dummy.next = NULL;

    // Traverse both lists
    while (head1 && head2) {
        if (head1->data <= head2->data) {
            tail->next = head1;
            head1 = head1->next;
        } else {
            tail->next = head2;
            head2 = head2->next;
        }
        tail = tail->next;
    }

    // Attach remaining nodes
    if (head1) tail->next = head1;
    if (head2) tail->next = head2;

    return dummy.next;
}
```
## Hashmap in C

### Code:

```c
#include <stdio.h>
#include <stdlib.h>

// define a hash size depending on use case
#define HASH_SIZE 100003

typedef struct Node {
    int value;
    int index;
    struct Node* next;
} Node;

Node* hashTable[HASH_SIZE];

// simple hash function
int hash(int value) {
    return (value % HASH_SIZE + HASH_SIZE) % HASH_SIZE;
}

void insert(int value, int index) {
    int hash_indx = hash(value);
    Node* newNode = malloc(sizeof(Node));
    newNode->value = value;
    newNode->index = index;
    newNode->next = hashTable[hash_indx];
    hashTable[hash_indx] = newNode;
}

// implementation depends on use cases
int find(int value, int curr_idx) {
    int hash_indx = hash(value);
    Node* cur = hashTable[hash_indx];
    while (cur) {
        if (cur->value == value && curr->index != curr_idx) return cur->index;
        cur = cur->next;
    }
    return -1;
}
```
### choosing a good hash table size

1. Problem constraints
- maximum number of elements the system will store - **n**
- Rule of thumb: a hash table big enough that the average chain length stays near 1: `table_size ~= 1.2 * n` [table has ~20% more slots than elements to reduce collisions]

2. Pick a prime number
- because if the table size shares factors with the data distribution (multiples of 10 e.g.), collisions explode
- a prime number helps scatter keys more evenly in the modulo operation
- trial division

3. Consider memory trade-offs
- each slot in the hash table needs a pointer or linked list node --> a tight memory budget might required reduction of the load factor to about ~0.7-0.8 instead of 1.2
- competitive programming: err on the side of slightly bigger tables to keep O(1) lookup time

***summary formula***: `table_size = next_prime_above(ceil(load_factor * n))`

### choosing a good hash function

1. Define "good"
Characteristics:
    1. Distribute keys evenly across buckets (avoid clustering).
    2. Be fast to compute (especially in competitive programming).
    3. Be deterministic (same input → same output).
    4. Minimize collisions for your expected input range.

2. Key's data types and characteristics
- Integers in a small range → direct hashing or modulo is fine.
- Integers in a wide range → need bit mixing or multiplication hashing.
- Strings → need polynomial rolling or FNV-like hash.
- Composite structures → combine field hashes (e.g., XOR, shift-add).

#### VARIOUS HASH FUNCTIONS:

Integers: **simple modulo** (for clean distributions)
- `hash = key % table_size` (table_size is prime and data distribution is not pathological)
- very fast
- --> **data cannot have patterns that align with table size**

Integers: **multiplicative hashing**
```c
unsigned int hash = (unsigned int)key;
hash = (hash * 2654435761u) % table_size; // golden ratio (scramble bits to even out patterend inputs)
```
- 2654435761 is derived from the golden ratio (2^32 / φ).
- Helps scramble bits so even patterned inputs spread out well.
- Often faster than % on some CPUs if table size is power of 2

Integers: **bitwise mixing (for big bits)**
```c
unsigned int hash = (unsigned int)key;
hash ^= hash >> 16;
hash *= 0x7feb352d;
hash ^= hash >> 15;
hash *= 0x846ca68b;
hash ^= hash >> 16;
return hash % table_size;
```
- This is a mixing function (inspired by MurmurHash).
- Great when your keys are large and have high correlation.
- Overkill for small, random-ish data but super safe.

Strings: **polynomial rolling**
```c
unsigned long hash = 0;
unsigned long p = 31; // prime base
unsigned long m = table_size;
for (char *s = str; *s; s++) {
    hash = (hash * p + (*s - 'a' + 1)) % m;
}
```
- Works very well if m is prime.
- Choose base p as a small prime > number of possible characters.

### practical advice for contests when choosing hash functions
- For integer keys and prime table size → simple modulo is usually enough.
- If you see patterns (like all multiples of 10) → use multiplicative hashing with golden ratio.
- Avoid % with non-primes unless you know your input distribution is random.
- In production code, prefer well-tested hashes like FNV-1a, MurmurHash, or CityHash.

### Other more complicated functions

| Hash Function            | Pros                              | Cons                                   | Best For                             |
| ------------------------ | --------------------------------- | -------------------------------------- | ------------------------------------ |
| **Knuth Multiplicative** | Tiny, very fast                   | Slightly weaker for adversarial inputs | Competitive programming integer keys |
| **FNV-1a**               | Simple, portable                  | Slightly weaker avalanche than Murmur  | Small strings, quick prototypes      |
| **MurmurHash3**          | Excellent distribution, very fast | Not cryptographically secure           | Hash tables, bloom filters           |
| **xxHash**               | Extremely fast                    | Larger code footprint                  | Large datasets, real-time processing |
| **SipHash**              | Secure                            | Slower                                 | Web servers, networked apps          |

## I/O

Quick comparison table:
| Feature                 | C (`stdio.h`)                | Java (`Scanner`)                | Python (`input`, `print`) |
| ----------------------- | ---------------------------- | ------------------------------- | ------------------------- |
| Prompt output           | `printf()`                   | `System.out.print()`            | `input(prompt)`           |
| Read int                | `scanf("%d", &x)`            | `sc.nextInt()`                  | `int(input())`            |
| Read string (no spaces) | `scanf("%s", str)`           | `sc.next()`                     | `input()`                 |
| Read line (with spaces) | `fgets(str, size, stdin)`    | `sc.nextLine()`                 | `input()`                 |
| Output newline          | `\n`                         | `println()` or `%n` in `printf` | `print()`                 |
| Output formatting       | Format specifiers `%d %f %s` | Format specifiers `%d %f %s`    | f-strings or `.format()`  |
| Memory safety           | Manual                       | Automatic                       | Automatic                 |

### C
- Uses <stdlib.h>
- format driven
- scanf requires the address of variables (&age) except for arrays (strings).
- %d, %f, %s, etc., are format specifiers.
- Strings with spaces need fgets() or scanf(" %[^\n]s", ...) instead.
- No automatic memory management — buffer sizes matter.
- The %c format specifier in scanf() does not ignore whitespace characters (spaces, tabs or newlines) unlike %d, %f, etc. (which skips newline characters as well) We can use a space before %c in scanf() to solve the problem. This will consume any leading whitespace, including the newline from the previous input.

```c
#include <stdio.h>

int main() {
    int age;
    printf("Enter your age: ");         // Output prompt
    scanf("%d", &age);                  // Read an integer (pass address!)

    char name[50];
    printf("Enter your name: ");
    scanf("%s", name);                  // Read a string (no spaces)

    printf("Hello %s, you are %d years old.\n", name, age);
    return 0;
}
```
### Java
- object oriented: I/O is class-based and often uses Scanner for input and System.out for output.
- Scanner methods: nextInt(), nextDouble(), next(), nextLine().
- You must handle leftover newline characters manually.
- Java strings are objects — no need for manual memory handling.
- Output supports both concatenation (+) and printf-style formatting.
- Output: %n is the platform-independent newline.

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter your age: ");
        int age = sc.nextInt();           // Reads an integer

        sc.nextLine();                    // Consume newline left by nextInt()

        System.out.print("Enter your name: ");
        String name = sc.nextLine();      // Reads full line (can have spaces)

        System.out.println("Hello " + name + ", you are " + age + " years old.");
    }
}
```

Code example on output, zoomed in:
```java
System.out.printf("Pi is approximately %.2f%n", 3.14159); // printf style
System.out.println("Hello World!"); // with newline
System.out.print("Hello ");         // without newline
```

### Python
- high-level, dynamic: is minimalistic and doesn’t require type declarations for input.
- input() always returns a string.
- Casting (int(), float()) is explicit when you want numeric types.
- No need for special newline handling.
- Output supports f-strings, format(), and %-formatting.
- `print` handles type conversion automatically.

```python
age = int(input("Enter your age: "))  # Always returns string; cast to int
name = input("Enter your name: ")     # Reads entire line

print(f"Hello {name}, you are {age} years old.")
```

Python code that zooms in on output:
```python
print("Hello World!")                      # Newline by default
print("Hello", "World", sep=", ", end="!")  # Custom separator & end char
print(f"Pi is approximately {3.14159:.2f}") # f-string formatting
```
