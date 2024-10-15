### Linux Accounts: Comprehensive Beginner’s Guide

#### 1. **Introduction to Linux Accounts**
Linux is a multi-user operating system, meaning that multiple users can access and use the system simultaneously. Each user is associated with an **account** that helps manage permissions and security. This guide covers the basics of user management, account types, how Linux accounts work, and how to manage users and groups effectively.

---

### 2. **Understanding Linux User Accounts**
Linux user accounts are essential for managing access to resources on the system. They ensure that only authorized users can access specific files, directories, and services.

Each Linux account is defined by:
- **Username**: The unique name used to identify a user.
- **User ID (UID)**: A unique numerical identifier assigned to each user.
- **Home Directory**: The directory where the user’s personal files are stored.
- **Shell**: The command interpreter assigned to the user (e.g., `/bin/bash`).
- **Password**: Used to authenticate the user when logging in.

---

### 3. **Types of User Accounts in Linux**
Linux systems typically have three types of user accounts:

#### 3.1. **Root User (Superuser)**
- **Root** is the most powerful account on the system and has unrestricted access to all commands and files.
- This account is used for administrative tasks such as installing software, changing system settings, and managing other users.
- The **UID** for the root user is always `0`.
- **Command prompt for root**: `#`

Because of its power, you should use the root account sparingly. Instead, use **sudo** for running administrative commands as a regular user.

#### 3.2. **Regular Users**
- Regular users are created for general use, and they have restricted access compared to the root user.
- Each regular user has a unique username, home directory, and shell. They can only modify files and processes they own unless granted additional privileges.
- **UID** for regular users starts from `1000` on most Linux systems.
- **Command prompt for regular users**: `$`

#### 3.3. **System Users (Service Accounts)**
- These accounts are created by the system or applications to run services such as web servers (e.g., Apache) or databases (e.g., MySQL).
- System users typically do not log in interactively and are used to manage specific processes.
- System users usually have UIDs between `1` and `999`.

---

### 4. **User Management in Linux**

#### 4.1. **Creating a New User**
To create a new user, you use the `useradd` command or the more user-friendly `adduser` command.

- **Creating a user**:
  ```bash
  sudo adduser username
  ```
  This command creates a new user with a home directory (`/home/username`) and prompts you to set a password.

#### 4.2. **Modifying an Existing User**
You can modify user details using the `usermod` command.

- **Change the user’s shell**:
  ```bash
  sudo usermod -s /bin/zsh username
  ```

- **Add a user to a group**:
  ```bash
  sudo usermod -aG groupname username
  ```

#### 4.3. **Deleting a User**
To delete a user and their home directory, use the `userdel` command.

- **Delete a user**:
  ```bash
  sudo userdel username
  ```

- **Delete a user and their home directory**:
  ```bash
  sudo userdel -r username
  ```

#### 4.4. **Listing Users**
All user accounts are stored in the `/etc/passwd` file. You can view this file to see a list of all users on the system.

- **List all users**:
  ```bash
  cat /etc/passwd
  ```

Each line in `/etc/passwd` contains information about a user, including their username, UID, home directory, and shell.

---

### 5. **Linux User Account Files**
Linux stores information about users and groups in specific configuration files:

#### 5.1. **/etc/passwd**
This file contains basic information about user accounts.

Example `/etc/passwd` entry:
```
username:x:1001:1001:User Name:/home/username:/bin/bash
```
Fields:
- `username`: The user’s login name.
- `x`: Placeholder for the password (actual passwords are stored in `/etc/shadow`).
- `1001`: User ID (UID).
- `1001`: Group ID (GID).
- `User Name`: Full name or description of the user.
- `/home/username`: The user’s home directory.
- `/bin/bash`: The user’s shell.

#### 5.2. **/etc/shadow**
This file stores encrypted passwords and additional password-related information.

Example `/etc/shadow` entry:
```
username:$6$OqG3F$wQhcDxtk7opkrA.x:18723:0:99999:7:::
```
Fields:
- `username`: The user’s login name.
- `$6$OqG3F$wQhcDxtk7opkrA.x`: The encrypted password.
- `18723`: Date of the last password change.
- Additional fields store password expiry and aging information.

#### 5.3. **/etc/group**
This file defines groups and group memberships.

Example `/etc/group` entry:
```
sudo:x:27:username
```
Fields:
- `sudo`: The group name.
- `x`: Placeholder for group password.
- `27`: Group ID (GID).
- `username`: List of users in the group.

---

### 6. **Linux Groups**
In Linux, groups are used to manage user permissions. Users can belong to one or more groups, and group membership determines access to files and resources.

#### 6.1. **Primary and Secondary Groups**
- **Primary Group**: The primary group is the user’s default group and is typically used when creating new files or directories.
  - The primary group is defined in the `/etc/passwd` file (4th field).
  
- **Secondary Groups**: Users can belong to additional groups, giving them extra privileges. For example, adding a user to the `sudo` group allows them to execute commands as root.

#### 6.2. **Managing Groups**
- **Create a new group**:
  ```bash
  sudo groupadd groupname
  ```

- **Add a user to a group**:
  ```bash
  sudo usermod -aG groupname username
  ```

- **List user’s groups**:
  ```bash
  groups username
  ```

- **Change user’s primary group**:
  ```bash
  sudo usermod -g groupname username
  ```

---

### 7. **Sudo and Root Privileges**
In Linux, administrative tasks (such as installing software or managing system files) require elevated privileges. Instead of logging in as root, it’s safer to use the **sudo** command, which allows a regular user to execute commands as root.

#### 7.1. **Granting a User Sudo Privileges**
To give a user administrative privileges, you need to add them to the `sudo` group.

- **Add a user to the sudo group**:
  ```bash
  sudo usermod -aG sudo username
  ```

Now, the user can run commands as root by typing `sudo` before the command.

#### 7.2. **Using Sudo**
When a user has sudo privileges, they can execute any command with administrative rights by prefixing it with `sudo`.

Example:
```bash
sudo apt update
```
The system will prompt for the user’s password, and then the command will run with root privileges.

#### 7.3. **Sudoers File**
The `sudoers` file (`/etc/sudoers`) defines which users or groups have permission to run `sudo`. This file should only be edited using the `visudo` command to prevent syntax errors.

---

### 8. **Password Management**
Password security is critical for maintaining a secure Linux system. Passwords are stored in an encrypted format in the `/etc/shadow` file.

#### 8.1. **Changing a User’s Password**
To change a user’s password, use the `passwd` command.

- **Change your own password**:
  ```bash
  passwd
  ```

- **Change another user’s password** (as root):
  ```bash
  sudo passwd username
  ```

#### 8.2. **Password Expiration and Aging**
Linux allows you to set password expiration policies for users.

- **View password status for a user**:
  ```bash
  sudo chage -l username
  ```

- **Force a password change every 90 days**:
  ```bash
  sudo chage -M 90 username
  ```

- **Disable a user’s password** (lock the account):
  ```bash
  sudo passwd -l username
  ```

---

### 9. **Account Security Best Practices**
To maintain a secure Linux environment, consider the following best practices:

- **Use strong passwords**: Enforce password complexity rules and change passwords periodically.
- **Minimize the use of root**: Only use root access when necessary. Use `sudo` for administrative tasks.
- **Lock inactive accounts**: Disable accounts that are no longer in use to prevent unauthorized access.
  ```bash
  sudo usermod -L username
  ```
- **Monitor login attempts**: Use tools like `last` and `

faillog` to check recent logins and failed login attempts.

---

### 10. **Conclusion**
Understanding Linux accounts is crucial for managing users, securing access, and ensuring system integrity. Regular users, the root account, and system users all have different roles, and learning how to create, modify, and manage these accounts is key to effective Linux administration.

---

### Linux Access Control Files: Comprehensive Beginner’s Guide

#### 1. **Introduction to Linux Access Control**
Access control in Linux determines who can read, modify, or execute files and directories. It is a fundamental aspect of Linux security, ensuring that only authorized users can access sensitive data or perform specific actions. Linux implements access control using **file permissions** and more advanced mechanisms like **Access Control Lists (ACLs)**. This guide covers file permissions, ACLs, and configuration files used to control access in a beginner-friendly way.

---

### 2. **Linux File Permissions**
Linux uses a permission model based on **users**, **groups**, and **others**. Every file and directory in Linux has associated permissions that define what actions a user can perform.

Each file or directory has three permission sets:
- **User (u)**: The owner of the file.
- **Group (g)**: Users who are part of the group associated with the file.
- **Others (o)**: All other users on the system who are not the owner or part of the group.

#### 2.1. **Permission Types**
There are three types of permissions:
- **Read (r)**: Allows reading the contents of a file or listing the contents of a directory.
- **Write (w)**: Allows modifying the file’s contents or making changes within a directory (e.g., creating/deleting files).
- **Execute (x)**: Allows executing the file (for scripts or programs) or accessing a directory.

#### 2.2. **Viewing File Permissions**
You can view the permissions of files and directories using the `ls -l` command:

```bash
ls -l
```

Example output:
```
-rw-r--r-- 1 user group 1024 Oct 10 12:34 example.txt
```

The permission string in this example is `-rw-r--r--`:
- The first character (`-`) indicates that it’s a file (if it were a directory, this would be `d`).
- The next three characters (`rw-`) represent the owner’s permissions: **read** and **write**.
- The next three characters (`r--`) represent the group’s permissions: **read** only.
- The last three characters (`r--`) represent the others’ permissions: **read** only.

#### 2.3. **Changing File Permissions**
You can modify file permissions using the `chmod` command. You can set permissions in two ways:
- **Symbolic mode**: Using letters to represent permissions.
- **Numeric mode**: Using numbers to represent the permission bits.

##### Symbolic Mode
- **Syntax**: `chmod [who][operation][permissions] filename`

- Example: Give the owner execute permission:
  ```bash
  chmod u+x example.sh
  ```

- Remove read permission for others:
  ```bash
  chmod o-r example.txt
  ```

##### Numeric Mode
Permissions are represented by numbers:
- **4**: Read (`r`)
- **2**: Write (`w`)
- **1**: Execute (`x`)

Each permission set is the sum of these values. For example:
- `7` (read + write + execute) = `4 + 2 + 1`
- `5` (read + execute) = `4 + 1`

- **Syntax**: `chmod [permissions] filename`

Example:
```bash
chmod 755 example.sh
```
This sets:
- Owner: Read, write, execute (`7`).
- Group: Read, execute (`5`).
- Others: Read, execute (`5`).

---

### 3. **Ownership in Linux**
Each file and directory in Linux is owned by a **user** and a **group**. The owner has special permissions over the file.

#### 3.1. **Changing Ownership**
You can change the owner or group of a file using the `chown` command.

- **Change the owner**:
  ```bash
  sudo chown new_owner filename
  ```

- **Change the group**:
  ```bash
  sudo chown :new_group filename
  ```

- **Change both owner and group**:
  ```bash
  sudo chown new_owner:new_group filename
  ```

#### 3.2. **Changing the Group Only**
You can use the `chgrp` command to change only the group.

- **Example**:
  ```bash
  sudo chgrp new_group filename
  ```

---

### 4. **Special File Permissions**
Linux includes special permissions that provide more control over file execution and directory access.

#### 4.1. **Setuid (Set User ID)**
When a file with the **setuid** bit set is executed, the process runs with the privileges of the file owner rather than the user running it. This is commonly used in system binaries like `passwd`.

- **Set setuid**:
  ```bash
  chmod u+s filename
  ```

- **Example**:
  ```bash
  ls -l /usr/bin/passwd
  ```
  Output:
  ```
  -rwsr-xr-x 1 root root 52480 Jun 28 18:35 /usr/bin/passwd
  ```

#### 4.2. **Setgid (Set Group ID)**
When the **setgid** bit is set on a file, the file executes with the privileges of the group that owns the file. When set on a directory, all files created inside inherit the group ownership of the directory.

- **Set setgid**:
  ```bash
  chmod g+s directory_name
  ```

#### 4.3. **Sticky Bit**
The **sticky bit** is used on directories to ensure that only the owner of a file can delete or modify it, even if other users have write permissions to the directory. This is commonly used on directories like `/tmp`.

- **Set sticky bit**:
  ```bash
  chmod +t directory_name
  ```

- **Example**:
  ```bash
  ls -ld /tmp
  ```
  Output:
  ```
  drwxrwxrwt 10 root root 4096 Oct 10 16:32 /tmp
  ```

---

### 5. **Access Control Lists (ACLs)**
Standard Linux file permissions are somewhat limited in flexibility. For more fine-grained access control, Linux supports **Access Control Lists (ACLs)**, which allow you to specify different permissions for individual users or groups beyond the traditional owner/group/others model.

#### 5.1. **Viewing ACLs**
To check if a file or directory has ACLs, use the `getfacl` command.

- **View ACLs**:
  ```bash
  getfacl filename
  ```

Example output:
```
# file: filename
# owner: user
# group: group
user::rw-
user:another_user:r--
group::r--
mask::r--
other::r--
```

#### 5.2. **Setting ACLs**
You can add or modify ACLs using the `setfacl` command.

- **Set ACL for a user**:
  ```bash
  setfacl -m u:username:permission filename
  ```

  Example: Grant read (`r`) permission to `john` on `example.txt`:
  ```bash
  setfacl -m u:john:r example.txt
  ```

- **Set ACL for a group**:
  ```bash
  setfacl -m g:groupname:permission filename
  ```

- **Set default ACLs** (for new files created in a directory):
  ```bash
  setfacl -m d:u:username:rwx directory_name
  ```

#### 5.3. **Removing ACLs**
To remove an ACL, use the `-x` option:

- **Remove an ACL for a user**:
  ```bash
  setfacl -x u:username filename
  ```

- **Remove all ACLs**:
  ```bash
  setfacl -b filename
  ```

---

### 6. **Important Access Control Configuration Files**
Several key files in Linux control system-wide access, especially for limiting user access to the system or network resources.

#### 6.1. **/etc/passwd**
This file stores information about all system users, including their home directories, shells, and UIDs. It does not store passwords (those are in `/etc/shadow`).

- Example entry:
  ```
  user:x:1000:1000:User Name:/home/user:/bin/bash
  ```

#### 6.2. **/etc/shadow**
This file contains encrypted passwords and other password-related information like expiration dates.

- Example entry:
  ```
  user:$6$wVQ..../:18730:0:99999:7:::
  ```

#### 6.3. **/etc/group**
This file contains information about groups and their memberships.

- Example entry:
  ```
  sudo:x:27:user
  ```

#### 6.4. **/etc/sudoers**
This file controls which users and groups can run commands with elevated privileges via `sudo`. Always edit this file using `visudo` to avoid syntax errors.

- Example entry:
  ```
  user ALL=(ALL:ALL) ALL
  ```

---

### 7. **Best Practices for Access Control**
1. **Use Least Privilege**: Ensure users have the minimum permissions needed to perform their tasks. Avoid granting write or execute permissions unnecessarily.
   
2. **Group Management**: Assign users to groups to simplify permission management rather than granting individual permissions.

3. **Use ACLs When Needed**: For complex permission scenarios, use ACLs to

 fine-tune access control.

4. **Monitor Permissions Regularly**: Review permissions periodically to ensure security policies are enforced.

5. **Setuid/Setgid with Caution**: Use `setuid` and `setgid` only when absolutely necessary, as they grant elevated privileges that could pose security risks.

---

### 8. **Conclusion**
Linux access control involves managing file permissions, ownership, and advanced mechanisms like ACLs. Understanding how these work is essential for securing your system, controlling who can access files and directories, and ensuring that users have appropriate levels of access. By applying best practices and using the right tools, you can effectively manage access to resources on a Linux system.
