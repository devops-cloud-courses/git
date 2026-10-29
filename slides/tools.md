## Git Power Tools

----

### Short Commit Hashes (`Short SHA-1`)

Display commit logs using abbreviated 7-character commit hashes:

```bash
git log --abbrev-commit
# or compact one-line view:
git log --oneline
```

----

### Viewing the Reflog (`git reflog`)

Your local safety net — records a chronological log of every movement of `HEAD` and branch tips (commits, checkouts, resets, rebases):

```bash
git reflog
```

> Even if a commit appears "lost" after a hard reset or rebase, you can almost always recover it via its reflog reference (e.g., `HEAD@{2}`).

----

### Relative Commit References (`HEAD~` & `HEAD^`)

Reference ancestor commits relative to `HEAD` (or any branch/tag name):

```bash
git show HEAD~1   # Parent of HEAD
git show HEAD~2   # Grandparent of HEAD
git show HEAD~4   # 4 commits before HEAD
```

----

### Selecting Commit Ranges

Inspect commits that exist in one branch but not another:

```bash
git log <from>..<to>

# Commits in your current branch not yet in main:
git log main..HEAD
```

----

### Interactive Staging (`git add -p`)

Stage individual hunks or lines of a modified file instead of the entire file at once — ideal for crafting small, atomic commits:

```bash
git add -p
# or full interactive menu:
git add -i
```

> Common patch keys: `y` (stage hunk), `n` (skip hunk), `s` (split into smaller hunks), `q` (quit).

----

### Stashing Work in Progress (`git stash`)

Temporarily shelve uncommitted changes so you can switch branches with a clean working directory:

```bash
git stash
# or with a descriptive label:
git stash push -m "WIP: refactor auth middleware"
```

----

### Listing Stashes

Inspect all saved stashes in your stack:

```bash
git stash list
```

----

### Restoring Stashed Work

```bash
# Apply latest stash and remove it from the stash stack
git stash pop

# Apply latest stash while keeping it in the stack
git stash apply

# Restore both working tree and previously staged state
git stash apply --index
```

----

### Dropping a Stash

Delete a specific stash entry when you no longer need it:

```bash
git stash drop <stash_id>

# Or clear all stashes at once:
git stash clear
```

----

### Cleaning Untracked Files (`git clean`)

Remove untracked files and directories from your working tree:

```bash
# Dry run first (preview what would be deleted):
git clean -n -d

# Force-delete untracked files and directories:
git clean -f -d
```

----

### Interactive Rebase (`git rebase -i`)

Clean up, reorder, reword, or squash local commits before opening a Pull Request:

```bash
git rebase -i HEAD~3
```

* **`reword` (`r`)** — Edit a commit message
* **`squash` (`s`) / `fixup` (`f`)** — Combine multiple small commits into a single cohesive commit
* **`drop` (`d`)** — Remove an unwanted commit from history
