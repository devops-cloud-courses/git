## Advanced Git

----

### Listing & Creating Tags

* **Annotated tag** *(recommended for releases)* — stores tagger identity, date, message, and signature
* **Lightweight tag** — a simple static pointer to a commit

```bash
# List all tags (or filter with -l "v1*")
git tag

# Create an annotated release tag vs. a lightweight tag
git tag -a v1.4.0 -m "Release version 1.4.0"
git tag v1.4.0-lw
```

----

### Inspecting, Pushing & Deleting Tags

By default, `git push` does not transfer tags — push them explicitly:

```bash
# Inspect tag metadata and commit diff
git show v1.4.0

# Push a single tag (or all local tags with --tags)
git push origin v1.4.0

# Delete a tag locally and on the remote
git tag -d v1.4.0 && git push origin --delete v1.4.0
```

----

### Relative Commit References & Ranges

Reference ancestor commits relative to `HEAD` or compare commits between branches:

```bash
git show HEAD~1        # 1 commit before HEAD (parent)
git show HEAD~3        # 3 commits before HEAD

# Show commits in your current branch not yet merged into main:
git log main..HEAD
```

----

### Amending the Last Commit

Update the most recent commit (fix a typo in the commit message or include forgotten staged changes):

```bash
git commit --amend
```

> **Warning:** `git commit --amend` rewrites commit history (creating a new SHA hash). Avoid amending commits that have already been pushed to shared branches.

----

### Rebase (1): Diverged History

<img src="images/basic-rebase-1.svg" alt="Rebase Step 1" />

----

### Rebase (2): Replaying Commits

<img src="images/basic-rebase-3.svg" alt="Rebase Step 2" />

----

### Rebase (3): Fast-Forward Target

<img src="images/basic-rebase-4.svg" alt="Rebase Step 3" />

----

### Rebasing a Branch (`git rebase`)

Replay the commits of your feature branch on top of the latest target branch:

```bash
git switch <branch_to_rebase>
git rebase <base_branch>
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

----

### Rebase: Pros & Golden Rule

* **Advantages**:
  * Produces a clean, linear commit history free of unnecessary merge commits
  * Makes `git log` and `git bisect` much easier to read and navigate
  * Keeps feature branches up to date with `main` before opening a Pull Request
* **The Golden Rule of Rebasing**:
  * **Never rebase commits that are shared on a public branch** used by other teammates

----

### Safe Force-Pushing (`--force-with-lease`)

After rebasing or amending a feature branch that was already pushed to a Pull Request, update your remote branch safely:

```bash
# Safe: fails if a teammate pushed new commits you haven't fetched yet
git push --force-with-lease

# Dangerous: blindly overwrites remote branch history
git push --force
```

> **Best Practice:** Always prefer `--force-with-lease` over `--force` on feature branches, and never force-push to `main`.

----

### Undoing Commits: `git reset` vs. `git revert`

<img src="images/reset-vs-revert.svg" alt="git reset vs git revert" />

----

### `git reset`: Modes Across the Three Areas

Move the current branch pointer backward (e.g., `git reset <mode> HEAD~1`):

| Mode | `.git (HEAD)` | `Staging Area (Index)` | `Working Directory` | Typical Use Case |
|---|---|---|---|---|
| `--soft` | Moves back | **Kept** (all changes staged) | **Kept** | Squash or recommit recent local commits |
| `--mixed` *(default)* | Moves back | Reset to target | **Kept** (unstaged) | Unstage changes and rework files before committing |
| `--hard` | Moves back | Reset to target | **Overwritten (!)** | Completely discard broken local commits and edits |

----

### Safe Undo on Shared Branches (`git revert`)

To undo a commit that has **already been pushed** to `main` without rewriting history, create a new commit that applies the exact inverse diff:

```bash
# Create a new commit that reverses <commit_sha>
git revert <commit_sha>
```

* Preserves full Git audit history and never breaks teammates' local repositories

----

### Surgical Backporting (`git cherry-pick`)

Copy a specific commit from one branch and apply it onto your current branch (e.g., backporting a hotfix to a release or `support/*` branch):

```bash
# Switch to target branch and apply a single commit
git switch release/v1.2
git cherry-pick <commit_sha>
```

----

### Recovering "Lost" Commits (`git reflog`)

Your local safety net — records a chronological log of every movement of `HEAD` and branch tips (commits, checkouts, resets, rebases):

```bash
git reflog
```

> Even if a commit appears "lost" after a `git reset --hard` or a bad rebase, you can recover it via its reflog reference (`git switch -c recovery HEAD@{2}`).
