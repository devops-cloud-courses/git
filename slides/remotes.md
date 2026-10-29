## Working with Remotes

----

### Listing & Inspecting Remotes

* View configured remote aliases (such as `origin` or `upstream`) and their details:

```bash
# List remote names and their fetch/push URLs
git remote -v

# View detailed info about a remote (URL, tracked branches, HEAD)
git remote show <remote_name>
```

----

### Adding, Renaming & Removing Remotes

```bash
# Register a new remote repository
git remote add <remote_name> <url>

# Rename or remove an existing remote alias
git remote rename <old_name> <new_name>
git remote remove <remote_name>
```

----

### Authentication: HTTPS vs. SSH Keys

* **HTTPS** (`https://github.com/org/repo.git`) — authenticates via Personal Access Tokens (`PAT`) or OAuth credential helpers
* **SSH** (`git@github.com:org/repo.git`) — industry standard for developers and CI runners using `Ed25519` cryptographic key pairs:

```bash
# Generate a modern Ed25519 SSH key pair
ssh-keygen -t ed25519 -C "jane.doe@example.com"

# Copy your public key to GitHub / GitLab Settings -> SSH Keys
cat ~/.ssh/id_ed25519.pub
```

----

### Remote-Tracking Branches (1): Initial Clone

<img src="images/remote-branches-1.svg" alt="Remote Branches 1" />

----

### Remote-Tracking Branches (2): Diverged Work

<img src="images/remote-branches-2.svg" alt="Remote Branches 2" />

----

### Fetching Changes (`git fetch`)

Download new commits, files, and refs from a remote repository into your local database:

```bash
git fetch <remote_name>
```

> `git fetch` only updates remote-tracking pointers (like `origin/main`) — it **never modifies** your local working directory or merges automatically.

----

### Remote-Tracking Branches (3): After `git fetch`

<img src="images/remote-branches-3.svg" alt="Remote Branches 3" />

----

### Pulling Changes (`fetch` + `merge`)

Download the latest changes from the tracked remote branch and integrate them into your current local branch:

```bash
git pull <remote_name> <branch>
```

* Use `git pull --rebase` to replay your local commits on top of the upstream changes instead of creating a merge commit.

----

### Pushing Changes to a Remote

Publish your local commits to a remote repository:

```bash
git push <remote_name> <branch>

# Set upstream tracking on first push of a new branch
git push -u origin <branch>
```

> If another contributor has pushed new commits since your last pull, Git will reject a non-fast-forward push until you pull and integrate their changes.

----

### Inspecting & Deleting Remote Branches

```bash
# Display local branches with their tracked upstream and ahead/behind counts
git branch -vv

# Delete a branch on the remote server (e.g., after merging a PR)
git push <remote_name> --delete <branch_name>
```

----

### Pull Requests (PR) & Merge Strategies

When merging a reviewed Pull Request (GitHub) or Merge Request (GitLab) into `main`:

| Strategy | How It Works | Best For |
|---|---|---|
| `Merge commit` | Preserves all branch commits and creates a merge commit (`--no-ff`) | Explicit feature boundaries & audit trails |
| `Squash and merge` | Combines all PR commits into a **single clean commit** on `main` | Keeping `main` linear when PRs have noisy `WIP` commits |
| `Rebase and merge` | Replays each PR commit linearly onto the tip of `main` | Clean linear history with atomic, well-crafted commits |
