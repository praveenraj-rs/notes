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

Great question 👍 — this is a **very professional habit** to build early.

Below are **best practices + ready-to-use commit messages** specifically for **your encoder work**.

---

## ✅ General Rules for a Good Commit Message

### 1️⃣ Use **imperative mood**

Think: _“This commit will …”_

❌ `Added encoder code`  
✅ `Add TIM1 quadrature encoder support`

---

### 2️⃣ Keep subject ≤ **50 characters**

Short, clear, searchable.

---

### 3️⃣ Explain **why**, not just what

Code shows _what_, commit message explains _why_.

---

### 4️⃣ One logical change per commit

Your change = encoder feature → one commit ✔

---

## 🔷 Recommended Commit Message Format

```
<type>: <short summary>

<optional detailed explanation>
```

---

## 🔷 Suggested Types (Common Convention)

|Type|Use when|
|---|---|
|feat|New feature|
|fix|Bug fix|
|refactor|Code structure change|
|docs|Comments / documentation|
|test|Tests added|
|chore|Cleanup / build changes|

---

## 🟢 BEST COMMIT MESSAGE FOR YOUR CASE (Recommended)

### ✔ If this is a **new feature**

```
feat: add TIM1 quadrature encoder interface (X4)

Configure TIM1 in encoder mode 3 with GPIO AF setup,
input filtering, and software scaling for KY-040 encoder.
Includes detailed register-level comments for future reference.
```

---

## 🟡 If main change is **documentation/comments**

```
docs: add detailed comments for STM32 encoder interface

Explain TIM1 encoder mode selection, CC/TI mapping,
input polarity, filtering, and X4 decoding behavior.
```

---

## 🔵 If this is part of learning / experimentation repo

```
feat: implement rotary encoder using TIM1 encoder mode

Use hardware quadrature decoding with X4 resolution
and debounce filtering for KY-040 mechanical encoder.
```

---

## 🔴 If this is a refactor of earlier code

```
refactor: clean up TIM1 encoder initialization

Reorganize GPIO and timer setup and add comprehensive
comments explaining encoder hardware behavior.
```

---

## 🔑 Ultra-Short Version (Still Acceptable)

```
feat: TIM1 quadrature encoder (X4, KY-040)
```

---

## 🚫 Avoid These Commit Messages

❌ `encoder working`  
❌ `final code`  
❌ `updated`  
❌ `changes done`

These give **zero context** later.

---

## 🧠 Pro Tip (Very Important)

Imagine **6 months later**, you ask:

> “Why did I change this?”

A good commit message should answer that **without opening the code**.

---

## ✅ My Strong Recommendation (Use This)

If I were reviewing your repo, I’d want to see:

```
feat: add TIM1 quadrature encoder interface (X4)

Hardware-based quadrature decoding using STM32 TIM1
encoder mode 3 with strong input filtering for KY-040.
Includes register-level documentation and software
scaling for logical step control.
```

---

If you want, I can also help you:

- 📌 Split this into **multiple clean commits**
    
- 🧾 Write **GitHub PR description**
    
- 🧠 Create **commit message template**
    
- 🏷 Tag releases professionally
    

Just say 👍


```
feat: add ADC_CH0 POT interface (PA0)

Potentiometer (10kohm) interfacing adc code with 480 sampling cycle.
```