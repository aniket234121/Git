# GIT

Git is a distributed version control system, which tracks changes in computer files, primarily used for coordinating development work by the programmers during software development process.

#### Meaning:

- It tracks every change you make to your project, so you can:

- go back to any old version

- see what changed

- who changed it

- when they changed it

- work on new features without breaking existing code

## Basics Git Commands

### 1. git init

git init initializes a new Git repository inside a folder.

It turns a normal folder into a version-controlled project by creating the hidden .git directory.

What Happens When You Run git init

Git creates:

```
.git/
 ├── HEAD
 ├── config
 ├── hooks/
 ├── objects/
 └── refs/

```

This folder stores:

- your commits

- branches

- history

- uconfiguration

**Without .git, Git cannot track anything.**

### Usage: -

#### Initialize in a folder

```git
git init        //initialize git in current folder
```

#### Initialize a repo with a specific default branch

```git
git init -b main      //Initialize a repo with a main branch
```

## **Git States**

Git tracks every file through four states:

1. Untracked

2. Unmodified

3. Modified

4. Staged

   ![alt text](image.png)

### 2. git add

git add moves changes from the Working **Directory → Staging Area**.

**stages everything**

    git add .

**stage a particular file**

    git add newfile.txt

**Stage only modified + deleted, not untracked**

    git add -u

**Stage all tracked files (modified + deleted), new untracked files**

    git add -A

### 3. git commit

git commit permanently saves the staged changes into the repository as a snapshot in time.

A commit contains:

- a unique hash

- author

- timestamp

- commit message

- the staged file snapshots

normal commit

    git commit -m "Add login validation"

Commit Skipping Staging (commit all tracked changes)

    git commit -am "Fixed bugs"

- -a only works for tracked files

- It does not add untracked files

Open the editor (default commit style)

    git commit

### 4. git log

git log shows the history of commits in your repository.

It displays:

- commit hash

- author

- date

- commit message

- optional refs (HEAD, tags, branches)

This is your timeline of the project.

    git log

Graph View (very useful for branches & merges)

    git log --oneline --graph --all

Show commits of a specific file

    git log file.js

Show author-specific commits

    git log --author="aniket"

### 5. git show

git show displays details about a specific object (usually a commit).

It shows:

- commit metadata

- commit message

- diff (changes made in that commit)

**Show the most recent commit**

    git show

Show a commit by its hash

    git show a1b2c3d    // git show <commit-hash>

output format: -

```
commit a1b2c3d
Author: Aniket <aniket@xyz.com>
Date:   Thu Dec 4 12:14 2025

    Fix: corrected API response type

diff --git a/app.js b/app.js
index 1234567..8910111 100644
--- a/app.js
+++ b/app.js
@@ -10,7 +10,7 @@ function getUser() {
-    return oldData;
+    return newData;
 }
```

## Backing out changes basics

### 1. BACK OUT UNCOMMITTED CHANGES (Working Directory)

These are edits you made but haven’t staged yet.
Discard changes in a single file

    git restore <file>
    git checkout -- <file> // old syntax
    git restore .          // Discard ALL uncommitted changes

### 2. BACK OUT STAGED CHANGES (Staging Area)

You ran git add, but NOT committed yet.

    git reset HEAD <filename>

**Unstage a file (keep changes in working directory)**

    git restore --staged <file>

**Unstage EVERYTHING**

    git restore --staged .

or backout after commit using git reset in later section

# Git alias

A Git alias is a shortcut command that you create to save time and avoid typing long or repetitive Git commands.

## WHERE ALIASES ARE STORED

Git aliases are stored inside your:

    ~/.gitconfig

Or inside a project’s local:

    .git/config

Global is recommended.

syntax: -

    git config --global alias.<shortcut> "<original command>"

## Access the alias config list

list all the config aliases

    git config --global --list

## Remove the alias

    git config --global --unset alias.<name>

## MOST USEFUL REAL-WORLD ALIASES

#### 1. Log (Pretty, one-line)

        git config --global alias.lg "log --oneline --graph --decorate --all"

#### 2. Add All

        git config --global alias.a "add -A"

#### 3. Commit with message

        git config --global alias.cm "commit -m"

#### 4. Undo last commit (keep changes)

        git config --global alias.uncommit "reset --soft HEAD~1"

## Rename file in git

Rename using Git command (recommended)

    git mv oldname.js newname.js

What happens?

- Git detects rename

- Git stages the rename automatically

- Old file is removed

- New file is added

- Ready for commit

OR

**Rename files manually (OS rename)**

You can rename using File Explorer or VS Code.

Example:

    Rename oldname.js → newname.js manually

Then tell Git:

    git add -A
    git commit -m "renamed"

## Deletion of file in git

Delete file using Git command (recommended)

    git rm filename.js

What happens?

- Deletes file from working directory

- Stages the deletion

- Ready to commit

same steps as Rename if deleted manually

## .gitignore

.gitignore tells Git:

“Do NOT track these files or folders.”

Anything listed inside .gitignore will:

- stay untracked

- never be staged

- never be committed

```
.env
secret.json
debug.log

// ignore by type of files
*.log
*.txt
*.zip
*.env

//Ignore by suffix
*.backup

//. Ignore by prefix
temp*
```
