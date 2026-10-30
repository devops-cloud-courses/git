# Git in a Nutshell

An interactive presentation on **Git, Branching Workflows, and DevSecOps**, powered by [Reveal.js 6.0.2](https://revealjs.com/).

* **Live Presentation:** [https://devops-cloud-courses.github.io/git](https://devops-cloud-courses.github.io/git)
* **Download PDF (Latest Release):** [git-in-a-nutshell.pdf](https://github.com/devops-cloud-courses/git/releases/latest/download/git-in-a-nutshell.pdf)
* **Browser Print View:** [https://devops-cloud-courses.github.io/git/?print-pdf&pdfSeparateFragments=false](https://devops-cloud-courses.github.io/git/?print-pdf&pdfSeparateFragments=false)

---

## Course Curriculum

1. **Overview of Git** (`slides/git.md`)
   * Centralized vs. Distributed VCS, Git hosting platforms (GitHub, GitLab, Bitbucket)
   * Snapshots vs. deltas, content-addressable `.git` object graph (`blob`, `tree`, `commit`, `tag`) with `SHA-1` / `SHA-256`
   * The Three Areas (`Working Directory`, `Staging Area / Index`, `.git` repository) & modern global setup
2. **Basic Usage & Commit Hygiene** (`slides/basics.md`)
   * Repository initialization (`git init`, `git clone`) and file lifecycle states
   * Staging, `.gitignore` globbing, inspecting diffs (`git diff`, `git diff --staged`), and committing
   * **Conventional Commits** & **Semantic Versioning (`SemVer`)**
   * Undoing working tree & index changes with modern CLI (`git restore`, `git restore --staged`)
   * Navigating and filtering commit history (`git log --oneline --graph`, pickaxe search `-S`, `--grep`)
3. **Branching & Merging** (`slides/branches.md`)
   * Internal mechanics of branches, commits, trees, parent pointers, `main`, and `HEAD`
   * Creating and switching branches (`git branch`, `git switch`, `git switch -c`)
   * Fast-forward vs. three-way merges (`git merge`) and resolving merge conflicts
4. **Working with Remotes & Pull Requests** (`slides/remotes.md`)
   * Managing remotes (`origin`, `upstream`) and **SSH `Ed25519`** vs. HTTPS authentication
   * Remote-tracking branches (`origin/main`), `git fetch`, `git pull --rebase`, and `git push -u`
   * Pull Request / Merge Request integration strategies (`Merge commit`, `Squash and merge`, `Rebase and merge`)
5. **Branching Workflows** (`slides/gitflow.md`)
   * **Gitflow** (`main`, `develop`, `feature/*`, `bugfix/*`, `hotfix/*`, `release/*`, `support/*`) & CI/CD pipeline mapping
   * **Trunk-Based Development & GitHub Flow** (short-lived branches, continuous integration, feature flags, DORA metrics)
6. **Advanced Git** (`slides/advanced.md`)
   * Annotated vs. lightweight release tags (`git tag -a`) and relative commit references (`HEAD~N`, `main..HEAD`)
   * Rewriting history safely: `git commit --amend`, `git rebase`, Interactive Rebase (`git rebase -i`), and `--force-with-lease`
   * Undoing commits: `git reset` (`--soft`, `--mixed`, `--hard`) vs. `git revert`, surgical backporting (`git cherry-pick`), and recovery (`git reflog`)
7. **Git Power Tools & DevSecOps** (`slides/tools.md`)
   * Interactive patch staging (`git add -p`, `git restore -p`), stashing (`git stash`), cleaning (`git clean`), and parallel working directories (`git worktree`)
   * Debugging regressions with `git blame` and binary search (`git bisect`)
   * **DevSecOps**: Cryptographic SSH commit signing (`gpg.format ssh`) and pre-commit secret scanning (`pre-commit`, `gitleaks`, `trufflehog`)

---

## Repository Structure

```text
.
├── .github/workflows/
│   └── export-pdf.yml  # GitHub Actions workflow exporting slides to PDF & GitHub Releases
├── index.html          # Reveal.js 6.0.2 entrypoint (jsDelivr CDN, zero-build setup)
├── css/
│   └── custom.css      # Custom light theme, typography (Inter & JetBrains Mono), and responsive layout
├── images/             # Custom vector SVG architecture diagrams & author avatars
└── slides/             # Modular Markdown slide decks loaded dynamically by Reveal.js
```

---

## Running Locally

Because Reveal.js loads external Markdown files (`slides/*.md`) via `fetch`, serve the repository over a local HTTP server rather than opening `index.html` via `file://`:

### Option 1: Python (built-in)
```bash
python3 -m http.server 8000
```
Then open [http://localhost:8000](http://localhost:8000).

### Option 2: Node.js (`npx`)
```bash
npx serve .
```

### Option 3: Docker (`nginx`)
```bash
docker run --rm -p 8080:80 -v "$PWD":/usr/share/nginx/html:ro nginx:alpine
```
Then open [http://localhost:8080](http://localhost:8080).

---

## Exporting to PDF

### Automated GitHub Release (Recommended)
Every push to slide assets on `master` triggers the [Export Slides to PDF & Release](.github/workflows/export-pdf.yml) GitHub Actions workflow using Playwright Chromium (`?print-pdf&pdfSeparateFragments=false`), publishing **`git-in-a-nutshell.pdf`** both as a workflow artifact and as a versioned GitHub Release asset (`vYYYY.MM.DD-<run>`):
* **Direct Download:** [git-in-a-nutshell.pdf](https://github.com/devops-cloud-courses/git/releases/latest/download/git-in-a-nutshell.pdf)

### Manual Export via Chrome / Chromium

1. Open [https://devops-cloud-courses.github.io/git/?print-pdf&pdfSeparateFragments=false](https://devops-cloud-courses.github.io/git/?print-pdf&pdfSeparateFragments=false)
2. Press `Cmd + P` (macOS) or `Ctrl + P` (Windows/Linux)
3. Configure the print dialog settings:

| Setting | Value |
|---|---|
| **Destination** | Save as PDF |
| **Pages** | All |
| **Margins** | None / Default |
| **Options** | Enable **Background graphics** |

---

## Authors

* **Laurent Grangeau** — Cloud Solution Architect @ Google ([@laurentgrangeau](https://twitter.com/laurentgrangeau) | [github.com/laurentgrangeau](https://github.com/laurentgrangeau))
* **Arthur Mauvezin** — DevOps Engineer @ Ouidou Consulting ([@arthurmauvezin](https://twitter.com/arthurmauvezin) | [github.com/arthurmauvezin](https://github.com/arthurmauvezin))
