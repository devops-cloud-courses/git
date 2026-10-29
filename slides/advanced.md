## Advanced Git

----

### Initializing a New Repository

Turn an existing local directory into a new Git repository (creates the `.git` folder):

```bash
git init
```

----

### Inspecting Line-by-Line History (`git blame`)

See who last modified each line of a file, when, and in which commit:

```bash
git blame <file_name>
```

----

### Amending the Last Commit

Update the most recent commit (fix a typo in the commit message or include forgotten staged changes):

```bash
git commit --amend
```

> **Warning:** `git commit --amend` rewrites commit history (creating a new SHA hash). Avoid amending commits that have already been pushed to shared branches.

----

### Listing Tags

Tags mark specific points in history as important (typically release versions like `v1.4.0`):

```bash
# List all tags
git tag

# Filter tags matching a pattern (e.g., all v1.* releases)
git tag -l "v1*"
```

----

### Creating a Tag

* **Annotated tag** *(recommended for releases)* — stores tagger identity, date, message, and signature
* **Lightweight tag** — a simple static pointer to a commit

```bash
# Annotated tag (full Git object)
git tag -a v1.4.0 -m "Release version 1.4.0"

# Lightweight tag
git tag v1.4.0-lw
```

----

### Inspecting a Tag

Display the tag metadata along with the commit and diff it points to:

```bash
git show <tag_name>
```

----

### Pushing Tags to a Remote

By default, `git push` does not transfer tags. Push them explicitly:

```bash
# Push a single tag
git push origin <tag_name>

# Push all local tags
git push origin --tags
```

----

### Deleting a Tag

```bash
# Delete a local tag
git tag -d <tag_name>

# Delete a remote tag
git push origin --delete <tag_name>
```

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

### Rebasing a Branch

Replay the commits of your feature branch on top of the latest target branch:

```bash
git switch <branch_to_rebase>
git rebase <base_branch>
```

----

### Rebase: Pros & Golden Rule

* **Advantages**:
  * Produces a clean, linear commit history free of unnecessary merge commits
  * Makes `git log` and `git bisect` much easier to read and navigate
  * Keeps feature branches up to date with `main` before opening a Pull Request
* **The Golden Rule of Rebasing**:
  * **Never rebase commits that are shared on a public branch** used by other teammates

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

### DevSecOps: Commit Signing (`SSH` / `GPG`)

Anyone can set `git config user.email` to impersonate an author. **Cryptographic commit signing** proves your identity (`Verified` badge on GitHub/GitLab):

```bash
# Sign commits using your SSH key (Git 2.34+)
git config --global gpg.format ssh
git config --global user.signingkey ~/.ssh/id_ed25519.pub
git config --global commit.gpgsign true
```

----

### DevSecOps: Git Hooks & Secret Scanning

* **Never commit secrets** (`.env`, cloud API keys, private certs, database passwords)
* Deleting a leaked secret in a later commit **does not remove it from `.git` history** — bots scan public commits in seconds!
* Use [`pre-commit`](https://pre-commit.com/) hooks (`gitleaks`, `trufflehog`, linters) to block secrets **before** a commit is created:

```bash
# Install git hooks defined in .pre-commit-config.yaml
pre-commit install
```
