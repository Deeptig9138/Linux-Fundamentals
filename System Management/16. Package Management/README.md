# Linux Package Management
Package management is a vital aspect of Linux administration. Whether you're maintaining a personal system, managing servers, or working with penetration testing distributions, mastering package managers is crucial for installing, updating, and removing software.  

---

## Key Features of Package Management Systems
- **Package Downloading:** Fetch software packages from repositories.
- **Dependency Resolution:** Automatically resolve and install necessary dependencies.
- **Standard Formats:** Use `.deb`, `.rpm`, or other package formats.
- **Quality Control:** Maintain system stability and integrity during installation or updates.

---

## Popular Package Management Commands

| Command      | Description                                                                                 |
|--------------|---------------------------------------------------------------------------------------------|
| `dpkg`       | Install, build, remove, and manage Debian packages.                                         |
| `apt`        | High-level command-line interface for package management.                                   |
| `aptitude`   | An alternative high-level interface to `apt`.                                               |
| `snap`       | Manage snap packages for secure, isolated applications.                                     |
| `gem`        | Manage Ruby packages using RubyGems.                                                        |
| `pip`        | Python package installer for managing Python packages and dependencies.                     |
| `git`        | Distributed version control system for managing source code and downloading repositories.   |

---

## Example: Using APT Package Manager

### Viewing Repositories
APT uses repositories to manage packages. 
```
username@htb[/htb]$ cat /etc/apt/sources.list.d/parrot.list
# parrot repository
deb http://htb.deb.parrot.sh/parrot/ rolling main contrib non-free
deb http://htb.deb.parrot.sh/parrot/ rolling-security main contrib non-free
```

### Searching for a Package
```
username@htb[/htb]$ apt-cache search impacket
impacket-scripts - Links to useful impacket script examples
python3-impacket - Python3 module to build and dissect network protocols
```

### Viewing Package Details
```
username@htb[/htb]$ apt-cache show impacket-scripts
Package: impacket-scripts
Version: 1.4
Maintainer: Kali Developers <devel@kali.org>
Size: 2080
```

### Installing a Package
```
username@htb[/htb]$ sudo apt install impacket-scripts -y
```

### Listing Installed Packages
```
username@htb[/htb]$ apt list --installed
accountsservice/rolling,now 0.6.55-2 amd64 [installed,automatic]
adduser/rolling,now 3.118 all [installed]
```

---

### Example: Using dpkg for Manual Installation

1) Download the package:
```
wget http://archive.ubuntu.com/ubuntu/pool/main/s/strace/strace_4.21-1ubuntu1_amd64.deb
```

2) Install it using dpkg:
```
sudo dpkg -i strace_4.21-1ubuntu1_amd64.deb
```

3) Verify installation:
```
strace -h
```

---

### Using git to Clone Repositories
Example: Download the Nishang project from GitHub.
```
username@htb[/htb]$ mkdir ~/nishang/ && git clone https://github.com/samratashok/nishang.git ~/nishang
```

---

Practice Tip:
Set up a local virtual machine (VM) to experiment with various package management tools and commands safely.
