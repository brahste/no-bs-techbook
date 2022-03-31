# Setting up SSH Key Pairs

> Links:
> 
> - [Creating an SSH Key Pair for User Authentication](https://www.ssh.com/academy/ssh/keygen#creating-an-ssh-key-pair-for-user-authentication)
> 
> - [How To Configure SSH Key-Based Authentication on a Linux Server](https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server)

When working with a server or headless embedded device that you connect with over SSH it is often useful (and sometime nessecary) to setup SSH key pairs. SSH key pairs allow the SSH client (e.g. your device) to connect to the SSH server (e.g. the remote device) without having to issue a password for each new connection. Think of it as a literal *key* that allows you to unlock the remote connection without having to know the password.

> **Note:** Since SSH key pairs allow secure connections without a password, always make sure you only save the *public* key to the server, and don't ever give someone access to you *private* key.

## Creating an SSH Key Pair

On the client device (the one you use to connect to the server), create a new key pair.

```bash
$ ssh-keygen -t ed25519
```

If you already have a few SSH keys on your machine it can be helpful to save them to a different file and add a comment.

```bash
$ cd ~/.ssh
$ ssh-keygen -t ed25519 -f id_ed25519_foo -C <your>@<email.com>
```

> **Note:** Ensure that the files generated are saved in the *~/.ssh* directory.
> 
> **Note:** This process with create a two files: *id_ed25519_foo* and *id_ed25519_foo.pub*. The one with the *pub* extension is you public key.
> 
> **Note:** There are other algorithms that can be used to create the key. While *ed25519* is one of the most secure, it is not yet universally supported so if you're working with a legacy system you may want to use an algorithm like *rsa*.

Next, on the server, add the newly generated key to the file *~/.ssh/authorized_keys*. This can be done in a number of ways. Using the command line:

```bash
$ ssh <user>@<server_ip>
$ echo "<full_ssh_key>" >> ~/.ssh/authorized_keys
```
