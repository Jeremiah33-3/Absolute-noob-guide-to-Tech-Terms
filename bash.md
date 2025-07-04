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
| for loop 'the normal way' | `for ((i = 1; i <= N; i++)); do .. done` |
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

## commands

- `printf` format specifier: `printf format [arguments]`
- e.g.: `printf "My brother %s is %d years old.\n" Peter 21`
  - inputing more arguments than specified --> might create another line with the same string but second argument
  - need check type of the argument as well
  - Note: The difference between echo and printf command is that echo automatically adds a new line character at the end but for printf, you have to explicitly add it.
  - check for list of supported format specifiers symbols
  - precision modifiers supported `%0.5d`
  - can display table:
```bash
#/bin/bash
seperator=--------------------
seperator=$seperator$seperator
rows="%-15s| %.7d| %3d| %c\n"
TableWidth=37

printf "%-15s| %-7s| %.3s| %s\n" Name ID Age Grades
printf "%.${TableWidth}s\n" "$seperator"
printf "$rows" "Sherlock Holmes" 122 23 A
printf "$rows" "James Bond" 7 27 F
printf "$rows" "Hercules Poirot" 6811 59 G
printf "$rows" "Jane Marple" 1234567 71 C
```

## Function Declarations

- `function` keyword is omittable but preferrable
- write function name in the script to call the function
- no args;
```bash
function greet {
    echo "Hello!"
}
```
- passing arguments ($1, $2, ...):
```bash
function say_hello() {
    echo "Hello, $1!"
}

say_hello "Alice"
```
- declaring variables as local for scope
```bash
counter=5

function increment() {
    local counter=0
    ((counter++))
    echo "Inside: $counter"
}

increment
echo "Outside: $counter"
```
- local variables can be assigned values of the arguments:
```bash
function draw_tree() {
    local row=$1
    local col=$2
    local height=$3
    local depth=$$

    # ...
}
```
- Returning values take care
  - method 1: return by exit code:
```bash
function is_even() {
    (( $1 % 2 == 0 )) && return 0 || return 1
}

is_even 4
if [[ $? -eq 0 ]]; then
    echo "Even"
else
    echo "Odd"
fi
```
  - method 2: return using `echo` and return a string:
```bash
function get_date() {
    echo "$(date)"
}

now=$(get_date)
echo "Current date: $now"
```

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
- `$(( ... ))` evaluates the expression inside the double parenthesis as an **integer** arithmetic operation and returns the result.
- `for i in {1..N}` This syntax does not expand N as a variable, use the 'normal way' for loop instead.
