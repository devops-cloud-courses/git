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
git tag
```

* Filter tags matching a pattern (e.g., all `v1.*` releases):

```bash
git tag -l "v1*"
```

----

### Creating a Tag

* **Annotated tag** *(recommended for releases)* — stores full object metadata (tagger name, email, date, message, and optional GPG/SSH signature):

```bash
git tag -a <tag_name> -m "<tag_message>"
```

* **Lightweight tag** — a simple static pointer to a specific commit:

```bash
git tag <tag_name>
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
