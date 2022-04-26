# Connecting to a NAS with Samba

> Resources:
> 
> - [How To Set Up a Samba Share For A Small Organization on Ubuntu 16.04 | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-samba-share-for-a-small-organization-on-ubuntu-16-04)
> 
> - [Network Administration: Samba smb.conf File - dummies](https://www.dummies.com/programming/networking/network-administration-samba-smb-conf-file/)

# What is Samba?

Samba is an open-source application that enables users to use the SMB/CIFS networking protocol used in Windows. In short, this allows Linux users to mount network drives on their devices, providing easy access either from the command line or file explorer.

# Set up

While it is feasible to set up a Samba fileshare from the command line, it is likely going to be easier to do it through the GUI of the shared file drive itself.

# Logging Into the Samba Server

On Linux there is a tool called `smbclient` that can be used to log into network drives.

```
sudo apt update
sudo apt install smbclient
```

Access the Samba CLI with `smbclient`.

```
smbclient //<nas-hostname-or-ip>/<shared-folder> -U <username>
```

You will be prompted to enter your password. For convenience, you can set up hostnames to access the Samba share in */etc/samba/smb.conf*, but you can also use the IP of the network file server as well. For example,

```
smbclient //10.0.0.21/Projects -U robert
```

If you can access the Samba drive with `smbclient` then you can mount the drive to your filesystem for more seamless access.

> Note: If you're mounting a *cifs* drive you may also have to install `cifs-utils`.

```
mount -t cifs -o credentials=/etc/cifs_passwd,vers=1.0 //10.0.0.21/Project /mnt/locations
```

Where the file `/etc/cifs_passwd` is a text file, should not have read permissions except by `root` (so you'll have to use `sudo`) and is formatted like,

```
username=engineering
password=qwerty123
```

In the above command, */mnt/location* can be any location on your device that you choose, but mounting it under */mnt/* or */media/* is often a good choice.
