# Introduction to BASH [scripts]

> Bash (Bourne Again Shell) is not an operating system like Linux, but rather a command-line interpreter or shell that is commonly used in Unix-like operating systems (GNU/Linux), including Linux. It was developed as a free software replacement for the Bourne shell (sh) and has since become the default shell on many Linux distributions.
- It is used as a default login shell for most Linux distributions.
- Scripting is used to automate the execution of the tasks so that humans do not need to perform them individually. Bash scripting is a great way to automate different types of tasks in a system.
- Shebang: In Unix-based systems like Linux, macOS, and BSD, the shebang is commonly used as the first line in script files to specify the interpreter that executes the commands present in the file.

## Various Shebang

(from [source](https://stackoverflow.com/questions/13872048/bash-script-what-does-bin-bash-mean))
| script | function |
| --- | --- |
| #!/bin/sh | Execute the file using sh, the Bourne shell, or a compatible shell |
| #!/bin/csh | Execute the file using csh, the C shell, or a compatible shell |
| #!/usr/bin/perl -T | Execute using Perl with the option for taint checks |
| #!/usr/bin/php | Execute the file using the PHP command line interpreter |
| #!/usr/bin/python -O | Execute using Python with optimizations to code |
| #!/usr/bin/ruby | Execute using Ruby |

## Syntax

--> GitHub table: [docs](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/organizing-information-with-tables)
| Use case | Syntax |
| :---: | :---: |
| for loop (list) | `for item in list_name do ... done` |
| for loop (range) | `for i in {0..99} do ... done` |
| input | `read var_name` |
| read multiple inputs (separate by space) | `read var_name1 var_name2` |
| read multiple inputs (separate by space) | `read var_name1 \n read var_name2` |
| use flags for input prompt | `read -p "Enter your age: " age` |
| reading from a file | `while IFS= read -r line; do \n echo "$line" \n done < file.txt` |
| read a single character | `read -n1 input` |
| output | `echo "hello"` or `printf` |
| output overwrite to a file | `echo "sth" > filename.txt` |
| output append to a file | `echo "sth" >> filename.txt` |
| Piping | `echo "Hello World" \| tr 'a-z' 'A-Z'` |
| Arithmetic expansions | `product=$((num1 * num2))` |
| Arithmetic expressions | `product=$(expr $num1 \* $num2)` |
| greater than/ equal to/ lesser than | `if [ "$num1" -gt/-eq/-lt $num2" ]; then ..` (must include space between [])|
| evaluate expressions | `expr {expression}` |
| if else | ```if [ condition ]; then .. elif [ another_condition ]; then .. else .. fi``` |
| regex | `[[ ..=~.. ]]` |

## Arithmetic core

### `bc`
`bc` is an external command-line calculator that expects input via standard output (`echo "expression" | bc`) or a file (`bc < file`).
Syntax:
```bash
result=$(echo "scale=2; $a / $b" | bc)
```
OR using here-string
```bash
result=$(bc <<< "scale=2; $a / $b")
```
- An example:
```bash
#!/bin/bash

read -p "Enter expression: " expr

# Replace ^ with ** since bc uses ^ for bitwise XOR, not power
expr="${expr//^/**}"

# Evaluate the expression using bc with scale set to high precision
result=$(echo "scale=10; $expr" | bc -l)

# Round to 3 decimal places using printf
printf "%.3f\n" "$result"
```

## notes

- for comparing multiple conditions (uses && and ||):
```bash
if [ "$X" -eq "$Y" ] && [ "$Y" -eq "$Z" ]; then
...
```
- note: `$(( ... ))` evaluates the expression inside the double parenthesis as an **integer** arithmetic operation and returns the result.
