# Understanding Sysfs and Procfs File Systems

## `procfs`: The `proc` File System

Files in the `/proc` directory provide information about processes on your system. The `procfs` is a _virtual filesystem_. Some of the files provide information on the hardware running on your system, others provide information and the ability to modify the system configuration. 

Typically you can view items on the `proc` file system using commands such as `cat` and `less`, though some specific commands exist to view certain types of hardware and system information (e.g. `lspci`). To modify items on the `proc` file system, the `echo` command is useful along with the redirect operator `>`.

```bash
echo value > /proc/foo/bar
```

## `sysfs`: The `sys` File System

The `sysctl` utility can be used to view and modify writable files in the `/proc/sys` directory. In other words, it is used to modify kernel parameters at runtime. The files under `sysfs` provide information about devices, kernel modules, filesystems, and other kernel components. Most of the files in the `sysfs` are read only and can be used to understand the system.
