# Git Tutorial

Watch my [YouTube tutorial]() for a comprehensive guide to using `git`. This cheatsheet contains all the commands covered in the video for quick reference.

It’s important to note that while this list summarizes the commands, the video covers many underlying concepts in detail, so make sure to watch it for a full understanding.

## Prerequisites

This is a beginner-friendly course with minimal prerequisites. All you need is a basic understanding of Linux commands and a passion for learning!

## Installing Git

To install Git, visit the [official Git website](https://git-scm.com/download) and follow the instructions for your operating system. It's available for Windows, macOS, and Linux.

## General good to know commands

```bash
watch -n .5 tree .git
```

Repeatedly runs the `tree .git` command every 0.5 seconds. Here's a breakdown of each part:

- **`watch`**: This is a command that repeatedly runs another command and displays the output in the terminal.
- **`-n .5`**: This option specifies the interval in seconds between command executions. In this case, `.5` means the command will run every 0.5 seconds (half a second).
- **`tree .git`**: This command displays the directory structure of the `.git` folder in a tree-like format, showing all files and subdirectories inside the `.git` directory, which contains the Git metadata for the repository.

## Git Commands

## Check the Status of Your Git Project

```bash
git status
git status -s
```

- **`git status`**: Displays the state of your working directory and staging area.
- **`git status -s` (or `--short`)**: Simplified, short-format output.

### Output Legend

- `M  file.txt`: File modified, not yet staged.
- `A  newfile.txt`: Newly added file, staged for commit.
- `D  oldfile.txt`: Deleted file, staged for commit.
- `??  untrackedfile.txt`: Untracked file, not added to staging area.

---

## Add Files to the Staging Area

```bash
git add .              # Add all files
git add file1          # Add a single file
git add file1 file2    # Add multiple files
```

---

## Unstage Files

```bash
git reset file1        # Unstage a specific file
git reset              # Unstage all files
```

- **`git reset`**: Removes files from the staging area without affecting your working directory changes.

---

## Remove Files from Git

```bash
git rm --cached file1    # Remove file from staging area only (untrack it)
git rm file1             # Remove file from both working directory and Git
```

- **`git rm --cached`**: Stops tracking the file but keeps it locally.
- **`git rm`**: Deletes the file from both the working directory and staging area.

---

## Commit Changes

```bash
git commit -m "Your commit message"
```

- **`git commit`**: Records a snapshot of the changes in the staging area.

---

## View Commit Logs

```bash
git log
```

- **`git log`**: Shows a history of commits.

### View Diffs with Commits

```bash
git log -p
```

- **`-p` stands for "patch"**: Displays commit history along with the differences (or patch) introduced by each commit.

---

## Show the Difference Between States

**View changes between your working directory and the staging area:**

```bash
git diff
```

**View changes between the staging area and the most recent commit:**

```bash
git diff --staged
```

**Compare two specific commits:**

```bash
git diff commit1 commit2
```

**Compare two branches:**

```bash
git diff branch1 branch2
```

---

## Show Changes for a Specific Commit

```bash
git show <commit-sha>
```

- **`git show`**: Displays details and the diff for a single commit. Useful for inspecting what was changed in a particular commit.

---

## Restore Files

```bash
git restore --staged file1   # Unstage a file but keep changes
git restore file1            # Discard local changes
```

## Tagging

**View all tags:**

```bash
git tag
```

**Create an annotated tag:**

```bash
git tag -a v1.0 -m "Release version 1.0"
```

---

## Checkout Commands

**Checkout a specific tag or commit:**

```bash
git checkout <tag-or-commit-sha>
```

- **Warning**: This puts you in a **detached HEAD** state, meaning any changes you make won't affect any branch unless you create a new branch from that commit/tag.

**Switch back to the previous branch:**

```bash
git switch -
```

---

## Branching Commands

**Create and switch to a new branch:**

```bash
git checkout -b new-branch
```

**Delete a branch:**

```bash
git branch -d old-branch       # Delete safely if merged
git branch -D old-branch       # Force delete if not merged
```

---

## Reset vs. Remove

- **`git reset <file>`**

  - Removes the file from the staging area, but keeps it in the working directory.
  - Use this when you mistakenly added a file to the staging area and want to unstage it.

- **`git rm <file>`**

  - Removes the file from both the staging area **and** the working directory.
  - Use this when you want to delete the file from the repository and the local filesystem.

---

## View Commit Tree

```bash
tree .git/objects
```

- **`tree`**: Shows the internal structure of your `.git` directory, displaying how Git stores commits.

---

### Branch Management

```bash
git branch issue-123
git checkout issue-1234
git checkout -b issue-123
```

- **Creating and switching branches**:

  - If you create a new branch and switch to it, everything should work fine.
  - If you try to switch to an existing branch, Git will prompt you to either commit or stash your changes before switching, as they could be overwritten by the branch you're checking out.

### Stashing Changes

```bash
git stash
```

- **`stash`**: Temporarily saves changes that you don't want to commit yet. Think of it as a clipboard where you can stash your changes and apply them later.

- **Important**: It's a good practice to have a clean working tree before switching branches.

### Advanced Checkout

```bash
git checkout -b branch_name <pointer location>  # Could be HEAD, a commit hash, or the name of another branch
git checkout -B issue-126 master
```

- **`-b`**: Creates and switches to a new branch.
- **`-B`**: Resets an existing branch to the specified location (e.g., `master` or a commit hash).

### Viewing Logs

```bash
git log --graph
```

- **`log --graph`**: Shows a visual representation of the commit history, displaying the branching and merging history.
- **Commits**: Each commit represents a snapshot of your repository at a given time.

### Viewing Differences

```bash
git log -p
git diff <commit1> <commit2>
```

- **`log -p`**: Displays the changes made in each commit.
- **`diff`**: Compares differences between two commits, branches, or files.

```bash
git show <commit_hash>
```

- **`show`**: Displays details of the current commit or a specific commit if a hash is provided.

### Diff Context

- **Blank lines in diffs**: These are lines of context that help you and diff tools understand where changes fit in a file.
- **Diff symbols**:
  - `+` indicates added lines.
  - `-` indicates removed lines.

---

### Fast-Forward Merges

```bash
git merge branch_name
```

- **Fast-Forward Merge**: Moves your current branch forward to match another branch, but only if there are no divergent changes.

```bash
git merge --ff-only issue-126
```

- **`--ff-only`**: Ensures that only fast-forward merges are allowed. If branches are not compatible for a fast-forward merge, it won't proceed.

- **Conflict Markers**: If there are merge conflicts, Git adds markers in the conflicting files. After resolving, you must stage the files and commit again to complete the merge.

### Merging

- If a fast-forward merge is not possible, Git will perform a **recursive merge**, which creates a new commit to fold together different lines of development.

---

### Handy `checkout` commands

```bash
git checkout -
git checkout -- file
```

- **`checkout -`**: Switches back to the previous branch you were on.
- **checkout --**: When combined with the -- option, it focuses specifically on files. It reverts the file to its last committed state, essentially undoing any modifications made since the last commit.

---

### Three-way Merges

A **three-way merge** in Git (and by extension, GitHub) is a method used to resolve differences between two branches when merging them. It involves three commits:

1. **The common ancestor commit**: This is the last commit that both branches share, before they diverged.
2. **The "current" branch (usually the branch you're on)**: This is the branch where you're merging changes into.
3. **The "other" branch (the branch being merged)**: This is the branch you're trying to merge into the current branch.

#### How it works:

1. **Identify the common ancestor**: Git looks for the latest commit that both branches have in common. This commit serves as the base for the merge.
2. **Compare changes**:
   - Git compares the common ancestor to the changes in the current branch.
   - Git compares the common ancestor to the changes in the other branch.
3. **Resolve conflicts**:
   - If there are differences in both branches that don’t conflict, Git merges them automatically.
   - If there are conflicts (i.e., the same line or part of the file is modified differently in both branches), Git will pause and ask you to manually resolve the conflicts.

#### Visualization

Imagine you have two branches: `main` and `feature`:

```text
       o---o---B  (main)
      /
 A---o---o---C  (feature)
```

- **A**: The common ancestor.
- **B**: The latest commit on `main`.
- **C**: The latest commit on `feature`.

In a three-way merge:

- Git compares `A` (the common ancestor) with `B` (the latest commit on `main`), and then compares `A` with `C` (the latest commit on `feature`).
- It tries to merge the differences from `C` into `B` based on the changes relative to `A`.

If all changes are non-conflicting, the merge happens automatically, producing a new merge commit.

---

### Undoing a Merge

If you accidentally merged a branch and want to undo the merge, you can use:

```bash
git merge --abort
```

If the merge is not yet completed, this will abort the merge process and revert to the pre-merge state. If the merge was completed and you want to undo it:

```bash
  git reset --hard <commit-before-merge>
```

---

It seems like you're summarizing and making notes on Git concepts related to remotes, upstream, fetch, pull, and branch management. Here's a refined version of those notes for better understanding:

---

### Amend Commits

1. **`git commit --amend`:**

   - **Amending the Last Commit**:
     - If you need to change something in your last commit (e.g., add or modify files, update the commit message), `git commit --amend` lets you "redo" the commit.
     - **Important**: The commit hash will change, meaning it rewrites history.

   ```bash
   git commit --amend
   ```

2. **Pushing Amended Commits:**

   - **Problem**: If the commit you're amending has already been pushed to a remote (like GitHub), and you rewrite history with `amend`, you won’t be able to push normally because the remote will reject the changes due to diverging history.
   - **Solution**: You would need to use `git push --force` to overwrite the remote branch with your local changes.
     - **Warning**: Force pushing is risky as it rewrites the remote history, which can cause issues for collaborators.

   ```bash
   git push --force
   ```

3. **Amending to Include Missing Files:**

   - If you forgot to include certain files in the last commit, you can simply stage them and run `git commit --amend`. This will create a new commit that includes the additional files.

   ```bash
   git add <forgotten-file>
   git commit --amend
   ```

4. **Amending Without Changing the Commit Message:**

   - Use the `--no-edit` flag to amend the last commit but keep the original commit message. This is useful when you only want to add more files to the commit without changing the message.

   ```bash
   git commit --amend --no-edit
   ```

---

### Rebasing and Fast-Forward Merges

1. **Rebasing to Keep History Clean:**

   - **Scenario**: Let’s say the `master` (or `main`) branch in the upstream repository has new commits that you want to integrate into your feature branch before merging it.
   - Instead of merging, you can use **rebasing** to "replay" your changes on top of the updated `master`. This makes your branch's history linear, and when you merge, it will be a **fast-forward merge** (cleaner commit history).

   ```bash
   git fetch upstream
   git rebase master
   ```

2. **Rebasing Steps:**

   - **`git rebase master`** calculates the difference between your branch and `master` and replays your commits on top of `master`.
   - If there are conflicts during the rebase, it will pause, and you will need to resolve them manually.

3. **Handling Merge Conflicts During Rebase:**

   - If a rebase encounters conflicts, it will stop, and you’ll have to resolve those conflicts.
   - After resolving conflicts, run `git rebase --continue` to proceed with the rebase.
   - If the conflicts are too complex or you want to back out, you can abort the rebase with `git rebase --abort`.

   ```bash
   git rebase --abort      # Abort the rebase if things go wrong
   git rebase --continue   # Continue after resolving conflicts
   ```

4. **Force Pushing After a Rebase:**

   - After a successful rebase, the branch history is rewritten. Therefore, if you've already pushed your branch, you'll need to force push (`git push --force`) to update the remote repository with your rebased history.
     - **Again, be cautious** when force pushing, especially if others are working on the same branch.

   ```bash
   git push --force
   ```

---

### Interactive Rebase

1. **Interactive Rebasing:**

   - Running `git rebase master -i` initiates an **interactive rebase**, which allows you to pick, squash, reorder, or drop commits interactively.
   - **Squash** combines two or more commits into one, making your commit history more concise.

   ```bash
   git rebase master -i
   ```

2. **Best Practices with Rebasing:**
   - **Do not rebase on shared branches or `master`**: Rebasing rewrites history, so avoid using it on branches that others are working on.
   - Rebase your **feature branch** instead to keep its history clean and linear before merging.
