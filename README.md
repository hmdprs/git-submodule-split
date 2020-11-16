# git-submodule-split
*Split a big project into submodules*

## Extracting Branches

Split a new branch from your history containing only the subtree rooted at a folder.

```bash
git subtree split -P [folder] -b [branch]
```

For each branch, create (empty) target remote repository, on GitHub or locally (like `/tmp/remote.git`). Add those remotes and push the branches to the `master` of them.

```bash
git init --bare [url-to-remote]
git remote add [remote] [url-to-remote]
git push [remote] [branch]:master
```

![](img/git-screenshot.png)

Clone those remotes to new places.

```bash
git clone [url-to-remote] [new-folder]
cd [new-folder]
git remote set-url origin [url-to-new-remote]
```

## Replace Branches with Submodules

```bash
git remote remove [remote]
git rm -r [folder]
git branch -D [branch]
git submodule add [url-to-new-remote]
git commit -m 'replaced [folder] with the submodule'
```

## Credit

- [Git Subtree](https://git-memo.readthedocs.io/en/latest/subtree.html)
- [Splitting a project sub-directory to a new Git repo](https://coderwall.com/p/a3a5xg/splitting-a-project-sub-directory-to-a-new-git-repo)
