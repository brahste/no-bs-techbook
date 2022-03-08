# Linux Command Line Quick Guide

`find`

- `-type X` indicate the type of object trying to be found, options include `f` for file, `d` for directory 


## Networks and File Transfers

`scp`

- Secure file copy over SSH
Usage:

## Monitoring System Processes

`top` or `htop`

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
