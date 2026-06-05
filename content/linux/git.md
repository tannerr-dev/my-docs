# Git
## Set Up
changing git default interactive commit message editor
```bash
git config --global core.editor "vim"
git config --global core.editor "nvim"
```
Display current settings / config
```bash
git config --list
```
Set username for owner of commits
```bash
user.email=tannerr.dev@protonmail.com
user.name=Tanner Reyons
```
Cange default trunk branch name
```bash
git config --global init.defaultBranch "main"
```
Setting rebase to default on `git pull`
```
git config --global pull.rebase true
```

## Basic Git usage
```bash
git branch -m oldname newname
git log --oneline --graph --all

git cat-file -p <hash>
```
Setting up a GitHub remote repository
```bash
git remote get-url origin
git remote remove origin
git remote add <name> <uri>  //branch name?
git remote add origin https://github.com/<username>/<repo>.git
git push origin main
git push -u origin <branch>

```
Checking for updates from remote repository
```
git fetch
git push --set-upstream origin main
```
Close a remote branch
```
git clone -b <branch> <remote_repo>
```
## Merge conflicts
To resolve Git merge conflicts, here's what you need to do:

1. Open the conflicting file (`config.kbd`) in your text editor. You'll see sections that look like this:

```
<<<<<<< HEAD
your current version
=======
incoming changes
>>>>>>> dbc4cb3... commit message
```

1. For each conflict section:
   - Remove the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)
   - Choose which version you want to keep, or combine them if needed
   - Delete the unwanted version

2. After editing, save the file

3. Stage the resolved file:
```bash
git add config.kbd
```

1. Continue the rebase:
```bash
git rebase --continue
```

Would you like to show me the actual conflicts in your `config.kbd` file? I can help you decide which changes to keep.

If you want to see the full conflict markers:
```bash
git diff
```

Or if you want to see just the conflicting file:
```bash
cat config.kbd
```


https://git-scm.com/book/en/v2/Git-Branching-Rebasing

## Rebase 

To rebase a Git branch onto another branch, you can follow these steps:

1. **Switch to the Source Branch**: First, switch to the branch you want to rebase. For example, if you want to rebase `feature` onto `main`, you would run:
   ```bash
   git checkout feature
   ```
   

2. **Rebase onto Target Branch**: Then, rebase the current branch onto the target branch. You can do this by running:
   ```bash
   git rebase main
   ```
   Alternatively, you can specify both branches directly:
   ```bash
   git rebase main feature
   ```
   

3. **Resolve Conflicts**: If there are any conflicts during the rebase, Git will pause and allow you to resolve them. After resolving the conflicts, you need to add the resolved files and continue the rebase:
   ```bash
   git add <resolved files>
   git rebase --continue
   ```
   

4. **Push Changes**: After resolving any conflicts and completing the rebase, you may need to force push the changes if the branch has already been pushed to a remote repository:
   ```bash
   git push --force
   ```
   

Rebasing can help keep your branch history clean and linear, but it should be used with caution, especially when working with public branches or branches that have been shared with others. 

If you want to rebase a branch onto another branch while staying on the source branch, you can use the `--onto` flag or the `-` shorthand, which refers to the previous branch you were on:
```bash
git rebase --onto target_branch source_branch
```
or
```bash
git rebase -
```


Alternatively, you can use `git cherry-pick` to apply specific commits from one branch to another without rebasing the entire branch history. This method is useful if you only need to apply a single commit or a few specific commits. 

By following these steps, you can effectively rebase one branch onto another in Git. 

rebase on pull so their are no pointlyess merge commits

## .gitignore examples
```.gitignore
.pyc
__pycache__

tmp
.env
*/*.db
*/*.csv

data
TODO.md

public/d3.min.js
public/plot.min.js
public/modules/idb.js
```
