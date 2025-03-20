## **Linux File Permissions in Numbers (Octal Mode) Explained**  

In Linux, file permissions are represented using **three-digit octal (base 8) numbers**. Each digit corresponds to a permission set for **owner (user), group, and others**.

---

### **1. Number Representation of Permissions**
Each permission type is assigned a value:  
- **Read (`r`) = 4**  
- **Write (`w`) = 2**  
- **Execute (`x`) = 1**  
- **No permission = 0**

To get the final permission number, add up the values for each set:  
- `rwx = 4+2+1 = 7` (Full access)  
- `rw- = 4+2+0 = 6` (Read & write)  
- `r-x = 4+0+1 = 5` (Read & execute)  
- `r-- = 4+0+0 = 4` (Read-only)  
- `--- = 0+0+0 = 0` (No access)  

---

### **2. How Octal Permissions Work**
Each file has three sets of permissions:  
1. **First digit** → Owner (User)  
2. **Second digit** → Group  
3. **Third digit** → Others  

For example:  
```bash
chmod 754 file.txt
```
Breakdown of `754`:
- **7 (`rwx`)** → Owner has read, write, and execute.  
- **5 (`r-x`)** → Group has read and execute.  
- **4 (`r--`)** → Others have read-only.  

---

### **3. Common Permission Examples**
| Command | Permission | Explanation |
|---------|-----------|-------------|
| `chmod 777 file` | `rwxrwxrwx` | Full access to everyone (insecure). |
| `chmod 755 file` | `rwxr-xr-x` | Owner can modify, others can only read & execute (used for scripts). |
| `chmod 644 file` | `rw-r--r--` | Owner can edit, others can only read (default for text files). |
| `chmod 600 file` | `rw-------` | Only owner can read & write (private files). |
| `chmod 400 file` | `r--------` | Read-only file for owner, no access for others. |

---

### **4. Special Permissions (Extra Digit)**
1. **Set User ID (SUID) (`4xxx`)**  
   - If set on a file, it runs **as the owner**, not the user executing it.  
   - Example:  
     ```bash
     chmod 4755 script.sh
     ```
     - `4` → SUID bit  
     - `755` → Normal permission  
     - Result: `rwsr-xr-x` (The `s` means SUID is active)

2. **Set Group ID (SGID) (`2xxx`)**  
   - If set on a **directory**, files created inside inherit the group.  
   - Example:  
     ```bash
     chmod 2755 folder/
     ```
     - `2` → SGID bit  
     - `755` → Normal permission  
     - Result: `rwxr-sr-x`

3. **Sticky Bit (`1xxx`)**  
   - Applied to directories to **prevent users from deleting others' files**.  
   - Used for shared directories like `/tmp`.  
   - Example:  
     ```bash
     chmod 1777 /tmp
     ```
     - `1` → Sticky bit  
     - `777` → Full access  
     - Result: `rwxrwxrwt` (The `t` means sticky bit is active)

---

### **5. Viewing Default Permissions (`umask`)**
- The **umask value** defines default permissions for new files.  
- Check your umask:  
  ```bash
  umask
  ```
  - Common values:  
    - `022` → Default new files `644` (`rw-r--r--`), directories `755` (`rwxr-xr-x`).  
    - `077` → Default new files `600` (`rw-------`), directories `700` (`rwx------`).  

---

### **6. Summary**
- Permissions are represented in **three-digit octal format** (`chmod 754 file`).  
- **First digit → Owner**, **Second → Group**, **Third → Others**.  
- Use **special permissions** (`4xxx` for SUID, `2xxx` for SGID, `1xxx` for sticky bit).  
- **Use `umask` to set default permissions** for new files and directories.  

This system ensures proper file security and access control in Linux. 🚀