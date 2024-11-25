# Network Configuration

## Penetration Testing
Penetration testing (pen testing) is a critical process for identifying and addressing vulnerabilities in Linux systems. It simulates cyber attacks to evaluate the effectiveness of security measures, detect vulnerabilities, and assess how well the system can resist attacks.

### Key Phases of Penetration Testing:
1. **Reconnaissance**:
    - **Active Reconnaissance**: Directly probing the target, such as scanning ports and services using tools like `Nmap` or `Nikto`.
    - **Passive Reconnaissance**: Gathering publicly available information such as WHOIS data, DNS information, and social engineering.

2. **Vulnerability Assessment**: 
    - After reconnaissance, vulnerabilities are identified using scanning tools like `Nessus`, `OpenVAS`, or `Nmap` for specific software weaknesses or misconfigurations.
    - Checking for open ports, vulnerable versions, weak passwords, and security loopholes.

3. **Exploitation**:
    - Attempting to exploit identified vulnerabilities to gain unauthorized access. This may involve techniques like SQL injection, buffer overflow, or exploiting weak configuration.
    - Tools like `Metasploit` or `Burp Suite` are used for this phase.

4. **Post-Exploitation**:
    - Once access is obtained, the attacker may escalate privileges, extract sensitive data, or pivot to other parts of the network.
    - This phase involves activities like maintaining persistence, covering tracks, and escalating privileges.

5. **Reporting**:
    - A comprehensive report is generated outlining vulnerabilities discovered, methods used, impact, and recommendations for remediation.

### Tools Commonly Used in Penetration Testing:
- **Nmap**: For network discovery and vulnerability scanning.
- **Metasploit Framework**: A tool for developing and executing exploit code.
- **Wireshark**: For packet capturing and traffic analysis.
- **Burp Suite**: For web application penetration testing.
- **Hydra**: For brute-forcing login credentials.
  
#### Ethical Considerations:
Penetration testing must always be done under the correct legal framework, with explicit permission from the target organization. Unauthorized penetration testing is illegal and unethical.

---

## System Hardening
System hardening is the practice of securing a computer system by reducing its vulnerabilities, making it more resilient to attacks. In the context of penetration testing, it’s crucial to harden Linux systems to prevent exploits during a test.

### Key Hardening Measures:
1. **System Updates**: Regularly updating the system is one of the most effective ways to close security gaps.
    ```
    sudo apt update && sudo apt upgrade -y
    ```

2. **Disabling Unnecessary Services**: Disable services you don’t need to minimize attack surfaces. Use the `systemctl` command to manage services.
    ```
    sudo systemctl stop <service_name>
    sudo systemctl disable <service_name>
    ```

3. **SSH Configuration**: Secure SSH access by modifying the `/etc/ssh/sshd_config` file.
    - Disable root login: `PermitRootLogin no`
    - Enforce SSH key-based authentication: `PasswordAuthentication no`

4. **Firewall Configuration**: Use a firewall to restrict access to services.
    - Using `UFW` (Uncomplicated Firewall) on Ubuntu:
    ```
    sudo ufw allow ssh
    sudo ufw enable
    ```

5. **Audit Logging**: Keep track of system activity to detect malicious behavior.
    - Use `auditd` to monitor file access, system changes, and suspicious activity.
    ```
    sudo apt install auditd
    sudo service auditd start
    ```

6. **Password Policies**: Implement strong password policies to prevent brute-force and dictionary attacks.
    - Use `passwd` command to enforce password expiration policies:
    ```
    sudo chage -M 90 <username>
    ```

7. **File Integrity Monitoring**: Use tools like `AIDE` to monitor system files for unexpected changes.
    ```
    sudo apt install aide
    sudo aideinit
    ```

8. **AppArmor/SELinux**: These are security modules used to enforce mandatory access controls (MAC). They provide a framework to restrict the capabilities of processes.

---

## Hardening Using SELinux, AppArmor, and TCP Wrappers
In addition to general hardening techniques, there are more specific tools like SELinux, AppArmor, and TCP Wrappers that provide additional layers of security by controlling access to system resources.

### SELinux (Security-Enhanced Linux)
SELinux is an integrated security system that enforces the principle of least privilege, providing fine-grained access controls for resources.

1. **Install SELinux on your VM**:
    - For CentOS/RHEL:
    ```
    sudo yum install policycoreutils selinux-policy-targeted
    sudo setenforce 1
    ```

2. **Configure SELinux to prevent a user from accessing a specific file**:
    - You can label files to restrict access using SELinux file contexts.
    ```
    semanage fcontext -a -t user_home_t "/path/to/file"
    restorecon -v /path/to/file
    ```

3. **Configure SELinux to allow a specific user to access a service but deny access to others**:
    - Set the appropriate SELinux booleans or ports for the service.
    ```
    semanage port -a -t http_port_t -p tcp 8080
    ```

4. **Deny access to a user or group for a network service**:
    - Restrict access to network services by adjusting SELinux settings:
    ```
    setsebool -P httpd_can_network_connect 0
    ```

### AppArmor
AppArmor is similar to SELinux but is considered easier to configure. It uses profiles that define the resources applications can access.

5. **Configure AppArmor to prevent a user from accessing a file**:
    - You can create AppArmor profiles for applications and restrict file access:
    ```
    sudo aa-logprof
    ```

6. **Configure AppArmor to allow a user to access a service but deny others**:
    - Modify `/etc/apparmor.d/usr.sbin.apache2` to specify allowed actions.
    ```
    /path/to/service/** r,
    ```

7. **Deny a user/group access to a service**:
    - Add denial rules to the AppArmor profile.
    ```
    deny /path/to/file r,
    ```

### TCP Wrappers
TCP Wrappers control access to network services based on IP addresses.

8. **Allow access from a specific IP address**:
    - Edit `/etc/hosts.allow` to allow specific IPs:
    ```
    sshd: 192.168.1.100
    ```

9. **Deny access from a specific IP address**:
    - Deny access by adding to `/etc/hosts.deny`:
    ```
    sshd: 192.168.1.101
    ```

10. **Allow access from a range of IP addresses**:
    - Allow a subnet by adding to `/etc/hosts.allow`:
    ```
    sshd: 192.168.1.100/255.255.255.0
    ```

---

### Conclusion
Implementing effective network security measures such as penetration testing and system hardening techniques is essential for protecting Linux systems. By configuring SELinux, AppArmor, and TCP Wrappers, administrators can significantly reduce the risk of unauthorized access and exploitation. These tools provide fine-grained control over system resources and enhance overall system security, helping to prevent potential breaches, especially during penetration tests.

Remember to keep your systems updated, disable unnecessary services, use firewalls, and apply least privilege principles in all configurations. It’s also important to practice your skills in a controlled environment, such as using personal VMs or containers, and always take snapshots before making significant changes.

With a commitment to these security best practices, you can ensure a robust, secure system that can withstand attacks and safeguard sensitive data.
