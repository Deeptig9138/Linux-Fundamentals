# Firewall Setup 
This document provides an overview of the basics of firewall setup and configuration in Linux, focusing on the use of `iptables` for managing network traffic. It outlines the key concepts, components, and practical examples for implementing firewall rules effectively.

---

## Overview
Firewalls provide a security mechanism for controlling and monitoring network traffic. Linux firewalls, such as `iptables`, allow filtering incoming and outgoing traffic based on rules to prevent unauthorized access and mitigate security threats.

The Netfilter framework in the Linux kernel underpins `iptables`, enabling packet filtering and network traffic management. Modern alternatives include `nftables`, `ufw`, and `firewalld`.

---

## Components of iptables
- **Tables:** Organize firewall rules based on traffic type.
- **Chains:** Group rules for specific traffic processing stages.
- **Rules:** Define criteria for filtering traffic and specify actions for matched packets.
- **Matches:** Specify the characteristics of traffic to filter.
- **Targets:** Specify actions to take for matched traffic (e.g., ACCEPT, DROP).

---

## Tables and Chains

### Tables
| Table Name | Description                        | Built-in Chains                                 |
|------------|------------------------------------|-------------------------------------------------|
| `filter`   | Filters traffic based on criteria. | INPUT, OUTPUT, FORWARD                          |
| `nat`      | Modifies source/destination IPs.   | PREROUTING, POSTROUTING                         |
| `mangle`   | Alters packet headers.             | PREROUTING, OUTPUT, INPUT, FORWARD, POSTROUTING |

### Chains
- **Built-in Chains:** Predefined chains like `INPUT`, `OUTPUT`, and `FORWARD`.
- **User-Defined Chains:** Custom chains for managing specific traffic scenarios.

---

## Rules, Matches, and Targets

### Rules
- Define traffic filtering criteria using matches.
- Specify actions using targets.

### Common Targets
| Target Name | Description                                                 |
|-------------|-------------------------------------------------------------|
| `ACCEPT`    | Allows traffic through.                                     |
| `DROP`      | Silently blocks traffic.                                    |
| `REJECT`    | Blocks traffic and sends an error response to the source.   |
| `LOG`       | Logs packet information.                                    |
| `SNAT`      | Source Network Address Translation.                         |
| `DNAT`      | Destination Network Address Translation.                    |
| `MASQUERADE`| NAT for dynamic IP scenarios.                               |
| `REDIRECT`  | Redirects traffic to another port or IP address.            |

### Matches
| Match Name    | Description                                               |
|---------------|-----------------------------------------------------------|
| `-p`          | Protocol (e.g., TCP, UDP).                                |
| `--dport`     | Destination port.                                         |
| `--sport`     | Source port.                                              |
| `-s`          | Source IP.                                                |
| `-d`          | Destination IP.                                           |
| `-m state`    | Matches connection states (e.g., NEW, ESTABLISHED).       |

---

## Practical Examples

1. **Launch a web server on TCP/8080 and block traffic:**
   ```
   sudo iptables -A INPUT -p tcp --dport 8080 -j DROP
   ```

2. **Allow incoming traffic on TCP/8080:**
   ```
   sudo iptables -D INPUT -p tcp --dport 8080 -j DROP
   sudo iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
   ```
   
3. **Block traffic from a specific IP:**
   ```
   sudo iptables -A INPUT -s 192.168.1.100 -j DROP
   ```
   
4. **Allow traffic from a specific IP:**
   ```
   sudo iptables -A INPUT -s 192.168.1.101 -j ACCEPT
   ```
   
5. **Block traffic based on protocol (e.g., UDP):**
   ```
   sudo iptables -A INPUT -p udp -j DROP
   ```
   
6. **Allow traffic based on protocol (e.g., TCP):**
   ```
   sudo iptables -A INPUT -p tcp -j ACCEPT
   ```
   
7. **Create a new chain:**
   ```
   sudo iptables -N CUSTOM_CHAIN
   ```

8. **Forward traffic to a specific chain:**
   ```
   sudo iptables -A INPUT -p tcp --dport 80 -j CUSTOM_CHAIN
   ```

9. **Delete a specific rule:**
   ```
   sudo iptables -D INPUT -p tcp --dport 22 -j ACCEPT
   ```
   
10. **List all existing rules:**
    ```
    sudo iptables -L -v
    ```

---

## Commands Summary
- Add Rule: `iptables -A <CHAIN> -p <PROTOCOL> --dport <PORT> -j <TARGET>`
- Delete Rule: `iptables -D <CHAIN> <RULE_NUMBER>`
- List Rules: `iptables -L -v`
- Create Chain: `iptables -N <CHAIN_NAME>`
