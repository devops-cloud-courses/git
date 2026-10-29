## Branching & Merging

----

### How Branches Work: Commits & Trees

<img src="images/commit-and-tree.svg" alt="Commit and Tree" />

----

### How Branches Work: Commits & Parents

<img src="images/commits-and-parents.svg" alt="Commits and Parents" />

----

### How Branches Work: Lightweight Pointers

<img src="images/branch-and-history.svg" alt="Branch and History" />

----

### Default Branch & `HEAD`

* A Git branch is simply a lightweight, movable pointer to a commit
* The default branch is named `main`
* A special pointer called `HEAD` always points to your currently checked-out local branch

----

### Listing Branches

```bash
git branch
```

* Common options:
  * `-a` / `--all` — list both local and remote-tracking branches
  * `-v` — show the latest commit hash and subject on each branch

----

### Creating a New Branch

* Create a new branch pointer, or create and switch to it in one step:

```bash
# Create a branch pointer without switching
git branch <branch_name>

# Create a new branch and switch to it immediately
git switch -c <branch_name>
```

----

### Switching Branches (`git switch`)

Switch your working directory to an existing branch:

```bash
# Switch to an existing local branch
git switch <branch_name>

# Quick tip — toggle back to your previously checked-out branch
git switch -
```

----

### Merging a Branch

Integrate changes from another branch into your currently active branch:

```bash
git merge <branch_to_merge_from>
```

* Two merge strategies can occur:
  * **Fast-forward (`ff`)**: The target branch is a direct ancestor — Git simply moves the branch pointer forward (no merge commit needed)
  * **Three-way merge**: Both branches have diverged — Git creates a new **merge commit** combining both histories

----

### Resolving Merge Conflicts

When two branches modify the same lines of a file, Git pauses the merge and marks the conflict:

* Inspect conflicted files using `git status`
* Edit the files to resolve conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)
* Stage the resolved files (`git add <file>`) and complete the merge (`git commit`)

----

### Deleting a Local Branch

* Delete a local branch once your work is merged:

```bash
# Safely delete a branch whose changes are already merged
git branch -d <branch_name>

# Force-delete an unmerged branch
git branch -D <branch_name>
```
