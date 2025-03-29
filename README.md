# **Git: A Complete Guide from Basics to Advanced Workflows**

## **Introduction to Git**

### **What is Git?**
Git is a **distributed version control system (DVCS)** that helps developers track changes in their codebase. Created by **Linus Torvalds** in 2005, Git allows:
- Tracking every modification to files
- Collaborating with other developers
- Reverting to previous versions when needed
- Managing multiple parallel development streams

### **Why Use Git?**
- **Version History:** Never lose previous work
- **Team Collaboration:** Multiple people can work simultaneously
- **Branching:** Isolate features/bug fixes without affecting main code
- **Open Source:** Free and widely adopted (used by >90% of developers)

### **Git vs GitHub**
- **Git:** The version control software that runs locally
- **GitHub/GitLab/Bitbucket:** Cloud platforms that host Git repositories with additional features

---

## **Getting Started with Git**

### **1. Installation**
Download Git from [git-scm.com](https://git-scm.com/) and verify:
```bash
git --version
# Should show e.g. "git version 2.39.2"
```

### **2. Configuration**
Set your identity (used in commits):
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### **3. Creating Your First Repository**
```bash
mkdir my-project
cd my-project
git init  # Initializes empty Git repo
```

---

## **Basic Git Workflow with Files**

### **Scenario 1: Creating and Tracking a Single File**
1. **Create a new file:**
   ```bash
   touch README.md
   ```

2. **Add content:**
   ```bash
   echo "# My Project" >> README.md
   ```

3. **Check status:**
   ```bash
   git status  # Shows README.md as untracked
   ```

4. **Stage the file:**
   ```bash
   git add README.md
   ```

5. **Commit changes:**
   ```bash
   git commit -m "Add project README"
   ```

---

### **Scenario 2: Working with Multiple Files**
1. **Create multiple files:**
   ```bash
   touch index.html style.css script.js
   ```

2. **Add content to each:**
   ```bash
   echo "<!DOCTYPE html>" > index.html
   echo "body { color: red; }" > style.css
   echo "console.log('Hello')" > script.js
   ```

3. **Stage all files at once:**
   ```bash
   git add .
   ```

4. **Commit together:**
   ```bash
   git commit -m "Add initial website files"
   ```

---

### **Scenario 3: Modifying Existing Files**
1. **Edit a file:**
   ```bash
   echo "<h1>Welcome</h1>" >> index.html
   ```

2. **Check changes:**
   ```bash
   git diff  # Shows unstaged changes
   ```

3. **Stage and commit:**
   ```bash
   git add index.html
   git commit -m "Add heading to index.html"
   ```

---
# **Git Branching: Concepts, Importance, and Naming Strategies**

## **What is a Git Branch?**

A **branch** in Git is an independent line of development that allows you to:
- Work on new features without affecting the main codebase
- Fix bugs in isolation
- Experiment safely
- Maintain different versions (e.g., production vs development)

**Technical Definition:**  
A branch is simply a lightweight movable pointer to a specific commit in your repository's history.

## **Why Branching is Important**

1. **Isolation of Work**  
   - Developers can work independently without stepping on each other's changes
   - Prevents unstable code from breaking the main project

2. **Parallel Development**  
   - Multiple features can be developed simultaneously
   - Different teams can work on separate components

3. **Risk Reduction**  
   - Changes can be tested thoroughly before merging
   - Easy to discard unsuccessful experiments

4. **Organized Workflow**  
   - Clear separation of concerns (features, releases, hotfixes)
   - Better historical tracking of changes

## **Branch Naming in GitFlow Strategy**

GitFlow is a popular branching model that defines strict naming conventions:

### **1. Main Branches (Permanent)**
| Branch Name | Purpose |
|-------------|---------|
| `main`/`master` | Production-ready code (always deployable) |
| `develop` | Integration branch for features (pre-release state) |

### **2. Supporting Branches (Temporary)**
| Branch Type | Naming Pattern | Purpose | Example |
|------------|---------------|---------|---------|
| **Feature** | `feature/*` | New functionality | `feature/user-auth` |
| **Release** | `release/*` | Preparing for production | `release/v1.2.0` |
| **Hotfix** | `hotfix/*` | Critical production fixes | `hotfix/login-bug` |
| **Bugfix** | `bugfix/*` | Non-critical fixes | `bugfix/typo-123` |

### **3. Common Naming Best Practices**
- Use **lowercase** with hyphens (`feature/new-dashboard`)
- Prefix with branch type (`fix/`, `docs/`, `chore/`)
- Reference issue IDs when applicable (`feature/PROJ-123-add-search`)
- Keep names **short but descriptive** (avoid generic names like `patch-1`)

## **Visualizing GitFlow Branches**

```
main
└── develop
    ├── feature/user-auth
    ├── feature/payment-gateway
    ├── release/v1.3.0
    └── hotfix/login-error
```

## **When to Create Branches**
1. **Starting a new feature** → `git checkout -b feature/awesome-feature`
2. **Preparing a release** → `git checkout -b release/v1.4.0`
3. **Fixing critical bugs** → `git checkout -b hotfix/db-connection`

## **Branch Lifecycle**
1. Create from `develop` (for features) or `main` (for hotfixes)
2. Work locally and push to remote
3. Merge via Pull Request (GitHub/GitLab)
4. Delete after merging (keeps repository clean)

**Pro Tip:**  
Use `git branch -a` to view all branches (local + remote) and `git fetch --prune` to clean up deleted remote branches.

---

# **Working with Remote Repositories: GitHub and Git Integration**

## **What is a Remote Repository?**

A **remote repository** is a version of your project hosted on:
- **GitHub** (Microsoft-owned, most popular)
- **GitLab** (self-hosting options)
- **Bitbucket** (Atlassian product, good for Jira integration)

Key benefits:
- Cloud backup of your code
- Enables team collaboration
- Provides issue tracking, CI/CD, and project management tools

## **Creating a GitHub Repository**

### **Step 1: Sign Up/Log In**
1. Go to [github.com](https://github.com)
2. Create an account or log in

### **Step 2: Create New Repository**
1. Click **+** → **New repository**
2. Configure settings:
   - **Repository name**: `my-project` (no spaces)
   - **Description**: Optional project description
   - **Visibility**: Public (free) or Private
   - **Initialize with README**: ✔️ (Recommended for new projects)
   - **Add .gitignore**: Select language/framework
   - **License**: Optional (MIT, Apache, etc.)

3. Click **Create repository**

### **Repository URL Formats**
- HTTPS: `https://github.com/username/my-project.git`
- SSH: `git@github.com:username/my-project.git`

## **Connecting Local Git to GitHub**

### **Method 1: New Project (No Existing Code)**
```bash
# Initialize local repo
mkdir my-project
cd my-project
git init

# Connect to GitHub
git remote add origin https://github.com/username/my-project.git

# First push
git push -u origin main
```

### **Method 2: Existing Local Project**
```bash
cd existing-project

# If not already a Git repo:
git init

# Connect to GitHub
git remote add origin https://github.com/username/my-project.git

# First push (may need to pull first if README exists)
git pull origin main --allow-unrelated-histories
git push -u origin main
```

### **Verifying the Connection**
```bash
git remote -v
# Should show:
# origin  https://github.com/username/my-project.git (fetch)
# origin  https://github.com/username/my-project.git (push)
```
---

# **Advanced Git Techniques:**

## **1. Selective Commit Integration (Cherry-Pick)**
**Purpose:** Apply specific commits from one branch to another without merging entire histories.

**Scenario:** Backporting a critical fix from `develop` to `main`
```bash
# On main branch
git cherry-pick abc1234  # Commit hash from develop
git push origin main
```

## **2. History Rewriting (Rebase)**
**Purpose:** Maintain linear project history by replaying commits.

**Scenario:** Updating a feature branch with latest `main` changes
```bash
git checkout feature/login
git rebase main
# Resolve conflicts if any
git push --force-with-lease
```

## **3. Temporary Work Storage (Stash)**
**Purpose:** Shelve uncommitted changes to switch contexts.

**Scenario:** Emergency bug fix while working on a feature
```bash
git stash -u  # -u includes untracked files
git checkout hotfix/issue-123
# After fixing...
git checkout feature/login
git stash pop
```

## **4. Precise Change Management (Interactive Add)**
**Purpose:** Stage specific portions of files.

**Scenario:** Committing only part of a file's changes
```bash
git add -p  # Opens interactive prompt
# Choose which hunks to stage
git commit -m "Partial feature implementation"
```

## **5. Commit History Surgery (Interactive Rebase)**
**Purpose:** Clean up local commit history before sharing.

**Scenario:** Combining WIP commits before PR
```bash
git rebase -i HEAD~5
# In editor: squash/split/reword commits
git push --force-with-lease
```

## **6. Binary Search Debugging (Bisect)**
**Purpose:** Identify the exact commit introducing a bug.

**Scenario:** Finding regression origin
```bash
git bisect start
git bisect bad HEAD
git bisect good v2.1.0
# Test at each step, mark good/bad
git bisect reset  # Clean up
```

## **7. Versioned Releases (Tagging)**
**Purpose:** Mark specific points as releases.

**Scenario:** Creating an annotated release tag
```bash
git tag -a v2.3.0 -m "Production release February 2024"
git push --tags
```

## **8. Change Portability (Patch Files)**
**Purpose:** Share changes without direct repo access.

**Scenario:** Sending a fix to a contributor
```bash
git format-patch HEAD~1  # Creates 0001-commit-message.patch
# Recipient applies with:
git am 0001-fix.patch
```

## **9. Parallel Development (Worktree)**
**Purpose:** Multiple working directories from one repo.

**Scenario:** Simultaneous work on different features
```bash
git worktree add ../hotfix-123 hotfix/issue-123
cd ../hotfix-123  # Independent working directory
```

## **10. Subproject Management (Submodules)**
**Purpose:** Include external repos as dependencies.

**Scenario:** Adding a shared component library
```bash
git submodule add https://github.com/team/ui-components.git
git commit -m "Add UI component submodule"
```

## **11. History Recovery (Reflog)**
**Purpose:** Retrieve lost commits or branches.

**Scenario:** Restoring accidentally deleted branch
```bash
git reflog  # Find last known good state
git checkout -b recovered-feature abc1234
```

## **12. Custom Automation (Hooks)**
**Purpose:** Trigger scripts on Git events.

**Scenario:** Pre-commit linting
```bash
# .git/hooks/pre-commit
#!/bin/sh
npm run lint || exit 1
chmod +x .git/hooks/pre-commit
```

## **Pro Tips for Advanced Workflows**
1. **Safety First:** Always:
   ```bash
   git push --force-with-lease  # Safer than --force
   git config --global rerere.enabled true  # Reuse recorded resolutions
   ```

2. **Visualization Tools:**
   ```bash
   git log --graph --oneline --all  # ASCII history graph
   ```

3. **Partial Clones (Large Repos):**
   ```bash
   git clone --filter=blob:none <repo>  # No file contents initially
   ```

---
