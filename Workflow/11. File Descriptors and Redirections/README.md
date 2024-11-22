# File Descriptors and Redirections 

## Introduction
A file descriptor (FD) in Unix/Linux operating systems is an indicator of connection maintained by the kernel to perform Input/Output (I/O) operations. In Windows-based operating systems, it is called filehandle. It is the connection (generally to a file) from the Operating system to perform I/O operations (Input/Output of Bytes).  

This guide covers how to manage file descriptors and use redirection to control the flow of data in Linux.

---

## **1. File Descriptors**
### Basics:
- **STDIN (FD 0)**: Input stream for commands or programs.
- **STDOUT (FD 1)**: Output stream for normal results.
- **STDERR (FD 2)**: Output stream for errors.

## **2. STDIN and STDOUT**
### Example:
```
$ cat
SOME INPUT
SOME INPUT
```
Input (SOME INPUT) is provided through STDIN (FD 0).
Output is displayed via STDOUT (FD 1).

## **3. STDOUT and STDERR**
### Example with find:
```
$ find /etc/ -name shadow
```
STDOUT (FD 1): Results of the search.
STDERR (FD 2): Errors, e.g., "Permission denied".

Redirecting STDERR to /dev/null:
```
$ find /etc/ -name shadow 2>/dev/null
```
This command discards all errors by redirecting them to the "null device."

## **4. Redirect STDOUT to a File**
### Example:
```
$ find /etc/ -name shadow 2>/dev/null > results.txt
```
results.txt contains STDOUT (FD 1) output without errors.

## **5. Redirect STDOUT and STDERR to Separate Files**
### Example:
```
$ find /etc/ -name shadow 2> stderr.txt 1> stdout.txt
```
stdout.txt: Contains the standard output.
stderr.txt: Contains the standard errors.

## **6. Redirect STDIN**
### Example:
```
$ cat < stdout.txt
```
Redirects the content of stdout.txt as input for cat.

## **7. Redirect STDOUT and Append to a File**
### Example:
```
$ find /etc/ -name passwd >> stdout.txt 2>/dev/null
```
Appends the output of find to stdout.txt.

## **8. Redirect STDIN Stream to a File**
### Example:
```
$ cat << EOF > stream.txt
This is an example of EOF.
EOF
```
Redirects the input stream (ending with EOF) to stream.txt.

## **9. Pipes**
Pipes (|) are used to pass STDOUT from one program to another.

### Example with grep:
```
$ find /etc/ -name *.conf 2>/dev/null | grep systemd
```
Searches for .conf files and filters results containing systemd.

### Example with wc:
```
$ find /etc/ -name *.conf 2>/dev/null | grep systemd | wc -l
```
Counts the number of lines in the filtered results.

---

## Summary
- Redirection Symbols:
  - **>: Redirect STDOUT to a file (overwrite).**
  - **>>: Append STDOUT to a file.**
  - **<: Redirect file content as STDIN.**
  - **2>: Redirect STDERR to a file or device.**
  - **|: Pipe STDOUT to another command.**

By mastering file descriptors and redirections, you can control the flow of data in Linux efficiently, enabling more effective troubleshooting and data processing.
