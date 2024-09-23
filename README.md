# Git

Useful Git commands and concepts.

## See also

* [Multiple identities](./docs/multiple-identities.md).
* [Private remotes](./docs/private-remotes.md).

## Branch

Rename branch.

1. Local.

   ```sh
   git checkout old-name
   git branch -m new-name
   ```

1. Remote.

   ```sh
   git push origin :old-name new-name
   git push origin -u new-name
   ```

## Rebase

Change committer without changing commit or author dates. This could be cleaner but it works!

```sh
git rebase -i --root --committer-date-is-author-date -x 'GIT_COMMITTER_DATE="$(git log -n 1 --format=%aD)" git commit --amend --reset-author --no-edit --date="$(git log -n 1 --format=%aD)"'
```
