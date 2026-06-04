## Git

[[dev-notes]]
[[github]]


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


[[rebase]]

rebase on pull so their are no pointlyess merge commits

```
git config --list

user.email=tannerr.dev@protonmail.com
user.name=Tanner Reyons

```

```bash
git config --global core.editor "nvim"

git branch -m oldname newname
git config --global init.defaultBranch "main"
git log --oneline --graph --all

git cat-file -p <hash>

git remote get-url origin
git remote remove origin
git remote add <name> <uri>  //branch name?
git remote add origin https://github.com/<username>/<repo>.git
git push origin main
git push -u origin <branch>

git fetch
git push --set-upstream origin main


git config pull.rebase false
git config --global pull.rebase true
git config --global core.editor "vim"


git clone -b <branch> <remote_repo>

```

```bash

rm -rf go-vanillajs
git clone -b live https://github.com/firtman/go-vanillajs.git
cp /my-go-vanillajs/.env /go-vanillajs/.env

mkdir test
touch test/test.js
cd test

cd ..
rm -rf test
ls

```



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


