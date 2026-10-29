## Overview of Git

----

### Why use a VCS?

* **VCS** stands for **Version Control System**
* Allows you to navigate through a complete commit history
* Enables parallel collaboration across isolated branches
* Provides traceability, auditability, and safe rollback

----

### The most widely used VCS: Git

* Created in `2005` by **Linus Torvalds**
* Originally built to manage **Linux kernel** development
* Fast, distributed, and the de facto standard across Open Source and Enterprise

----

### Centralized VCS vs. ...

<img src="images/centralized.svg" alt="Centralized VCS" />

----

### Distributed VCS

<img src="images/distributed.svg" alt="Distributed VCS" />

----

### Popular Git Hosting Platforms

* **GitHub** — Largest open-source & enterprise platform (GitHub Actions, Pull Requests, Dependabot)
* **GitLab** — Complete DevSecOps platform (self-hosted or SaaS with GitLab CI/CD & Container Registry)
* **Bitbucket** — Atlassian's enterprise Git platform (Bitbucket Pipelines & native Jira integration)

----

### Everything is a snapshot: Deltas (Other VCS)

<img src="images/deltas.svg" alt="Delta-based VCS" />

----

### Everything is a snapshot: Git Snapshots

<img src="images/snapshots.svg" alt="Git Snapshots" />

----

### Inside `.git`: Integrity & Hashing

* Git verifies data integrity using cryptographic hashes (`SHA-1` 40-char hex, or `SHA-256` 64-char hex)
* Every object (`blob`, `tree`, `commit`, `tag`) is content-addressed by the hash of its contents
* Almost every Git operation only **appends data** to the `.git` database, making committed history tamper-evident

----

### Inside `.git`: Object Graph

<img src="images/object-graph.svg" alt="Git Object Graph" />

----

### The Three Areas of a Git Project

* **Working Directory**: A single checked-out version of the project on your local filesystem
* **Staging Area (`Index`)**: Tracks which modified files will go into your **next commit**
* **Git Directory (`.git`)**: The compressed database storing all metadata and object history for your project

----

### The Three Areas of a Git Project

<img src="images/areas.svg" alt="The Three Areas of Git" />

----

### Installation & First-Time Setup

* [Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) & [First-Time Setup](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)

```bash
git config --global user.name "Jane Doe"
git config --global user.email "jane.doe@example.com"
git config --global init.defaultBranch main
git config --global pull.rebase true
git config --global push.autoSetupRemote true
```

> **Note:** Setting your `user.name` and `user.email` is required before creating commits in the hands-on labs.

----

### Getting Help & Documentation

* [Official Pro Git Book](https://git-scm.com/book/en/v2)
* [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials/what-is-git)
* Built-in command-line help:

```bash
git help <verb>
man git-<verb>
git <verb> -h
```
