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
