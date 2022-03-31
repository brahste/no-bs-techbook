# Setting up SSH SOCKS Tunnels

> Links:
> 
> https://linuxize.com/post/how-to-setup-ssh-socks-tunnel-for-private-browsing/

Using an SSH SOCKS proxy tunnel allows you to route local traffic through an encrypted proxy. This lets any programs using the proxy to connect to the server which will then forward traffic to the intended destination IP.

## Creating the Tunnel with SSH

To create an SSH proxy tunnel run

```
ssh -f -N -D <port> <user>@<proxy-ip>
```

Here the option `-f` runs the command in the background so a terminal window isn't required to remain open for the tunnel to exist, `-N` tells SSH not to execute a remote command, `-D <port>` opens a SOCKS tunnel on the `<port>` provided (make sure to use a port number greater than 1024), and `<user>@<proxy-ip>` is the information of the proxy server. Optionally a `-p <port-ssh>` can be used if SSH is not running on the default port 22.

## Configuring an Application to Use the Proxy

Whether using Firefox, Google Chrome, FileZilla, or any other program, there is typically a way to configure the proxy settings. In the proxy settings page enter the loopback address (e.g. `127.0.0.1`) as the SOCKS 5 host and the `<port>` specified when the SSH proxy was initialized.

### FileZilla

Using FileZilla follow these steps

1. Go to *Edit > Settings...*

2. Go to *Connection > Generic Proxy*

3. Select *SOCKS 5*

4. Set *Proxy host:* 127.0.0.1; *Proxy port:* <port>; and the proxy user and password according to the user and password you would otherwise connect to through SSH

## Example

A server or headless embedded device (*dev2*) is accessible only through a remote shell session from another server or headless device (*dev1*). To access *dev2* one can SSH through *dev1*.

```bash
orig@comp $ ssh user1@<dev1_ip>
user1@dev1 $ ssh user2@<dev2_ip>
user2@dev2 $
```

Say you need to transfer files from *dev2* to your computer (*comp*). In a pinch you could use `scp` twice to copy the files from *dev2* to *dev1* and then from *dev1* to *comp*. Alternatively, you could setup *dev1* as a proxy such that the files on *dev2* can be transferred directly to *comp*. To do this, on *comp* issue

```bash
orig@comp $ ssh -f -N -D 9001 user1@<dev1_ip>
```

Now *dev1* will be a proxy for *dev2*. Then follow the setups above to configure FileZilla to use the proxy with port 9001. Now you can connect to *dev2* at <dev2_ip> by configuring a typical FileZilla site. 

You can also use SFTP from *comp* to directly access *dev2* by issuing

```bash
$ sftp -o ProxyCommand='/usr/bin/nc -x 127.0.0.1:9001 %h %p' user2@<dev2_ip>

Connected to <dev2_ip>
sftp>  
```

Now use standard SFTP commands such as `cd`, `pwd`, `get`, and `put` to traverse the file system and transfer files
