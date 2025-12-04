- [Advanced Git](#advanced-git)

  - [Comparing Differences](#comparing-differences)
    - [Working Directory ↔ Staging Area](#1-compare-working-directory--staging-area)
    - [Staging Area ↔ Last Commit](#2-compare-staging-area--last-commit)
    - [Working Directory ↔ Last Commit](#3-compare-working-directory--last-commit-ignore-staging)
    - [Compare Two Commits](#4-compare-two-commits)
    - [Compare With Remote Branch](#5-compare-current-branch-with-remote-branch)

  - [git difftool](#git-difftool)

  - [Branching](#branching)
  
  - [Merge](#merge)
    - [Fast-Forward Merge](#1-fast-forward-merge-ff)
    - [3-Way Merge](#2-3-way-merge-merge-commit)
    - [Squash Merge](#3-squash-merge)
    - [Merge Conflicts](#merge-conflicts)
    - [Abort a Merge](#abort-a-merge)

  - [Tagging](#tagging)
    - [Lightweight Tag](#1️⃣-lightweight-tag)
    - [Annotated Tag](#️⃣-annotated-tag-recommended-for-releases)

  - [Stashing](#stashing)

  - [Git Time Travel](#git-time-travel)
    - [HEAD](#what-is-head)
    - [git reset](#git-reset--the-core-time-travel-command)
      - [reset --soft](#a-git-reset---soft)
      - [reset --mixed](#b-git-reset---mixed-default)
      - [reset --hard](#c-git-reset---hard-dangerous)
    - [git reflog](#git-reflog)
      - [Recover Lost Commits](#recover-lost-commits-with-reflog)
---

# Advanced Git

## Comparing Differences

When working with Git, you often need to compare changes between:

- Working directory vs staging area

- Staging area vs last commit

- Two commits

- Two branches

- A file across history

### 1. Compare Working Directory ↔ Staging Area

Shows what you changed but haven’t staged yet.

    git diff

Use case:

You edited files but didn't run git add yet.

This shows differences between your working tree and the index (staging area).

### 2. Compare Staging Area ↔ Last Commit

Shows what you have staged to commit.

    git diff --staged

or

    git diff --cached

Use case:

See exactly what will be committed.

### 3. Compare Working Directory ↔ Last Commit (ignore staging)

    git diff HEAD

Use case:

Full diff of everything you changed since the last commit.

### 4. Compare Two Commits

    git diff <commit1> <commit2>

Example:

    git diff a12f3b7 9e2c1da

### 5. Compare Current Branch With Remote Branch

    git diff origin/main

## git difftool

git difftool is an alternative to git diff that lets you compare file changes using a GUI diff tool

(like VSCode, Meld, Beyond Compare, etc.).

same commands for difftool as diff

anything that can pass to diff can be passed to difftool

example: -

    git difftool <commit1> <commit2>
    git difftool origin/main

## Branching

A branch is simply a pointer to a commit.

- It moves forward automatically as you commit.

- It allows isolated development.

- It keeps your work separate from other features.

create branch

    git branch <branch-name>

switch to branch

    git checkout <branch-name>

create+ switch

    git checkout -b <branch-name>

list all branches

    git branch

list all branches local+remote

    git branch -a

rename branch

    git branch -m old-name new-name

delete branch

    git branch -d feature-auth

## Merge

git merge is used to combine changes from one branch into another.

You always merge into the branch you are currently on.

```
git switch main
git merge feature-auth
```

“Bring all commits from feature-auth → into main”.

### 1. Fast-Forward Merge (FF)

Happens when the target branch has NO new commits

Main branch didn’t move after you branched off.

```
main:    A—B—C
                \
feature:         D—E
```

Since main has no new commits → Git just moves main’s pointer forward.

### 2. 3-Way Merge (Merge Commit)

Happens when both branches added commits → histories diverged

```
         D—E (feature)
       /
A—B—C—F—G (main)

---after----merging----

        D—E
       /   \
A—B—C—F—G—(M)
```

### 3. Squash Merge

✔ All commits from the feature branch are combined into ONE commit

Commonly used in PRs on GitHub/GitLab.

```
git switch main
git merge --squash feature
git commit -m "Add feature"
```

Result:

Even if feature had 20 commits → only one commit is added to main.

Characteristics:

- Clean commit history

- All small messy commits squashed

- Feature branch is not marked as merged

- Requires manual commit after squashing

### Merge Conflicts

Conflicts occur when:

- both branches changed the same line

- or one deleted a file while the other modified it

```
    git merge feature-auth
```

If conflict occurs:

Git marks conflict in file:

```
<<<<<<< HEAD
main version
=======
feature version
>>>>>>> feature-auth
```

Resolve → save → add → commit:

#### Abort a Merge

If merge is messy and you want to cancel:

    git merge --abort

Returns repository to the pre-merge state.

### Tagging

Tags are labels you attach to specific commits.
They are used mainly for:

- Releases (v1.0.0, v2.5.1)

- Marking important points in history

Tags do not move like branches.
A tag always stays attached to the exact commit it was created on.

Types of Tags

#### 1️⃣ Lightweight Tag

- Just a pointer to a commit

- No message, no metadata

- Like a bookmark

Command:

    git tag v1.0.0

#### #️⃣ Annotated Tag (Recommended for releases)

- Stored as a full Git object

- Includes: tag message, author name, email, date

Command:

    git tag -a v1.0.0 -m "Release version 1.0.0"

### Stashing

git stash lets you temporarily save your uncommitted changes (both tracked AND optionally untracked files) without committing them.

It’s used when:

- You need to switch branches but don’t want to commit yet

- You want to save incomplete work

- You want to try something quickly without losing current changes

- Stashed changes go into a stack-like storage.

---

stash only tracked files

    git stash

Stash Untracked Files

- Untracked + tracked:

  git stash -u

List Stashes

    git stash list

Example output:

    stash@{0}: On main: WIP: login logic
    stash@{1}: On feature: UI changes

#### Apply Stash

    //(keep stash in list)

    git stash apply


    //or apply specific stash:

    git stash apply stash@{2}

#### Pop Stash

(apply + remove)

    git stash pop

#### Drop/Delete Stash

    git stash drop stash@{0}

Delete all:

    git stash clear

---

# Git Time Travel

Git gives you the power to travel back in time — undo commits, recover lost commits, restore deleted branches — without losing history (as long as reflog exists).

The two main tools:

- git reset → moves HEAD & optionally modifies your working directory

- git reflog → shows everything HEAD has ever pointed to (including deleted commits)

Combined: you can undo ANY mistake.

## What is HEAD?

HEAD = pointer to the current commit.

When you time-travel, you are moving HEAD.

## git reset — The Core “Time-Travel” Command

There are 3 types of reset, each more destructive depending on what it touches:

### A. git reset --soft

- Moves HEAD to an older commit
- Keeps staging area intact
- Keeps working directory intact

Use when:

You want to rewrite commit history but keep all your changes.

    git reset --soft HEAD~1

Undo last commit but changes remain staged.

### B. git reset --mixed (default)

- Moves HEAD
- Clears staging area
- Keeps working directory

Use when:

- You want to unstage files

- or undo commits but keep edits

example

    git reset HEAD~1

### C. git reset --hard (Dangerous)

- Moves HEAD
- Resets staging
- Resets working directory (deletes changes)

Everything becomes exactly like the target commit.

Example:

    git reset --hard HEAD~1

Deletes last commit AND all changes.

**Important:You can recover it using reflog (if not garbage-collected).**

## Git Reflog

git reflog records every move HEAD has ever made, including:

- checkout

- reset

- commit

- merge

- rebase

- branch delete

- stash apply/pop

view reflog

    git reflog

output:

    0a1b2c3 (HEAD -> main) HEAD@{0}: commit: Fix bug
    7x8y9z1 HEAD@{1}: reset: moving to HEAD~1
    1f2e3d4 HEAD@{2}: checkout: moving from feature to main

Every entry is recoverable.

---

### Recover Lost Commits with Reflog

#### Imagine you ran:

    git reset --hard HEAD~5

**Lost commits?**

- NO — reflog can restore them.

Steps:

- View reflog

```
git reflog
```

Find the commit you want

Example: abc1234

Reset back to it

    git reset --hard abc1234

Boom → commit fully recovered.
