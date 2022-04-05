# Using Update Alternatives

The `update-alternatives` command is useful when you want to support more than one version of a shared command.

It is typical for a Linux machine to use symbolic links to place programs in the *PATH* without having to create copies of the program.

---

**Example**

```bash
$ which ftp
/usr/bin/ftp
$ ls -l /usr/bin/ftp
rwxrwxrwx  1  root  root  21 B  <..date..>  ftp  ⇒ /etc/alternatives/ftp
$ ls -l /etc/alternatives/ftp
rwxrwxrwx  1  root  root  19 B  <..date..>  ftp  ⇒ /usr/bin/netkit-ftp
```

Here we see that when I call `ftp` I'm actually calling a double symbolic link through */etc/alternatives/ftp* (not in my *PATH*), back to the */usr/bin/netkit-ftp* (which is in my *PATH*). This redirection using symbolic links is what `update-alternatives` uses to manage multiple versions of the same command.

## Essential Usage

The essential usage of `update-alternatives` relies on three commands

`update-alternatives --install <link> <name> <path> <priority>`

`update-alternatives --list <name>`

`update-alternatives --config <name>`

- `<link>` is the location where you are placing the symbolic link the program. This link should point to somewhere in your *PATH* (preferably in */usr/local/bin*).

- `<name>` is the name given to the program. This should be the command line usage you're familiar with (e.g. `python`, `gcc`, etc.).

- `<path>` is the location of the altnerative you're specifying.

- `<priority>` is an arbitrary priority that determines which alternative is the default.

**Example**

Say you need to manage multiple versions of GCC and G++, in this case `update-alternatives` is a good solution.

First install all of the alternatives you may need.

```bash
$ sudo apt -y install gcc-7 g++-7 gcc-8 g++-8 gcc-9 g++-9
```

Next add these alternatives to the `update-alternatives` interface.

```bash
$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 7
$ sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-7 7
$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 8
$ sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-8 8
$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 9
$ sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-9 9
```

Next, list the alternatives with `--list` or switch between them with `--config`.

```bash
$ sudo update-alternatives --config gcc
There are 3 choices for the alternative gcc (providing /usr/bin/gcc).

  Selection    Path            Priority   Status
------------------------------------------------------------
  0            /usr/bin/gcc-9   9         auto mode
  1            /usr/bin/gcc-7   7         manual mode
* 2            /usr/bin/gcc-8   8         manual mode
  3            /usr/bin/gcc-9   9         manual mode
Press  to keep the current choice[*], or type selection number: 
```
































