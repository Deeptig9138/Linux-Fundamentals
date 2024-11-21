# Linux Structure

## Overview
Linux, an open-source operating system, has a rich history and a modular architecture that makes it versatile and widely used. From managing hardware resources to providing users with utilities and interfaces, Linux is a cornerstone of modern computing across various domains like cybersecurity, system administration, and software development.

---

## 📜 History
The journey of Linux began with Unix, released in 1970 by Ken Thompson and Dennis Ritchie. 

Key milestones include:
- **1977**: Release of the Berkeley Software Distribution (BSD).
- **1983**: Richard Stallman initiated the GNU Project, creating the GNU General Public License (GPL).
- **1991**: Linus Torvalds developed the first Linux kernel, now with over 23 million source code lines.

Today, Linux powers servers, embedded systems, and even Android devices. With over 600 distributions like Ubuntu, Debian, Fedora, and RedHat, Linux is a secure, stable, and high-performance operating system.

---

## 🌟 Philosophy
Linux adheres to five core principles:
| **Principle**                           | **Description**                                                                                  |
|-----------------------------------------|--------------------------------------------------------------------------------------------------|
| **Everything is a file**                | Configuration files for services are stored as text files.                                       |
| **Small, single-purpose programs**      | Provides modular tools that can be combined for complex tasks.                                   |
| **Ability to chain programs**           | Enables combining tools to perform large, intricate operations.                                  |
| **Avoid captive user interfaces**       | Prioritizes shell-based control over graphical interfaces.                                       |
| **Configuration data stored in text**   | Uses text files (e.g., `/etc/passwd`) for system and application configuration.                  |

---

## 🧩 Components
| **Component**            | **Description**                                                                                  |
|--------------------------|--------------------------------------------------------------------------------------------------|
| **Bootloader**           | Guides the system boot process (e.g., GRUB Bootloader).                                          |
| **OS Kernel**            | Manages hardware resources like CPU, memory, and I/O devices.                                    |
| **Daemons**              | Background services for scheduling, printing, and multimedia.                                    |
| **OS Shell**             | Command-line interface (CLI) for user interaction.                                               |
| **Graphics Server**      | Provides graphical capabilities (e.g., X-server).                                                |
| **Window Manager**       | Graphical user interface (GUI) environments like GNOME, KDE, and Cinnamon.                       |
| **Utilities**            | Programs and applications performing specific tasks.                                             |

---

## 🛠 Linux Architecture
The Linux operating system is composed of several layers:
1. **Hardware**: Physical components like RAM, CPU, and storage.
2. **Kernel**: Core of the OS, managing resources and ensuring process isolation.
3. **Shell**: CLI for users to interact with the OS.
4. **System Utilities**: Tools and applications providing OS functionality.

---

## 📂 File System Hierarchy

![hierarchy](https://tecadmin.net/wp-content/uploads/2022/06/linux-filesystem-hierarchy.png)

Linux follows a tree-like file system hierarchy, defined by the Filesystem Hierarchy Standard (FHS). Key directories include:

| **Path**      | **Description**                                                                                         |
|---------------|---------------------------------------------------------------------------------------------------------|
| `/`           | Root directory containing essential files for booting the system.                                       |
| `/bin`        | Essential command binaries.                                                                             |
| `/boot`       | Static bootloader and kernel files.                                                                     |
| `/dev`        | Device files for hardware access.                                                                       |
| `/etc`        | Local system configuration files.                                                                       |
| `/home`       | User-specific directories for storage.                                                                  |
| `/lib`        | Shared libraries required for system boot.                                                              |
| `/media`      | Mount point for removable media like USB drives.                                                        |
| `/mnt`        | Temporary mount point for filesystems.                                                                  |
| `/opt`        | Optional third-party software and tools.                                                                |
| `/root`       | Home directory for the root user.                                                                       |
| `/sbin`       | System binaries for administration.                                                                     |
| `/tmp`        | Temporary files, cleared on boot.                                                                       |
| `/usr`        | User utilities, libraries, and manuals.                                                                 |
| `/var`        | Variable data like logs, emails, and web application files.                                             |

---

## 🤔 Why Linux?
- **Security**: More resistant to malware than other operating systems.
- **Stability**: Reliable performance with fewer crashes.
- **Open Source**: Modifiable and distributable by anyone.
- **Versatility**: Runs on servers, desktops, embedded systems, and more.

---

## 🔗 Get Started
Explore Linux by practicing its principles, components, and architecture. The interactive exercises in this module will help you apply these concepts practically.
