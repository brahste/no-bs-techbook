# Setting up SSH SOCKS Tunnels

Resources: https://linuxize.com/post/how-to-setup-ssh-socks-tunnel-for-private-browsing/

Using an SSH SOCKS proxy tunnel allows you to route local traffic through an encrypted proxy. This lets any programs using the proxy to connect to the server which will then forward traffic to the intended destination IP.

## Creating the Tunnel with SSH

To create an SSH proxy tunnel run
```
ssh -f -N -D <port> <user>@<proxy-ip>
```

Here the option `-f` runs the command in the background so a terminal window isn't required to remain open for the tunnel to exist, `-N` tells SSH not to execute a remote command, `-D <port>` opens a SOCKS tunnel on the `<port>` provided (make sure to use a port number greater than 1024), and `<user>@<proxy-ip>` is the information of the proxy server. Optionally a `-p <port-ssh>` can be used if SSH is not running on the default port 22.

## Configuring an Application to Use the Proxy

Whether using Firefox, Google Chrome, FileZilla, or any other program, there is typically a way to configure the proxy settings. In the proxy settings page enter the loopback address (e.g. `127.0.0.1`) as the SOCKS 5 host and the `<port>` specified when the SSH proxy was initialized.
