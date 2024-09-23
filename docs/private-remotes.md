# Private Remotes

How to set up a Git on a remote server and clone it through SSH to a local machine.

## On the remote server

1. Create a developer group for developers to access.

   ```sh
   sudo groupadd dev
   ```

1. Add developer users to the group.

   ```sh
   sudo usermod -aGdev USERNAME
   ```

1. Create the Git directory.

   ```sh
   sudo mkdir -p /srv/git
   ```

1. Change the group.

   ```sh
   sudo chgrp dev /srv/git
   ```

1. Create a repository.

   ```sh
   git init --bare --shared /srv/git/test.git
   ```

## On the local machine

1. Clone the repository.

   ```sh
   git clone USERNAME@HOSTNAME:/srv/git/test.git
   ```
