# Multiple Identities

How to manage multiple identities (and SSH keys), for git commits, on a local machine.

Credit [Russell Brown](https://medium.com/@brownian) for the original article [How to Handle Multiple Git Accounts](https://medium.com/expedia-group-tech/how-to-handle-multiple-git-accounts-385afe430d5a).

In this setup, the following directory structure is used to manage different remotes in a user's `git` directory.

```text
git
├── github.com
|   ├── repo1
|   ├── repo2
|   └── repo3
├── personal-example.com
|   ├── repo1
|   ├── repo2
|   └── repo3
└── work-example.com
    ├── repo1
    ├── repo2
    └── repo3
```

1. Set up a default `~/.gitconfig` to manage the identities for the different directories.

```ini
[includeIf "gitdir:~/git/github.com"]
    path = ~/.gitconfig.github.com
[includeIf "gitdir:~/git/personal-example.com/"]
    path = ~/.gitconfig.personal-example.com
[includeIf "gitdir:~/git/work-example.com/"]
    path = ~/.gitconfig.work-example.com
```

1. Create a SSH key pair on the local machine for <github.com>.

   ```sh
   $ ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519-github.com
   Generating public/private ed25519 key pair.
   Enter passphrase (empty for no passphrase): 
   Enter same passphrase again: 
   Your identification has been saved in /c/Users/USERNAME/.ssh/id_ed25519-github.com
   Your public key has been saved in /c/Users/USERNAME/.ssh/id_ed25519-github.com.pub
   ```

1. Add the public key to the SSH agent.

   ```sh
   $ eval "$(ssh-agent -s)"
   Agent pid 2016
   $ ssh-add ~/.ssh/id_ed25519-github.com
   Identity added: /c/Users/USERNAME/.ssh/id_ed25519-github.com (USERNAME@HOSTNAME)
   ```

1. Add the public key to the SSH keys on <github.com>.

1. Set up a `~/.gitconfig-github.com` to manage the <github.com> identity.

```ini
[user]
    name = User Name
    email = 99999999+aaaaaa@users.noreply.github.com
[core]
    sshCommand = "ssh -i ~/.ssh/id_ed25519-github.com"
```

1. Repeat these steps to create keys and config for the other identities.
