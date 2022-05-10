# Managing Repositories with PPA
The Personal Package Archive (PPA) allows developers to distribute their own software via non-official repositories.

Information about your repositories are stored in the */etc/apt/sources.list* file and in the */etc/apt/sources.list.d* directory.

When you issue `sudo apt update` the repositories configured for your system will pull any versions that are available for update for the software you currently have installed. Then, issuing `sudo apt install <package>` will pull the newer version those packages from the repository URL and install the update.

You can add PPA repos to your *sources.list.d* directory, which enables the standard `apt` commands for custom (personal) repositiories.

**Example**
```bash
sudo add-apt-repository ppa:custom/repository_name
sudo apt update
audo apt install repository_name
```

The first command adds the repository information to the file */etc/apt/source.list.d/repository_name.list* (another backup file is also created with a *.save* suffix).

> Note: Typically you shouldn't mess with the */etc/apt/sources.list* file as this is the file that manages your Linux distribution's standard repositories.

### Tips
1. Use *synaptic* to search for files installed with PPA before deleting them

## PPA Purge
PPA Purge is a command line utility that removes a PPA repository from your software sources list and reverts your system back to official Ubuntu packages. This differs from simply deleting the PPA repo.

**Example**
```bash
sudo apt install ppa-purge
sudo ppa-purge ppa:repository-name
```

