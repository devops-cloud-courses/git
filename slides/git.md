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

### Everything is a snapshot: Deltas (Other VCS)

<img src="images/deltas.svg" alt="Delta-based VCS" />

----

### Everything is a snapshot: Git Snapshots

<img src="images/snapshots.svg" alt="Git Snapshots" />

----

### Inside `.git`: Object Graph

<img src="images/object-graph.svg" alt="Git Object Graph" />

----

### Inside `.git`: Integrity & Hashing

* Git verifies data integrity using cryptographic checksums (`SHA-1` / `SHA-256`)
* Every object (blob, tree, commit, tag) is addressed by its **40-character hexadecimal hash**
* Almost every Git operation only **adds data** to the Git database, making it very hard to lose committed work

----

### The Three Areas of a Git Project

<img src="images/areas.svg" alt="The Three Areas of Git" />

----

### The Three Areas of a Git Project

* **Git Directory (`.git`)**: The compressed database storing all metadata and object history for your project
* **Working Directory**: A single checked-out version of the project on your local filesystem
* **Staging Area (`Index`)**: A file that tracks which modified snapshots will go into your **next commit**

----

### Installation & First-Time Setup

* [Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [First-Time Git Setup](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)

```bash
git config --global user.name "Jane Doe"
git config --global user.email "jane.doe@example.com"
git config --global init.defaultBranch main
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

----

### Popular Git Hosting Platforms

* **GitHub** — Largest open-source & enterprise platform (GitHub Actions, Pull Requests)
* **GitLab** — Complete DevSecOps platform (self-hosted or SaaS with GitLab CI/CD)
* **Bitbucket** — Atlassian's Git solution (tight integration with Jira & Trello)
