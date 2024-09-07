# Vulnversity
_Learn about active recon, web app attacks and privilege escalation._

![image](https://github.com/user-attachments/assets/0644b711-5394-4861-b3b7-dacb581e3d98)
![image](https://github.com/user-attachments/assets/13415f11-a36d-42f6-a0ba-4568319694b6)



![image](https://github.com/user-attachments/assets/8cc87bbe-3aca-45fd-8b86-038b0e77ffeb)
![image](https://github.com/user-attachments/assets/4a296704-105b-44d4-b708-75eea9efc5cb)



---------------
A **file descriptor (FD)** is a low-level, abstract representation for accessing files, network sockets, or other input/output (I/O) resources in operating systems like Linux, UNIX, and Windows. It's simply an integer that uniquely identifies an open file or resource, allowing programs to perform operations like reading from or writing to that file or resource.

### Key Concepts of File Descriptors

1. **Types of File Descriptors**:
   - **Standard File Descriptors**: These are predefined when a program starts.
     - **0**: **Standard Input (stdin)** – Used to read input (typically from the keyboard or another input device).
     - **1**: **Standard Output (stdout)** – Used to write output (typically to the terminal).
     - **2**: **Standard Error (stderr)** – Used to write error messages (separate from stdout, allowing errors to be handled differently).

2. **Extended File Descriptors**:
   - **3 and above**: File descriptors above 2 are used for additional resources like files, sockets, pipes, and other I/O streams. For example, when you open a file in a program, the operating system assigns it a file descriptor, starting from 3 onwards.

### Example of File Descriptors in Action

When a program opens a file or network socket, the OS returns a file descriptor, which the program can use to refer to that resource. Let’s go through an example:

```c
int fd = open("example.txt", O_RDONLY);
```

- The `open()` system call opens the file `example.txt` for reading (`O_RDONLY`), and returns a file descriptor (an integer).
- If successful, the FD returned might be `3` (since 0, 1, and 2 are reserved for stdin, stdout, and stderr).
  
Now, every time you want to read from or write to `example.txt`, you refer to it by this file descriptor (`fd`), rather than by its name.

### Standard File Descriptors

| FD Number | Name         | Description                                                  |
| --------- | ------------ | ------------------------------------------------------------ |
| **0**     | stdin        | Standard input, typically from the keyboard or a file.        |
| **1**     | stdout       | Standard output, typically to the terminal screen.            |
| **2**     | stderr       | Standard error, typically for error messages, also sent to the terminal. |

### **How File Descriptors Are Used**

#### 1. **File I/O**:
When you open a file, the OS gives you a file descriptor. You use this descriptor for operations like reading or writing to the file:
```c
int fd = open("file.txt", O_RDWR); // open file.txt and return FD (e.g., 3)
write(fd, "Hello", 5);            // use FD 3 to write to the file
close(fd);                        // close the FD when done
```

#### 2. **Pipes and Redirection**:
File descriptors are heavily used in redirection. For instance:
```bash
command > output.txt
```
This redirects the **stdout** (file descriptor 1) to a file `output.txt`, so any output of the command will go into that file.

You can also redirect stderr:
```bash
command 2> error.log
```
This sends the **stderr** (file descriptor 2) to `error.log`, so error messages from the command will be written to that file.

#### 3. **Duplication and Redirection**:
In shell scripts and system calls, file descriptors can be duplicated or redirected to point to the same place. For example:
```bash
command > output.txt 2>&1
```
This redirects both **stdout** (FD 1) and **stderr** (FD 2) to the same file `output.txt`.

#### 4. **Network Sockets**:
When you create a socket for network communication, the socket is also represented by a file descriptor. For example, when you use `fsockopen()` in PHP or `socket()` in C, the socket returns an FD.

### File Descriptor in Reverse Shells

In reverse shell attacks, like the PHP reverse shell you mentioned earlier, file descriptors are used to connect the attacker to the victim machine. Here's how they fit in:

- A network socket, just like a file, is opened by the server and assigned a file descriptor.
- By using `>&3`, the shell redirects output to the **socket** (FD 3), which is connected to the attacker's machine.
  
If the connection uses FD 3:
```bash
/bin/sh -i <&3 >&3 2>&3
```
- **stdin** is taken from the socket (FD 3), meaning the attacker can input commands.
- **stdout** and **stderr** are both redirected to FD 3, meaning any output or errors are sent back to the attacker.

If the socket isn’t using FD 3, you try higher file descriptors like 4, 5, or 6.

### **Checking Open File Descriptors**

You can check which file descriptors are in use for a process using the `lsof` (list open files) command:
```bash
lsof -p <PID>   # Where <PID> is the process ID.
```
This will show all the files and network connections (with their respective file descriptors) that a process has open.

---

### **Real-World Applications of File Descriptors**

- **Server Programming**: Web servers like Apache or Nginx use file descriptors to manage client connections. Each incoming connection is assigned a new FD.
- **Shell Redirection**: Shell scripts rely on file descriptor manipulation to manage output streams. 
- **Exploits and Security**: As shown in reverse shells, attackers use FDs to hijack stdin/stdout of processes and redirect them over network connections.

---

### Summary

File descriptors are the backbone of how Unix-like operating systems handle I/O for files, sockets, and other resources. They allow programs to open multiple resources and manage them efficiently, which is essential for tasks like reading from files, writing to network sockets, and handling redirection in shell scripts.

In security contexts, FDs can be exploited, particularly in attacks where an attacker gains control of input/output streams (e.g., reverse shells) by hijacking the file descriptors of running processes. Understanding file descriptors is key for system administrators and cybersecurity professionals to identify potential vulnerabilities and secure systems.
