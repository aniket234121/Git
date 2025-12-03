# Advanced Git

## comparing differences
When working with Git, you often need to compare changes between:

* Working directory vs staging area

* Staging area vs last commit

* Two commits

* Two branches

* A file across history

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