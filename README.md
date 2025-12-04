# GIT
This repository contains structured notes and practical guidance for Git, ranging from basic commands to advanced workflows. It is designed to help both beginners and experienced developers understand and efficiently use Git in real projects.
## Basics
### - [GIT](./git.md#git)
  - [Meaning](./git.md#meaning)
  - [Basics Git Commands](./git.md#basics-git-commands)
    - [git init](./git.md#1-git-init)
    - [Git States](./git.md#git-states)
    - [git add](./git.md#2-git-add)
    - [List tracked files (git ls-files)](./git.md#get-list-of-files-tracking-by-git)
    - [git commit](./git.md#3-git-commit)
    - [git log](./git.md#4-git-log)
    - [git show](./git.md#5-git-show)

- [Backing Out Changes](./git.md#backing-out-changes-basics)
  - [Back out UNCOMMITTED changes](./git.md#1-back-out-uncommitted-changes-working-directory)
  - [Back out STAGED changes](./git.md#2-back-out-staged-changes-staging-area)

- [Git Alias](./git.md#git-alias)
  - [Where aliases are stored](./git.md#where-aliases-are-stored)
  - [Access alias config list](./git.md#access-the-alias-config-list)
  - [Remove alias](./git.md#remove-the-alias)
  - [Most useful aliases](./git.md#most-useful-real-world-aliases)

- [Rename File in Git](./git.md#rename-file-in-git)

- [Delete File in Git](./git.md#deletion-of-file-in-git)

- [.gitignore](./git.md#gitignore)
---
## Advanced
### - [Advanced Git](./gitAdvanced#advanced-git)

  - [Comparing Differences](./gitAdvanced#comparing-differences)
    - [Working Directory ↔ Staging Area](./gitAdvanced#1-compare-working-directory--staging-area)
    - [Staging Area ↔ Last Commit](./gitAdvanced#2-compare-staging-area--last-commit)
    - [Working Directory ↔ Last Commit](./gitAdvanced#3-compare-working-directory--last-commit-ignore-staging)
    - [Compare Two Commits](./gitAdvanced#4-compare-two-commits)
    - [Compare With Remote Branch](./gitAdvanced#5-compare-current-branch-with-remote-branch)

  - [git difftool](./gitAdvanced#git-difftool)

  - [Branching](./gitAdvanced#branching)
  
  - [Merge](./gitAdvanced#merge)
    - [Fast-Forward Merge](./gitAdvanced#1-fast-forward-merge-ff)
    - [3-Way Merge](./gitAdvanced#2-3-way-merge-merge-commit)
    - [Squash Merge](./gitAdvanced#3-squash-merge)
    - [Merge Conflicts](./gitAdvanced#merge-conflicts)
    - [Abort a Merge](./gitAdvanced#abort-a-merge)

  - [Tagging](./gitAdvanced#tagging)
    - [Lightweight Tag](./gitAdvanced#1️⃣-lightweight-tag)
    - [Annotated Tag](./gitAdvanced#️⃣-annotated-tag-recommended-for-releases)

  - [Stashing](./gitAdvanced#stashing)

  - [Git Time Travel](./gitAdvanced#git-time-travel)
    - [HEAD](./gitAdvanced#what-is-head)
    - [git reset](./gitAdvanced#git-reset--the-core-time-travel-command)
      - [reset --soft](./gitAdvanced#a-git-reset---soft)
      - [reset --mixed](./gitAdvanced#b-git-reset---mixed-default)
      - [reset --hard](./gitAdvanced#c-git-reset---hard-dangerous)
    - [git reflog](./gitAdvanced#git-reflog)
      - [Recover Lost Commits](./gitAdvanced#recover-lost-commits-with-reflog)
