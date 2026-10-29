## Working with Remotes

----

### Listing Remote Repositories

View configured remote names and their fetch/push URLs:

```bash
git remote -v
```

----

### Inspecting a Remote

View detailed information about a specific remote (URL, tracked branches, `HEAD`):

```bash
git remote show <remote_name>
```

----

### Adding a Remote Repository

Register a new remote repository with a short alias (such as `origin` or `upstream`):

```bash
git remote add <remote_name> <url>
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

### Renaming & Removing a Remote

```bash
git remote rename <old_remote_name> <new_remote_name>
git remote remove <remote_name>
```

----

### Fetching Changes from a Remote

Download new commits, files, and refs from a remote repository into your local database:

```bash
git fetch <remote_name>
```

> `git fetch` only downloads the latest data — it **never modifies** your working directory or merges automatically.

----

### Pulling Changes (`fetch` + `merge`)

Download the latest changes from the tracked remote branch and integrate them into your current branch:

```bash
git pull <remote_name> <branch>
```

* Use `git pull --rebase` to replay your local commits on top of the upstream changes instead of creating a merge commit.

----

### Pushing Changes to a Remote

Publish your local commits to a remote repository:

```bash
git push <remote_name> <branch>

# Set upstream tracking on first push
git push -u origin <branch>
```

> If another contributor has pushed new commits since your last pull, Git will reject a non-fast-forward push until you pull and resolve any differences.

----

### Safe Force-Pushing (`--force-with-lease`)

After rebasing a pushed feature branch, update your remote Pull Request safely:

```bash
# Safe: fails if a teammate pushed new commits you haven't fetched yet
git push --force-with-lease

# Dangerous: blindly overwrites remote branch history
git push --force
```

> **Best Practice:** Always prefer `--force-with-lease` over `--force` on feature branches, and never force-push to `main`.

----

### Pull Requests (PR) & Merge Strategies

When merging a reviewed Pull Request (GitHub) or Merge Request (GitLab) into `main`:

| Strategy | How It Works | Best For |
|---|---|---|
| `Merge commit` | Preserves all branch commits and creates a merge commit (`--no-ff`) | Explicit feature boundaries & audit trails |
| `Squash and merge` | Combines all PR commits into a **single clean commit** on `main` | Keeping `main` linear when PRs have noisy `WIP` commits |
| `Rebase and merge` | Replays each PR commit linearly onto the tip of `main` | Clean linear history with atomic, well-crafted commits |
