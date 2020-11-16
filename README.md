# git-submodule-split
*Split a big project into submodules*

## Extracting Branches

Split a new branch from your history containing only the subtree rooted at a folder.

```bash
git subtree split -P [folder] -b [branch]
```

For each branch, create (empty) target repository, on GitHub or locally. Add those repos as remotes and push the branches to the `master` of them.

```bash
git init --bare [/tmp/remote.git]
git remote add [branch] [/tmp/remote.git]
git push [remote] [branch]:master
```

![](img/git-screenshot.png)

Clone those remotes to new places.

```bash
git clone [/tmp/remote.git] [new-folder]
cd [new-folder]
git remote set-url origin [url-to-new-remote]
```

Replace branches with submodules in the original repository.

```bash
git remote remove [remote]
git rm -r [folder]
git branch -D [branch]
git submodule add [url-to-new-remote]
git commit -m 'replaced [folder] with the submodule'
```

## More Info

- [Git Subtree](https://git-memo.readthedocs.io/en/latest/subtree.html)
- [Splitting a project sub-directory to a new Git repo](https://coderwall.com/p/a3a5xg/splitting-a-project-sub-directory-to-a-new-git-repo)
