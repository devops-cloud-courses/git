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
