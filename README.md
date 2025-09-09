# Bash Cheat Sheet

Essential Bash commands and scripting techniques for shell productivity.

---

## Table of Contents
- [Basic Commands](#basic-commands)
- [File Operations](#file-operations)
- [Text Processing](#text-processing)
- [System Information](#system-information)
- [Process Management](#process-management)
- [Scripting Basics](#scripting-basics)
- [Variables & Arrays](#variables--arrays)
- [Control Structures](#control-structures)
- [Functions](#functions)

---

## Basic Commands

| Command | Description | Example |
|---------|-------------|---------|
| `pwd` | Print working directory | `pwd` |
| `cd <dir>` | Change directory | `cd /home/user` |
| `cd ~` | Go to home directory | `cd ~` |
| `cd -` | Go to previous directory | `cd -` |
| `ls` | List files | `ls -la` |
| `mkdir <dir>` | Create directory | `mkdir my-folder` |
| `mkdir -p <path>` | Create nested directories | `mkdir -p path/to/folder` |
| `rmdir <dir>` | Remove empty directory | `rmdir empty-folder` |
| `which <command>` | Find command location | `which python` |
| `whereis <command>` | Find command and manual | `whereis python` |

## File Operations

| Command | Description | Example |
|---------|-------------|---------|
| `touch <file>` | Create empty file or update timestamp | `touch newfile.txt` |
| `cp <src> <dest>` | Copy file | `cp file1.txt file2.txt` |
| `cp -r <src> <dest>` | Copy directory recursively | `cp -r folder1 folder2` |
| `mv <src> <dest>` | Move/rename file | `mv oldname.txt newname.txt` |
| `rm <file>` | Delete file | `rm file.txt` |
| `rm -rf <dir>` | Delete directory recursively | `rm -rf folder` |
| `ln -s <target> <link>` | Create symbolic link | `ln -s /path/to/file link` |
| `find <path> -name <pattern>` | Find files by name | `find . -name "*.txt"` |
| `find <path> -type f -exec <cmd> {} \;` | Execute command on found files | `find . -name "*.log" -exec rm {} \;` |

## Text Processing

| Command | Description | Example |
|---------|-------------|---------|
| `cat <file>` | Display file content | `cat file.txt` |
| `less <file>` | View file with pagination | `less file.txt` |
| `head -n <num> <file>` | Show first n lines | `head -n 10 file.txt` |
| `tail -n <num> <file>` | Show last n lines | `tail -n 10 file.txt` |
| `tail -f <file>` | Follow file changes | `tail -f /var/log/syslog` |
| `grep <pattern> <file>` | Search text in file | `grep "error" log.txt` |
| `grep -r <pattern> <dir>` | Recursive search | `grep -r "TODO" src/` |
| `sed 's/<old>/<new>/g' <file>` | Replace text | `sed 's/foo/bar/g' file.txt` |
| `awk '{print $1}' <file>` | Extract columns | `awk '{print $1}' data.txt` |
| `sort <file>` | Sort lines | `sort names.txt` |
| `uniq <file>` | Remove duplicates | `sort file.txt \| uniq` |
| `wc -l <file>` | Count lines | `wc -l file.txt` |

## System Information

| Command | Description | Example |
|---------|-------------|---------|
| `whoami` | Current username | `whoami` |
| `id` | User and group IDs | `id` |
| `uname -a` | System information | `uname -a` |
| `df -h` | Disk space usage | `df -h` |
| `du -sh <dir>` | Directory size | `du -sh /home/user` |
| `free -h` | Memory usage | `free -h` |
| `uptime` | System uptime | `uptime` |
| `date` | Current date/time | `date` |
| `cal` | Calendar | `cal` |
| `env` | Environment variables | `env` |
| `history` | Command history | `history` |

## Process Management

| Command | Description | Example |
|---------|-------------|---------|
| `ps aux` | List all processes | `ps aux` |
| `top` | Dynamic process list | `top` |
| `htop` | Enhanced process viewer | `htop` |
| `jobs` | List active jobs | `jobs` |
| `bg` | Put job in background | `bg %1` |
| `fg` | Bring job to foreground | `fg %1` |
| `nohup <command> &` | Run command immune to hangup | `nohup ./script.sh &` |
| `kill <pid>` | Terminate process | `kill 1234` |
| `kill -9 <pid>` | Force kill process | `kill -9 1234` |
| `killall <name>` | Kill processes by name | `killall firefox` |
| `pgrep <name>` | Find process ID by name | `pgrep nginx` |
| `pkill <name>` | Kill processes by name | `pkill nginx` |

## Scripting Basics

### Shebang and Basic Structure
```bash
#!/bin/bash
# This is a comment
echo "Hello, World!"
```

### Exit Codes
```bash
# Check exit code of last command
if [ $? -eq 0 ]; then
    echo "Success"
else
    echo "Failed"
fi

# Exit with specific code
exit 1
```

### Input/Output
```bash
# Read user input
read -p "Enter your name: " name
echo "Hello, $name"

# Redirect output
echo "Hello" > file.txt    # Overwrite
echo "World" >> file.txt   # Append
```

## Variables & Arrays

### Variables
```bash
# Variable assignment (no spaces around =)
name="John"
age=25

# Use variables
echo "My name is $name and I'm $age years old"
echo "My name is ${name} and I'm ${age} years old"

# Command substitution
current_date=$(date)
current_dir=`pwd`

# Environment variables
export PATH=$PATH:/new/path
```

### Arrays
```bash
# Array creation
fruits=("apple" "banana" "orange")
numbers=(1 2 3 4 5)

# Access elements
echo ${fruits[0]}        # First element
echo ${fruits[@]}        # All elements
echo ${#fruits[@]}       # Array length

# Add elements
fruits+=("grape")
```

## Control Structures

### Conditional Statements
```bash
# If statement
if [ $age -gt 18 ]; then
    echo "Adult"
elif [ $age -eq 18 ]; then
    echo "Just became adult"
else
    echo "Minor"
fi

# Case statement
case $1 in
    start)
        echo "Starting service"
        ;;
    stop)
        echo "Stopping service"
        ;;
    *)
        echo "Usage: $0 {start|stop}"
        ;;
esac
```

### Loops
```bash
# For loop
for i in {1..5}; do
    echo "Number: $i"
done

# For loop with array
for fruit in "${fruits[@]}"; do
    echo "Fruit: $fruit"
done

# While loop
counter=1
while [ $counter -le 5 ]; do
    echo "Counter: $counter"
    ((counter++))
done

# Until loop
counter=1
until [ $counter -gt 5 ]; do
    echo "Counter: $counter"
    ((counter++))
done
```

## Functions

```bash
# Function definition
greet() {
    echo "Hello, $1!"
}

# Function with return value
add() {
    local num1=$1
    local num2=$2
    echo $((num1 + num2))
}

# Function usage
greet "World"
result=$(add 5 3)
echo "Result: $result"
```

## Advanced Operations

### File Tests
```bash
if [ -f "file.txt" ]; then echo "File exists"; fi
if [ -d "directory" ]; then echo "Directory exists"; fi
if [ -r "file.txt" ]; then echo "File is readable"; fi
if [ -w "file.txt" ]; then echo "File is writable"; fi
if [ -x "script.sh" ]; then echo "File is executable"; fi
```

### String Operations
```bash
string="Hello World"
echo ${#string}           # String length
echo ${string:0:5}        # Substring (Hello)
echo ${string/World/Bash} # Replace (Hello Bash)
echo ${string,,}          # Lowercase
echo ${string^^}          # Uppercase
```

### Arithmetic
```bash
# Arithmetic expansion
result=$((5 + 3))
result=$((result * 2))

# Using let
let result=5+3
let result*=2

# Using expr
result=`expr 5 + 3`
```

---

## Resources
- [Bash Manual](https://www.gnu.org/software/bash/manual/)
- [Advanced Bash Scripting Guide](https://tldp.org/LDP/abs/html/)
- [ShellCheck](https://www.shellcheck.net/) - Script analysis tool

---
*Originally compiled from various sources. Contributions welcome!*