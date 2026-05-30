Q: Core components of Linux
There are three types of core components in linux, Kernal, User space and init/systemd.

  **Kernal** 
This is the core of the Operating system.
Kernal acts as a bridge between Hardware and software.
It manages memory allocation, CPU scheduling, file system, networking etc.

  **User Space**
User space is where user runs applications.
Examples: Bash, Python, Docker, Nginx.
Applications communicate with the kernel through system calls. 
What are System Calls?
A system call is a request made by a user-space program to the Linux kernel to perform an operation that requires privileged access.

  **init/systemd**
init or systemd is the first process started by kernel whose process ID (PID) is 1.
system means who starts the process and d stands for deamon. the process works in the background.

Q: How processes are created and managed

What is a Process?
A running instance of a program is called as a process. Every process has a unique Process ID (PID).

How processes are created and managed?
1. Parent Process Uses fork()
The parent process is any already-running program. When it calls fork(), the OS makes an exact copy of itself memory, variables, open files, everything.

2. Child Process Is Created
The child is now a clone of the parent, running the same code from the same point.
Both processes continue executing independently from where fork() was called.
They share the same code but have separate memory spaces.

3. Child Loads a Program Using exec()
The child then calls exec(), which replaces its memory with a completely new program.
In short: fork duplicates, exec transforms. Together they give the OS a clean, flexible way to launch any program from any other program.


Q: What systemd does and why it matters.
Basically init or systemd is the first process started by kernel whose process ID (PID) is 1.
system means who starts the process and d stands for deamon. the process works in the background.



