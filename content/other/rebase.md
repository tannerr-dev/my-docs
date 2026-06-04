
https://git-scm.com/book/en/v2/Git-Branching-Rebasing

Git Rebase Command

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