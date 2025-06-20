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

## Mathematical functions

| Functions | Java | C | Python |
| :--- | :--- | :--- | :--- |
| Absolute | overloaded `Math.abs()` for different numeric types | <stdlid.h> --> `abs(int)`, <math.h> --> `fabs(double)` | abs() | 

## Dynamic memory allocation in C

| consideration | `malloc()` | `calloc()` |
| :--- | :--- | :--- |
| key difference | does not initialize any memory | initializes the memory with 0 |
| syntax | `malloc(size_t size)` | `calloc(int n, size_t size)` |
| function | allocated contiguous memory on the heap at runtime | same |
| behaviour when allocation failed | returns a NULL pointer | same |
| caveat | should use `free(ptr)` to deallocate memory (release dynamically allocated mem back to the OS) to prevent memory leaks | same |
| other considerations | `realloc()`, dangling pointers, and fragmentation | same |
