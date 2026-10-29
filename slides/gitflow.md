## Gitflow

----

### Gitflow: Branching Workflow

<img src="images/gitflow.svg" alt="Gitflow Workflow" />

----

### Branch: `main`

* Represents the **production-ready** state of the codebase
* Long-lived (`infinite`) branch
* The most stable branch in the repository — every merge into it corresponds to a production release tag

----

### Branch: `develop`

* Main **integration branch** for ongoing development work
* Long-lived (`infinite`) branch
* Must remain stable at all times, as Continuous Integration (`CI`) pipelines run continuously against it

----

### Branch: `feature/*`

* Dedicated to developing a single new feature or user story
* **Short-lived** branch designed to isolate work-in-progress
* Branches off from `develop` and merges back into `develop` via a Pull / Merge Request

----

### Branch: `bugfix/*` & `hotfix/*`

* Dedicated to fixing a bug in an upcoming release (`bugfix/*`) or an urgent production issue (`hotfix/*`)
* **Short-lived** branch
* `hotfix/*` branches off from `main` and merges back into both `main` and `develop`

----

### Branch: `release/*`

* Prepares and stabilizes a new production release (version bump, final QA, documentation)
* **Short-lived** branch — no new features are added here, only release bug fixes
* Branches off from `develop` and merges into `main` (and back into `develop`)

----

### Branch: `support/*`

* Used to maintain and patch a legacy major version still running in production
* Lives as long as that specific legacy version is supported
* Fixes are typically backported from `main` using `git cherry-pick`

----

### CI/CD Pipelines by Branch

* Different branch types trigger tailored **Continuous Integration / Continuous Delivery** workflows:
  * **`feature/*`**: Fast feedback loop — linting, unit tests, and build verification
  * **`develop`**: Full build, integration tests, static code analysis (`SAST`), and deployment to staging
  * **`main` / `release/*`**: Security scans, release artifact signing, and automated production deployment

----

### Modern Alternative: Trunk-Based & GitHub Flow

<img src="images/trunk-based.svg" alt="Trunk-Based Development & GitHub Flow" />

----

### Gitflow vs. Trunk-Based Development

| Dimension | Gitflow | Trunk-Based / GitHub Flow |
|---|---|---|
| `Long-lived branches` | `main` + `develop` (+ `support/*`) | Single trunk (`main` is always deployable) |
| `Branch lifespan` | Days to weeks (`feature/*`, `release/*`) | Hours to `< 2 days` (small, frequent PRs) |
| `Incomplete features` | Isolated on long-lived branches | Hidden behind **Feature Flags** in `main` |
| `Best suited for` | Scheduled / versioned software, mobile apps, regulated releases | Cloud-native SaaS, microservices, high-velocity **CI/CD & DORA** teams |
