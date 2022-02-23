# Connecting to a NAS with Samba

Resources:
- https://www.digitalocean.com/community/tutorials/how-to-set-up-a-samba-share-for-a-small-organization-on-ubuntu-16-04
- https://www.dummies.com/programming/networking/network-administration-samba-smb-conf-file/

# What is Samba

Samba is an open-source application that enables users to use the SMB/CIFS networking protocol used in Windows.

# Set up

While it is feasible to set up a Samba fileshare from the command line, it is likely going to be easier to do it through the GUI of the shared file drive itself.

# Logging Into the Samba Server

On Linux there is a tool called `smbclient` that can be used to log into file drives served over a network.
```
sudo apt update
sudo apt install smbclient
```

Access the Samba shares with `smbclient` by formatting your command in the following way
```
smbclient //<nas-hostname-or-ip>/<shared-folder> -U <username>
```

You can set up hostnames to access the Samba share in `/etc/samba/smb.conf`, but you can also use the IP of the network file server as well. For example,

```
smbclient //10.0.0.21/Projects -U engineering
```

If you can access the Samba drive with `smbclient` then you can mount the driver to your filesystem for more seamless access

```
mount -t cifs //10.0.0.21/Projects -o credentials=/etc/cifs_passwd,ver=1.0
```

Where the file `/etc/cifs_passwd` should not have read permissions except by `root` and is formatted like
```
username=engineering
password=qwerty123
```

It may also be required that you installs `cifs-utils`.
