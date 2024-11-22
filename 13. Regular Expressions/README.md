# Regular Expressions (RegEx) Guide
Regular expressions (RegEx) are a powerful tool for searching, matching, and manipulating text patterns. They are widely used in various programming languages and utilities like `grep` and `sed`. RegEx allows you to define complex search patterns, validate input, analyze data, and more.

---

## Introduction to RegEx
A **regular expression** is a sequence of characters that defines a search pattern. It can include literal characters as well as special symbols called **metacharacters**, which represent specific matching criteria.

### Common Uses of RegEx:
- Text search and replace
- Input validation
- Data analysis
- Parsing logs or configurations

---

## Grouping in Regular Expressions
Grouping allows you to combine patterns and apply operations to the group as a whole. RegEx supports various grouping operators, each serving a unique purpose.

### Grouping Operators:

| **Operator** | **Description**                                                                |
|--------------|--------------------------------------------------------------------------------|
| `(a)`        | Round brackets group parts of a regex and apply patterns collectively.         |
| `[a-z]`      | Square brackets define character classes, matching any character in the set.   |
| `{1,10}`     | Curly brackets define quantifiers, specifying the number of repetitions.       |
| `|`          | The OR operator, matching one of the two expressions.                          |
| `.*`         | The AND operator, matching only if both expressions are present.               |

---

### Example: Using OR Operator (`|`)
The OR operator matches lines containing either of the specified patterns. 

```
grep -E "(my|false)" /etc/passwd
```

### Output:
```
lxd:x:105:65534::/var/lib/lxd/:/bin/false
pollinate:x:109:1::/var/cache/pollinate:/bin/false
mysql:x:116:120:MySQL Server,,:/nonexistent:/bin/false
```
Here, lines containing either my or false are matched.

### Example: Using AND Operator (.*)
The AND operator matches lines containing both specified patterns in the given order.

```
grep -E "(my.*false)" /etc/passwd
```

### Output:
```
mysql:x:116:120:MySQL Server,,:/nonexistent:/bin/false
```
This command looks for lines containing both my and false in sequence.

Alternatively, you can use grep twice to achieve the same result:
```
grep -E "my" /etc/passwd | grep -E "false"
```

---

## Practice Tasks with /etc/ssh/sshd_config

Show all lines that do not contain the # character:
```
grep -v "#"
```

Search for all lines that contain a word starting with Permit:
```
grep -E "\bPermit\w*"
```

Search for all lines that contain a word ending with Authentication:
```
grep -E "\b\w*Authentication"
```

Search for all lines containing the word Key:
```
grep -E "\bKey\b"
```

Search for all lines beginning with Password and containing yes:
```
grep -E "^Password.*yes"
```

Search for all lines that end with yes:
```
grep -E "yes$"
```

---

## Summary
Regular expressions are a versatile tool for text processing and manipulation. By understanding grouping operators and practicing with real-world examples, you can become proficient in their use. Experiment with the provided tasks to deepen your understanding and efficiency with RegEx.
