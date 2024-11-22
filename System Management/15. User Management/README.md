# User Management
User management is a crucial aspect of Linux administration. It involves creating, modifying, and managing user accounts and their permissions. Understanding and effectively managing users and groups ensures secure and efficient system operations.

---

## Overview
User management tasks include:
- Creating new users.
- Adding users to specific groups.
- Executing commands as different users.
- Managing user permissions for files and directories.

---

## Execution as a Different User

### Example: Attempting to access restricted files as a regular user.
```
username@htb[/htb]$ cat /etc/shadow
cat: /etc/shadow: Permission denied
```

### Example: Executing the same command with elevated privileges:
```
username@htb[/htb]$ sudo cat /etc/shadow
root:<SNIP>:18395:0:99999:7:::
daemon:*:17737:0:99999:7:::
bin:*:17737:0:99999:7:::
<SNIP>
```

---

## Key Commands for User Management
| **Command** |	Description                                                               |
|-------------|---------------------------------------------------------------------------|
| **sudo	    | Execute a command as a different user.                                    |
| **su	      | Switch to another user ID (default is the superuser) and execute a shell. |
| **useradd	  | Create a new user or update default new user information.                 |
| **userdel	  | Delete a user account and related files.                                  |
| **usermod	  | Modify an existing user account.                                          |
| **addgroup  | Add a new group to the system.                                            |
| **delgroup  | Remove a group from the system.                                           |
| **passwd	  | Change a user password.                                                   |

---

## Examples

### Creating a New User
```
sudo useradd newuser
```

### Deleting a User
```
sudo userdel newuser
```

### Modifying a User
```
sudo usermod -aG sudo newuser  # Add user to the sudo group
```

### Adding a Group
```
sudo addgroup devteam
```

### Removing a Group
```
sudo delgroup devteam
```

### Changing a Password
```
passwd newuser
```

---

## Practice Tip
The best way to master user management is by experimenting with these commands and their options. Use a test environment to safely explore their functionalities.
