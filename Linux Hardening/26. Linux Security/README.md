# Linux Security

## Introduction
Linux systems, though less prone to viruses compared to other operating systems like Windows, still require fundamental security measures to protect against intrusions. These measures help in securing the system from unauthorized access, privilege escalation, and other security vulnerabilities.

---

## Key Security Measures

### 1. Keep the System and Packages Updated
One of the most important aspects of securing a Linux system is keeping the OS and installed packages up to date. Use the following command to update your system:
```
username@htb[/htb]$ apt update && apt dist-upgrade
```

### 2. Firewall Configuration
If firewall rules are not set at the network level, Linux's built-in firewall (iptables) can be used to restrict traffic into and out of the host. Properly configured firewall rules are critical for limiting access to the system.

### 3. SSH Configuration
If SSH is enabled on the server:
- Disable password login to improve security.
- Prevent root user login via SSH.
- Use SSH key-based authentication instead of passwords.
- Limit login attempts using tools like fail2ban.
  
Example configuration to disable root login and password authentication in /etc/ssh/sshd_config:
```
PermitRootLogin no
PasswordAuthentication no
```

### 4. Access Control & Privilege Management
Administrators should avoid logging into and administering the system as the root user. Access control should be managed based on the principle of least privilege. Only allow users to execute specific commands as root using sudo:
```
username@htb[/htb]$ visudo
```

### 5. Monitoring and Auditing
Regularly audit the system for privilege escalation risks such as:
- Outdated kernel versions
- Misconfigured user permissions
- World-writable files
- Misconfigured cron jobs and services
  
### 6. SELinux / AppArmor
Security-Enhanced Linux (SELinux) or AppArmor are kernel security modules that provide mandatory access control (MAC). These modules control access between processes and resources on a granular level by enforcing policies.

For example, SELinux uses security labels to control access, ensuring that only authorized users or processes can modify or access specific files.

### 7. Additional Security Applications
Tools like Snort, chkrootkit, rkhunter, and Lynis can be used to enhance system security by detecting rootkits, misconfigurations, and vulnerabilities.

### 8. Other Security Settings
To further harden the system:
- Remove or disable unnecessary services and software.
- Remove services relying on unencrypted authentication.
- Enable NTP and ensure Syslog is running.
- Enforce strong password policies and password aging.
- Lock user accounts after multiple failed login attempts.
- Disable unwanted SUID/SGID binaries.

---

## TCP Wrappers

### Overview
TCP wrappers are a security feature that restricts access to network services based on IP addresses or hostnames. It works by consulting the /etc/hosts.allow and /etc/hosts.deny configuration files to determine whether a connection is allowed.

### Configuration Files
1) /etc/hosts.allow: Specifies which services are allowed access from specific IP addresses or hostnames.
2) /etc/hosts.deny: Specifies which services are denied access from specific IP addresses or hostnames.
   
### Example Configuration
/etc/hosts.allow

```
# Allow access to SSH from the local network
sshd : 10.129.14.0/24

# Allow access to FTP from a specific host
ftpd : 10.129.14.10

# Allow access to Telnet from any host in the inlanefreight.local domain
telnetd : .inlanefreight.local
```

/etc/hosts.deny

```
# Deny access to all services from any host in the inlanefreight.com domain
ALL : .inlanefreight.com

# Deny access to SSH from a specific host
sshd : 10.129.22.22

# Deny access to FTP from hosts with IP addresses in the range of 10.129.22.0 to 10.129.22.255
ftpd : 10.129.22.0/24
```

---

## Important Notes
- The order of rules in /etc/hosts.allow and /etc/hosts.deny is important. The first matching rule is applied.
- TCP wrappers are not a replacement for a firewall. They only control access to services, not ports.

---

## Conclusion
Securing a Linux system is an ongoing process. Administrators must stay vigilant, applying patches, reviewing system configurations, and ensuring that services are correctly configured to prevent unauthorized access. By following these guidelines and using tools like SELinux, fail2ban, and TCP wrappers, Linux systems can be hardened to defend against common threats.
