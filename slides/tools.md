## Git Power Tools & DevSecOps

----

### Interactive Patch Mode (`-p` / `--patch`)

Stage, unstage, or discard individual **hunks** of a file instead of the whole file at once — ideal for crafting small, atomic commits:

```bash
git add -p <file>       # Interactively stage selected hunks
git restore -p <file>   # Interactively discard selected hunks
```

> Common patch keys: `y` (apply hunk), `n` (skip hunk), `s` (split into smaller hunks), `q` (quit).

----

### Stashing Work in Progress (`git stash`)

Temporarily shelve uncommitted changes so you can switch branches with a clean working directory:

```bash
# Push uncommitted changes onto the stash stack
git stash push -m "WIP: refactor auth middleware"

# Inspect all saved stashes in your stack
git stash list
```

----

### Restoring & Dropping Stashes

```bash
# Apply latest stash and remove it from the stash stack
git stash pop

# Apply latest stash while keeping it in the stack
git stash apply

# Delete a specific stash entry (or clear all with git stash clear)
git stash drop <stash_id>
```

----

### Cleaning Untracked Files (`git clean`)

Remove untracked build artifacts, temporary files, and directories from your working tree:

```bash
# Dry run first (preview what would be deleted):
git clean -n -d

# Force-delete untracked files and directories:
git clean -f -d
```

----

### Parallel Working Directories (`git worktree`)

Check out multiple branches simultaneously in separate folders — no need to `git stash` or clone the repository twice:

```bash
# Create a second working directory checked out on a hotfix branch
git worktree add ../project-hotfix -b hotfix/login-bug main

# List or clean up active worktrees
git worktree list
git worktree remove ../project-hotfix
```

----

### Inspecting Line-by-Line History (`git blame`)

See who last modified each line of a file, when, and in which commit:

```bash
git blame <file_name>

# Restrict blame to a specific line range (e.g., lines 40 to 60)
git blame -L 40,60 <file_name>
```

----

### Binary Search Debugging (`git bisect`)

Pinpoint the exact commit that introduced a regression across hundreds of commits in `O(log N)` steps:

```bash
git bisect start
git bisect bad                 # Current commit is broken
git bisect good v1.2.0         # Last known working tag/commit

# Automate verification using any test command or script:
git bisect run npm test
git bisect reset               # Return to original HEAD when done
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
