# Probing Unfamilar Devices

When working with embedded linux devices where you only have command line access, there are still several ways that you can gain basic information about the system. This can be important to understand how to interact with it and its processes.

## System & Architecture

`uname -a`
- Provides info on system hardware, kernel, and hostname

`lscpu`
- CPU info and architecture

`lshw -short`
- Lists info about system hardware
- Pro tip: The standrd `lshw` command is very verbose. Redirect output to html and view it with `sudo lshw -html > hwinfo.html && firefox hwinfo.html`
## Processes & Services

`top` or `htop`
    
- Shows the processes that are running and the command that spawned them (among other things)

    - Often embedded devices don't run too many processes because they're specialized for specific tasks 

`systemctl list-unit-files` 
- These files are located in `/lib/systemd/system` and are the raw text files that encode info about the associated service, socket, etc.

`systemctl list-units`
- Lists all current units (eg. services, sockets, devices) in memory

- Tips:
    - To search a for a service use `systemctl list-unit-files | grep <search-string>`. You can then manage that service as discussed in *no-bs-systemd*

## Network

`ip a`
- Display information about currently configured IP addresses, MAChine addresses, and network connections

`ip r`
- Display the IP of your gateway/router

`[sudo] nmap -sn <subnet>`
- Conduct a ping scan on the specified subnet (eg. `nmap -sn 192.168.1.0/24`)

## Devices

`lsblk`
- Lists info on block storage devices (eg. hard drives, partitions, flash drives)

`lsusb -t`
- Lists info on USB devices with a tree-like structure

`lsmod`
- Lists info on loadable kernel modules
