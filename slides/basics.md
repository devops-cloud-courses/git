## Basic Usage

----

### Cloning a Git Repository

* Clone a full local copy of an existing remote repository:

```bash
git clone <url>
```

----

### File States & Lifecycle

* **Untracked**: File is not in the last snapshot and not in the staging area
* **Tracked**: File is known to Git and can be in one of three states:
  * `Unmodified (Committed)` — safely stored in your local Git database
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
  * `-s` / `--short` — display status in a compact format

----

### Staging Files

Stage new (`untracked`) or updated (`modified`) files into the **Staging Area**:

```bash
git add <files>
```

* Examples:

```bash
git add myfile.txt
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

* View unstaged changes in **modified** files (Working Directory vs. Staging Area):

```bash
git diff
```

* View **staged** changes ready for the next commit (Staging Area vs. Last Commit):

```bash
git diff --staged
# or
git diff --cached
```

----

### Committing Changes

Record your staged snapshot into the repository history:

```bash
git commit
```

* Common options:
  * `-m "<commit_message>"` — provide the commit message inline without opening an editor
  * `-a` — automatically stage all tracked, modified files before committing

----

### Commit Hygiene: Conventional Commits

Structure commit messages so humans and CI/CD pipelines can automatically generate changelogs and bump Semantic Versions (`SemVer`):

```text
<type>(<optional scope>): <short summary>
```

| Type | Purpose | SemVer Impact |
|---|---|---|
| `feat` | Introduce a new feature (`feat(auth): add OAuth2 PKCE flow`) | `MINOR` (`0.x.0`) |
| `fix` | Patch a bug (`fix(api): handle null pagination cursor`) | `PATCH` (`0.0.x`) |
| `docs` / `chore` / `refactor` | Documentation, maintenance, or internal restructuring | None |
| `feat!` / `BREAKING CHANGE:` | Incompatible API or infrastructure change | `MAJOR` (`x.0.0`) |

----

### Removing Files

* Remove a file from both the working directory and the staging area:

```bash
git rm <file>
```

* Stop tracking a file in Git while **keeping it on disk** (`untracked`):

```bash
git rm --cached <file>
```

----

### Moving or Renaming Files

Move or rename a tracked file and stage the change in one step:

```bash
git mv <from> <to>
```

----

### Viewing Commit History

Inspect the chronological history of commits in the current branch:

```bash
git log
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

----

### Unstaging a File

Move a file from the **Staging Area** back to `modified` (without losing your edits):

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
