# Multiple Git Accounts with SSH Keys

Links:
- freecodecamp.org/news/manage-multiple-github-accounts-the-ssh-way-2dadc30ccaca/

The basic steps in this process are to have SSH keys set up on for each of the users you want to be able to access different repositories, and then configure those SSH keys to point to the different git hosts.

1. Generate the SSH keys
2. Add the appropriate SSH keys to the GitHub/GitLab account
3. Register the SSH keys with the `ssh-agent`
4. Create the SSH configuration file `~/.ssh/config`
