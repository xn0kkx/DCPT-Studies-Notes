# Bash Scripting Guide

## Script Initialization

Every Bash script should start with the following shebang line:
```bash
#!/bin/bash
```
This defines the interpreter to be used.

## Comments
Use `#` to add comments in the script.
```bash
# This is a comment
```

## Displaying Text
Use `echo` to print text to the terminal:
```bash
echo "This is a text."
```

## Command Substitution
To display the output of a command inside a string, use `$(command)`:
```bash
echo "Today is $(date)"
```

## Variables

### Declaring Variables
Assign a value to a variable without spaces:
```bash
variable="some text"
```

### Printing Variables
Print a variable using `$`:
```bash
echo "$variable"
```

You can also interpolate variables inside strings:
```bash
echo "This is an example and here is the variable: $variable"
```

### Reading User Input
Use `read` to get input from the user:
```bash
read variable
```

## Conditional Statements

### Comparison Operators
- `-lt` : less than (`<`)
- `-gt` : greater than (`>`)
- `-le` : less than or equal to (`<=`)
- `-ge` : greater than or equal to (`>=`)
- `-eq` : equal to (`==`)
- `-ne` : not equal to (`!=`)

### If-Else Conditions
```bash
if [ "$variable" -eq 10 ]; then
  echo "Variable equals 10"
elif [ "$variable" -gt 10 ]; then
  echo "Variable is greater than 10"
else
  echo "Variable is less than 10"
fi
```

### Case Statements
Separate each case with `;;` and close with `esac`:
```bash
case "$variable" in
  start)
    echo "Starting";;
  stop)
    echo "Stopping";;
  *)
    echo "Invalid option";;
esac
```

## Script Arguments

When you call a script, arguments are passed after the script name:
```bash
./script.sh 192.168.0.20 80
```
- `$0` = script name
- `$1` = first argument
- `$2` = second argument

Example:
```bash
#!/bin/bash
host="$1"
port="$2"
echo "Connecting to $host on port $port"
```

## Loops

### Sequential Loops
```bash
echo {1..10}
seq 1 10
seq 1 100
```

### For Loop
```bash
for ip in {1..10}; do
  echo "192.168.0.$ip"
done
```

### While Loop
```bash
while true; do
  echo "hacked"
done
```

## HTML Parsing Script Example

Extract URLs from an HTML file:
```bash
cat index.html | \
  grep href | \
  cut -d "/" -f3 | \
  grep "\." | \
  cut -d '"' -f1 | \
  grep -v "<l" > lista.txt
```

## Host Lookup from a List

Perform a DNS lookup on each URL:
```bash
for url in $(cat businesscorp_href.txt); do
  host "$url" | grep "has address"
done
```
