# Working with the Linux Kernel


Tip:

- You can find which kernel you're surrently running by using the `uname -r` command
- Other useful information can be found by using the `uname -a` command

The Linux kernel is the software that drives everything your computer does. Though you don't want to alter the kernel while it's running, you can manage kernel functionality without a reboot using Loadable Kernel Modules (LKMs). 'Kernel modules act as translators between hardware devices and the Linux kernel'.

## Finding Kernel Modules

Tips:

- Modules have a `.ko` (kernel object) extension and reside in the `/lib/modules/$(uname -r)/kernel` directory
- You can quickly see which kernel modules are currently loaded using `lsmod`
- You can also find all available modules using `modprobe -c` and piping the output to `grep` 

Adding a module to the kernel is *a lot* easier than it sounds

1. Ensure that the module is available using `find /lib/modules/$(uname -r) -type f -name <module-name>`
2. Load the module with `modprobe <module-name>`

### Additional commands

- `rmmod`
