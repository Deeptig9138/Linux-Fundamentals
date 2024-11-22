# Filtering and Viewing File Contents
This guide provides examples and usage of various Linux tools to filter and view the contents of files efficiently. It focuses on practical usage with `/etc/passwd` as the example file.

---

## Tools Overview

### `more`
- A pager to view file content interactively.
- Starts from the beginning of the file.

#### Example:
```
more /etc/passwd
```
Quit with [Q]. Output remains in the terminal.

### `less`
- Advanced pager with more features than more.
- Does not leave content in the terminal after exiting.

#### Example:
```
less /etc/passwd
```
Quit with [Q].

### `head`
- Displays the first N lines of a file. Default is 10 lines.

#### Example:
```
head /etc/passwd
```

### `tail`
- Displays the last N lines of a file. Default is 10 lines.

#### Example:
```
tail /etc/passwd
```

### `sort`
- Sorts content alphabetically or numerically.

#### Example:
```
cat /etc/passwd | sort
```

### `grep`
- Searches for patterns in files.
- Use -v to exclude specific patterns.

#### Example:
```
grep "/bin/bash" /etc/passwd
grep -v "nologin\|false" /etc/passwd
```

### `cut`
- Extracts parts of lines based on delimiters.

#### Example:
```
cat /etc/passwd | cut -d":" -f1
```

### `tr`
- Translates or deletes characters.

#### Example:
```
cat /etc/passwd | tr ":" " "
```

### `column`
- Formats data into a table.

#### Example:
```
cat /etc/passwd | tr ":" " " | column -t
```

### `awk`
- A programming tool for text processing. Extracts and manipulates fields.

#### Example:
```
awk '{print $1, $NF}' /etc/passwd
```

### `sed`
- Stream editor for search and replace using regex.

#### Example:
```
sed 's/bin/HTB/g' /etc/passwd
```

### `wc`
- Counts lines, words, or characters.

#### Example:
```
cat /etc/passwd | wc -l
```

---

## Practice Exercises
Use the /etc/passwd file for the following:

1) **Line with username cry0l1t3**:
```
grep "cry0l1t3" /etc/passwd
```

2) **Usernames only**:
```
cut -d":" -f1 /etc/passwd
```

3) **Username cry0l1t3 and UID**:
```
grep "cry0l1t3" /etc/passwd | cut -d":" -f1,3
```

4) **Username cry0l1t3 and UID, separated by a comma**:
```
grep "cry0l1t3" /etc/passwd | awk -F: '{print $1 "," $3}'
```

5) **Username cry0l1t3, UID, and shell, separated by a comma**:
```
grep "cry0l1t3" /etc/passwd | awk -F: '{print $1 "," $3 "," $7}'
```

6) **All usernames with UID and shells, separated by a comma**:
```
awk -F: '{print $1 "," $3 "," $7}' /etc/passwd
```

7) **All usernames with UID and shells, excluding nologin and false**:
```
grep -v "nologin\|false" /etc/passwd | awk -F: '{print $1 "," $3 "," $7}'
```

8) **Exclude nologin and count filtered lines**:
```
grep -v "nologin\|false" /etc/passwd | awk -F: '{print $1 "," $3 "," $7}' | wc -l
```
