# C I/O
(to be continued)
Firstly, we have scanf():
```c
#include <stdio.h>

int main() {
    char line[100]; 
    while (scanf("%99[^\n]%*c", line) == 1) { // scanf("%[^\n]%*c", input)
        printf("You entered: %s\n", line);
    }
    return 0;
}
```

Secondly, fgets():
```c
#include <stdio.h>

int main() {
    char line[100];
    while (scanf("%99[^\n]%*c", line) == 1) {
        printf("You entered: %s\n", line);
    }
    return 0;
}
```
