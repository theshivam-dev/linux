# Environment Variables

## What are Environment Variables?
Environment variables are key-value pairs used to configure settings and pass information to applications and processes in an operating system. They help manage configurations without modifying source code, making applications more flexible and secure.

## Types of Environment Variables
1. **System-wide Variables**
   - Set globally and available to all users and processes.
   - Example: `PATH`, `HOME`, `SHELL`
   
2. **User-specific Variables**
   - Defined for a specific user session.
   - Example: `EDITOR=vim`

3. **Temporary Variables**
   - Exist only in the current shell session.
   - Example: `export TEMP_VAR=value`

## Setting Environment Variables
### On Linux/macOS:
- Temporary (only for current session):
  ```sh
  export MY_VAR="Hello"
  echo $MY_VAR
  ```  
- Permanent (add to `~/.bashrc` or `~/.zshrc`):
  ```sh
  echo 'export MY_VAR="Hello"' >> ~/.bashrc
  source ~/.bashrc
  ```  

### On Windows (Command Prompt):
- Temporary:
  ```cmd
  set MY_VAR=Hello
  echo %MY_VAR%
  ```  
- Permanent (using PowerShell):
  ```powershell
  [System.Environment]::SetEnvironmentVariable("MY_VAR", "Hello", "User")
  ```  

## Accessing Environment Variables
### In JavaScript (Node.js):
```js
console.log(process.env.MY_VAR);
```

### In Python:
```python
import os
print(os.getenv("MY_VAR"))
```

## Environment Variable Separators in Windows and Linux
### Windows (`;` Separator)
- In Windows, environment variables (especially `PATH`) are separated by a **semicolon (`;`)**.
- Example:
  ```
  C:\Program Files\Node.js\;C:\Python39\;C:\Windows\System32\
  ```

### Linux (`:` Separator)
- In Linux, environment variables are separated by a **colon (`:`)**.
- Example:
  ```sh
  echo $PATH
  ```
  Output:
  ```
  /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
  ```

### Why This Difference?
- **Windows uses `;`** because file paths may contain spaces, and using a semicolon prevents confusion.
- **Linux uses `:`** since colons are **not used in file paths**, making them a safe delimiter.

## Security Considerations
- Never hardcode secrets in source code. Use `.env` files or secret managers.
- Restrict access to sensitive environment variables.
- Avoid exposing environment variables in logs or errors.

## Using .env Files
`.env` files store environment variables in a simple format:
```
DATABASE_URL=postgres://user:password@localhost:5432/db
API_KEY=secret123
```

### Loading `.env` in Node.js:
```js
require('dotenv').config();
console.log(process.env.DATABASE_URL);
```

