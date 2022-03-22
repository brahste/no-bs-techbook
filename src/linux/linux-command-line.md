# Linux Command Line Quick Guide

`find`

- `-type X` indicate the type of object trying to be found, options include `f` for file, `d` for directory 

## Networks and File Transfers

`scp`

- Secure file copy over SSH
  Usage:

## Monitoring System Processes

Every program on your system is running in a *process*. Each process has an associated process ID (PID). The PID is required when issing a command such as `kill` or `nice`. Processes are also run with a controlling terminal (TTY). If a process doesn't have a controlling terminal (e.g. they were initialized at boot time) are shown with `?`. Processes also have a CPU time (TIME), which denotes the amount of CPU time used by the process (different that run time). Each processes is initialized with a specific command (CMD).

`ps`

- This command gives a user access to view relevant information about processes running on a system.

    `x`: View all processes associated with the current user.

    `e`: View all processes in the system.

    `H`: Shows process heirarchy.

    `aux`: Combines the `a`, `u`, and `x` commands. Useful for majority of                                troubleshooting tasks.

`top` or `htop`

- This command provides much of the same information `ps aux` provides, but it dynamically updates and provides a quasi-graphical interface for a user to interact with to filter/manage system processes.

`kill`: to be filled

`nice`: to be filled.

## Working with Symbolic Links

To create a symbolic link use the command `ln -s <link-target> <symbolic-link>`.
To see your symbolic links you can use the `ls -lah` command. This will show the name of the link (`<symbolic-link>`) and the object its linked to (`<link-target>`).
To remove a symbolic link you can either use the `rm` or `unlink` command, though I prefer to use `unlink` since there's a lower chance of making unrecoverable errors, especially when working in below the `/home` directory. 

```bash
$ touch dummy.sh
$ ln -s dummy.sh dummy-link.sh
$ ls -lah | grep dummy
  rwxrwxrwx   1  braden  braden  8 B  Fri Jan 21 12:56:12 2022  dummy-link.sh ⇒ dummy.sh
  rw-rw-r--   1  braden  braden  0 B  Fri Jan 21 12:54:42 2022  dummy.sh 
$ unlink dummy-link.sh
$ ls -lah | grep dummy
  rw-rw-r--   1  braden  braden  0 B  Fri Jan 21 12:54:42 2022  dummy.sh
```
