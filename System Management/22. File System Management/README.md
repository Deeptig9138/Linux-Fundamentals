# File System Management
File system management on Linux involves organizing and maintaining data stored on disks or storage devices. Linux supports multiple file systems, such as `ext2`, `ext3`, `ext4`, `XFS`, `Btrfs`, and `NTFS`, each catering to different requirements:

- **ext2**: Basic file system management tasks.
- **Btrfs**: Data integrity and snapshot capabilities.
- **NTFS**: Windows compatibility.

Proper analysis of the application or user needs is crucial before selecting a file system.

---

## File System Hierarchy
Linux uses a Unix-based hierarchical file system structure, with components such as:

1. **Inode Table**: 
   - Contains metadata (permissions, size, type, owner) for files/directories.
     
2. **File Types**:
   - **Regular files**: Stored in directories, accessible directly.
   - **Directories**: Contain collections of files.
   - **Symbolic links**: References to other files/directories for quick access.
  
---

## Managing File Permissions

File and directory permissions control access and consist of three types:
- **Read (r)**: View contents.
- **Write (w)**: Modify contents.
- **Execute (x)**: Run the file or access the directory.

Example:
```
ls -il
10678872 -rw-r--r--  1 user group 234123 Feb 14 19:30 myscript.py
10678869 -rw-r--r--  1 user group 43230 Feb 14 11:52 notes.txt
```

---

## Disk Management
Linux manages physical storage devices like hard drives, SSDs, and removable devices using tools such as fdisk, gpart, and GParted.

### Partitioning with fdisk

Example usage:
```
sudo fdisk -l
```

Output:
```
Disk /dev/vda: 160 GiB, 171798691840 bytes, 335544320 sectors
Device     Boot     Start       End   Sectors  Size Id Type
/dev/vda1  *         2048 158974027 158971980 75.8G 83 Linux
/dev/vda2       158974028 167766794   8792767  4.2G 82 Linux swap / Solaris
```

---

## Mounting and Unmounting
Mounting attaches a drive to a specific directory, making it accessible within the file system hierarchy.

### Mount a File System
```
sudo mount /dev/sdb1 /mnt/usb
cd /mnt/usb && ls -l
```

### Unmount a File System
```
sudo umount /mnt/usb
```

Check active processes using the file system:
```
lsof | grep <mount-point>
```

### Configuring Mounts at Boot
Define file systems in /etc/fstab for automatic mounting at boot. Example:
```
/dev/sda1 / ext4 defaults 0 0
/dev/sda2 /home ext4 defaults 0 0
/dev/sdb1 /mnt/usb ext4 rw,noauto,user 0 0
192.168.1.100:/nfs /mnt/nfs nfs defaults 0 0
```

---

## Swap Space Management
Swap space is used for memory management when physical memory is full.

### Create and Activate Swap
```
sudo mkswap /dev/sdx
sudo swapon /dev/sdx
```

### Hibernation
Swap can store the system's state during hibernation, enabling power-off without data loss.

---

## Useful Commands

- View mounted file systems:
  ```
  mount
  ```
  
- Disk usage and storage details:
  ```
  df -h
  ```
  
- List open files:
  ```
  lsof
  ```
  
Linux file system and disk management are powerful tools for ensuring optimal system performance and data integrity.
