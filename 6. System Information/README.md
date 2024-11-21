# System Information
Understanding the structure and details of a Linux system is fundamental for system administrators, penetration testers, and developers. This guide provides a comprehensive overview of commands used to gather system information, explore processes, configure networks, and much more. These commands are often pre-installed on most Linux systems.

---

## 🔧 Basic Commands

| **Command**  | **Description**                                                     |
|--------------|---------------------------------------------------------------------|
| `whoami`     | Displays the current username.                                      |
| `id`         | Returns user identity and group membership.                         |
| `hostname`   | Sets or prints the hostname of the system.                          |
| `uname`      | Prints basic information about the operating system and hardware.   |
| `pwd`        | Returns the current working directory.                              |

---

## 🌐 Network and Process Commands

| **Command**  | **Description**                                                                |
|--------------|--------------------------------------------------------------------------------|
| `ifconfig`   | Views or assigns a network interface address and configuration.                |
| `ip`         | Shows or manipulates routing, network devices, interfaces, and tunnels.        |
| `netstat`    | Displays network status and statistics.                                        |
| `ss`         | Investigates network sockets.                                                  |
| `ps`         | Displays process status and information.                                       |
| `who`        | Shows users currently logged in.                                               |

---

## 💾 Hardware Commands

| **Command**  | **Description**                               |
|--------------|-----------------------------------------------|
| `lsblk`      | Lists information about block devices.        |
| `lsusb`      | Displays connected USB devices.               |
| `lsof`       | Lists open files.                             |
| `lspci`      | Lists PCI devices connected to the system.    |

---

## 🖥️ Examples

### **Hostname**
Prints the hostname of the system.
```
$ hostname
nixfund
```

### **Whoami**
Displays the current username.
```
$ whoami
cry0l1t3
```

### Id
Provides user ID, group ID, and group memberships.
```
$ id
uid=1000(cry0l1t3) gid=1000(cry0l1t3) groups=1000(cry0l1t3),1337(hackthebox),27(sudo)
```

### Uname
Prints system information. Use uname -a for detailed output.
```
$ uname -a
Linux box 4.15.0-99-generic #100-Ubuntu SMP Wed Apr 22 20:32:56 UTC 2020 x86_64 GNU/Linux
```

To print only the kernel release:
```
$ uname -r
4.15.0-99-generic
```

---

## 🔒 Using SSH for Remote Access
Secure Shell (SSH) allows remote access to a Linux system. It is widely used for managing servers and systems securely.

### **Syntax**
```
$ ssh [username]@[IP address]
```

### **Example**
```
$ ssh admin@192.168.1.100
```

---

## 💡 Additional Tips
Man Pages: Use man <command> to access the manual for a specific command.
```
$ man uname
```

Help Option: Many commands have --help or -h flags to display quick usage information.
```
$ uname --help
```

For detailed command breakdowns, visit Explainshell.

---

## 📚 Conclusion
By mastering these commands, you can gain valuable insights into any Linux system, aiding in system administration, troubleshooting, and security assessments. Take time to study the manual pages (man <command>) for deeper understanding and exploration of advanced options.
