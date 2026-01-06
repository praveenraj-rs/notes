# Git Commands

All Commands

```
# Setup Config

ssh-keygen
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

git help
git config --global user.name "<username>"
git config --global user.email "<email>"
git config --global --edit


git init
git add <filename>
git restore --staged <filename>
git commit -m "commit message here"

git status
git diff
git diff --staged
git show <commitid>
git log
git log --oneline
git shortlog
git revert hashcode
 
git remote add origin URL
git remote -v
git remote set-url origin URL
git remote rm Name

git fetch
git pull
git push

git submodule add <URL> <path>
git submodule status
git submodule update --remote subModuleName


git branch
git branch newBranch
git checkout nexBranch
git checkout -
git checkout master
git merge newBranch
git push --set-upstream origin newBranch

git log --oneline
git reset <commitid>
git revert <commitid>

git reflog
git reset HEAD@{index} # magic time machine

git checkout [saved hash] -- path/to/file
git clean -d --force  #delete untracked files and directories

```

### ESS

```
git rm --cached 'fileName'
export GIT_EDITOR=vim
git show <commitid>

# Print object content
git cat-file -p <objectid>
git cat-file blob <objectid>

#show object type
git cat-file -t <objectid>
commit -> tree -> blob

# show object size
git cat-file -s <objectid>

```
## Help Git

```shell
git help --all
```

## Configure Git

```shell
git config --global user.name “<username>”
```

```shell
git config --global user.email “<email>”
```

Edit the Configuration

```shell
git config --global --edit
```

## Initialize Git

```shell
git init
```

## Add files

```shell
git add <filename>
```

## Undoing Add

Unstaging files (undoing git add)
Copies the last version of file.js from repo to index

```shell
git restore file.js
```

## Removes all untracked files

```
git clean -id
```

## Commit

Commits with a one-line message

```shell
git commit -m “Message”
```

## Revert

```
git revert HEAD~3
```

Revert the changes specified by the fourth last commit in HEAD and create a new commit with the reverted changes.

```
git revert -n master~5..master~2
```

Revert the changes done by commits from the fifth last commit in master (included) to the third last commit in master (included), but do not create any commit with the reverted changes. The revert only modifies the working tree and the index.

## Git Branch

Making a new Git Branch

```shell
git branch <name of branch>
```

Checking all available Branches

```shell
git branch
```

To create a new branch and switch to it

```
git branch newBranch
git checkout newBranch
```

Switching branches

```
git checkout nextBranch
```

Switching to the master branch

```
git checkout master
```

Merging the branches

```
git merge newBranch
```

Deleting the branch

```
git branch -d newBranch
```
