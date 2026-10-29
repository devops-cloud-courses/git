## Basic Usage

----

### Initializing or Cloning a Repository

* Initialize a brand-new Git repository in an existing local folder (creates `.git/`), or clone an existing remote repository:

```bash
# Option 1: Turn current directory into a new Git repository
git init

# Option 2: Clone a full local copy of an existing remote repository
git clone <url>
```

----

### File States & Lifecycle

* **Untracked**: File is not in the last snapshot and not in the staging area
* **Tracked**: File is known to Git and can be in one of three states:
  * `Unmodified (Committed)` — safely stored in your local `.git` database
  * `Modified` — changed in your working directory, but not staged yet
  * `Staged` — marked in its current version to go into your next commit snapshot

----

### File States & Lifecycle

<img src="images/lifecycle.svg" alt="Git File Lifecycle" />

----

### Checking File Status

Whenever you want to inspect the current branch and state of files in your repository:

```bash
git status
```

* Common option:
  * `-s` / `--short` — display status in a compact two-column format

----

### Staging Files (`git add`)

Stage new (`untracked`) or updated (`modified`) files into the **Staging Area**:

```bash
# Stage a specific file
git add myfile.txt

# Stage all new and modified files in the current directory
git add .
```

----

### Ignoring Files (`.gitignore`)

To prevent generated artifacts, secrets, or dependencies from being tracked or staged during `git add`, define glob patterns in a `.gitignore` file:

```gitignore
*.log
.env
node_modules/
build/
doc/**/*.pdf
```

----

### Inspecting Changes (`git diff`)

* Compare unstaged vs. staged changes in your repository:

```bash
# Unstaged changes (Working Directory vs. Staging Area)
git diff

# Staged changes ready for next commit (Staging Area vs. HEAD)
git diff --staged   # (or: git diff --cached)
```

----

### Committing Changes (`git commit`)

Record your staged snapshot into the repository history:

```bash
git commit -m "feat(api): add healthcheck endpoint"
```

* Common options:
  * `-m "<commit_message>"` — provide the commit message inline without opening an editor
  * `-a` — automatically stage all tracked, modified files before committing

----

### Commit Hygiene: Conventional Commits

Format: `<type>(<scope>): <short summary>` — powers automated changelogs and Semantic Versioning (`SemVer`):

| Type | Purpose | SemVer Impact |
|---|---|---|
| `feat` | Introduce a new feature (`feat(auth): add OAuth2 PKCE`) | `MINOR` (`0.x.0`) |
| `fix` | Patch a bug (`fix(api): handle null cursor`) | `PATCH` (`0.0.x`) |
| `docs` / `chore` / `refactor` | Documentation, maintenance, or code restructuring | None |
| `feat!` / `BREAKING CHANGE` | Incompatible API or infrastructure change | `MAJOR` (`x.0.0`) |

----

### Unstaging a File

Move a file from the **Staging Area** back to `modified` (without losing your file edits):

```bash
# Modern syntax (Git 2.23+)
git restore --staged <file>

# Classic syntax
git reset HEAD <file>
```

----

### Discarding Local Modifications

Revert a `modified` file in your working directory back to its last committed state:

```bash
# Modern syntax (Git 2.23+)
git restore <file>

# Classic syntax
git checkout -- <file>
```

> **Warning:** Discarding local modifications cannot be undone — uncommitted changes in that file are permanently lost.

----

### Removing & Moving Files

* Remove or rename tracked files and stage the change in one step:

```bash
# Remove from both Working Directory and Staging Area
git rm <file>

# Stop tracking in Git while keeping the file on disk (untracked)
git rm --cached <file>

# Move or rename a tracked file
git mv <from> <to>
```

----

### Viewing Commit History (`git log`)

Inspect the chronological history of commits in the current branch:

```bash
git log

# Compact one-line view with abbreviated 7-character SHA hashes
git log --oneline --graph
```

----

### `git log`: Formatting Options

| Option | Description |
|---|---|
| `-n <N>` | Limit output to the last `N` commits |
| `-p` / `--patch` | Show the full diff (patch) introduced in each commit |
| `--stat` | Show abbreviated stats for modified files in each commit |
| `--oneline` | Condense each commit to a single line (`short SHA` + title) |
| `--graph` | Draw an ASCII graph of the branch and merge history |

----

### `git log`: Filtering by Time & Author

| Option | Description |
|---|---|
| `--since=<date>` | Commits more recent than a specific date (e.g., `--since=2.weeks`) |
| `--until=<date>` | Commits older than a specific date (e.g., `--until="2026-01-01"`) |
| `--author=<pattern>` | Only show commits where the author matches `<pattern>` |
| `--committer=<pattern>` | Only show commits where the committer matches `<pattern>` |

----

### `git log`: Filtering by Content

| Option | Description |
|---|---|
| `--grep=<pattern>` | Only show commits with a commit message matching `<pattern>` |
| `--all-match` | Require commits to match all given `--grep` / `--author` criteria |
| `-S <string>` | *Pickaxe search*: only show commits that added or removed `<string>` |
| `--no-merges` | Hide merge commits (commits with more than one parent) |
