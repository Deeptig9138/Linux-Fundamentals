# Network Services

## Overview
This project explores network services in Linux, providing knowledge critical for various purposes such as:
- Communication with other computers over the network.
- File transfer and network traffic analysis.
- Configuring services to identify vulnerabilities during penetration tests.
- Enhancing understanding of network security.

Key topics covered include SSH, NFS, web servers, and VPNs. Each section provides installation instructions, configurations, and use cases, both from an administrator's and penetration tester's perspectives.

---

## Table of Contents
1. [Secure Shell (SSH)](#secure-shell-ssh)
2. [Network File System (NFS)](#network-file-system-nfs)
3. [Web Server](#web-server)
4. [Virtual Private Network (VPN)](#virtual-private-network-vpn)

---

## Secure Shell (SSH)

### Description
SSH is a protocol for securely managing and accessing remote systems. The most common SSH server, OpenSSH, ensures encrypted communication and is widely used for executing commands, transferring files, and remote system management.

### Installation
```bash
sudo apt install openssh-server -y
```
Check Server Status
bash
Copy code
systemctl status ssh
Example Usage
Connect to a remote host:

bash
Copy code
ssh username@remote_host
Configuration
Edit /etc/ssh/sshd_config to customize settings like:

Maximum concurrent connections.
Login methods (passwords or keys).
Network File System (NFS)
Description
NFS allows sharing files across networks, appearing as local to the user. It supports real-time file transfer, efficient collaboration, and privilege management.

Installation
bash
Copy code
sudo apt install nfs-kernel-server -y
Check Server Status
bash
Copy code
systemctl status nfs-kernel-server
Configuration
Edit /etc/exports to specify shared directories and permissions:

rw: Read and write access.
sync: Ensures data consistency.
Example Usage
Share a directory:

bash
Copy code
mkdir ~/nfs_sharing
echo '/home/user/nfs_sharing hostname(rw,sync,no_root_squash)' | sudo tee -a /etc/exports
Mount an NFS share:

bash
Copy code
mkdir ~/target_nfs
sudo mount remote_host:/path_to_share ~/target_nfs
Web Server
Description
Web servers like Apache and Python's HTTP server are essential for hosting web applications, transferring files, and analyzing traffic.

Apache Installation
bash
Copy code
sudo apt install apache2 -y
Apache Configuration
Edit /etc/apache2/apache2.conf:

plaintext
Copy code
<Directory /var/www/html>
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
</Directory>
Python Web Server
Start a simple web server:

bash
Copy code
python3 -m http.server
Serve a specific directory:

bash
Copy code
python3 -m http.server --directory /path_to_directory
Virtual Private Network (VPN)
Description
VPNs create secure tunnels for encrypted data transmission, enabling secure remote access and anonymizing traffic. OpenVPN is a commonly used solution.

Installation
bash
Copy code
sudo apt install openvpn -y
Example Usage
Connect to a VPN using an .ovpn file:

bash
Copy code
sudo openvpn --config internal.ovpn
Configuration
Customize /etc/openvpn/server.conf to set encryption, routing, and traffic shaping options.

Contributions
Feel free to contribute by improving configurations, adding use cases, or suggesting additional network services.
