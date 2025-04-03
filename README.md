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

**Windows/macOS:**  
- Download and run the installer  

**Linux (Debian/Ubuntu):**  
```bash
sudo apt update && sudo apt install git -y
```  

**Linux (RHEL/CentOS):**  
```bash
sudo yum install git -y
```  

Verify installation:  
```bash
git --version  # Should show e.g., "git version 2.39.2"
```  

### **2. Configuration**  
Set your identity (used in commits):  
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```  

Optional settings:  
```bash
git config --global core.editor "code --wait"  # Use VS Code as default editor
git config --global init.defaultBranch "main"  # Set default branch name
```  

View your Git config:  
```bash
git config --list
```  

### **3. Creating Your First Repository**  
Initialize a new repository:  
```bash
mkdir my-project
cd my-project
git init  # Creates a hidden .git directory
```  

Check repository status:  
```bash
git status
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
   git status  # Shows README.md as "untracked"
   ```  

4. **Stage the file:**  
   ```bash
   git add README.md
   ```  

5. **Commit changes:**  
   ```bash
   git commit -m "Add project README"
   ```  

6. **View commit history:**  
   ```bash
   git log  # Shows commit history with details
   git log --oneline  # Compact view
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

4. **Check staged changes:**  
   ```bash
   git status  # Shows files as "staged"
   ```  

5. **Commit together:**  
   ```bash
   git commit -m "Add initial website files"
   ```  

6. **Unstage a file before committing (if needed):**  
   ```bash
   git reset HEAD style.css  # Removes style.css from staging
   git status  # Now shows style.css as "not staged"
   ```  

---

### **Scenario 3: Modifying and Undoing Changes**  
1. **Edit a file:**  
   ```bash
   echo "<h1>Welcome</h1>" >> index.html
   ```  

2. **Check changes before staging:**  
   ```bash
   git diff  # Shows unstaged changes
   ```  

3. **Stage the modified file:**  
   ```bash
   git add index.html
   ```  

4. **Check staged changes:**  
   ```bash
   git diff --staged  # Shows changes in staging
   ```  

5. **Commit changes:**  
   ```bash
   git commit -m "Add heading to index.html"
   ```  

6. **Undo the last commit (before pushing):**  
   ```bash
   git reset --soft HEAD~1  # Keeps changes staged
   git reset --mixed HEAD~1  # Unstages changes (default)
   git reset --hard HEAD~1  # Discards changes completely (use with caution!)
   ```  

7. **Revert a commit (safe undo for pushed commits):**  
   ```bash
   git revert <commit-hash>  # Creates a new commit undoing changes
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

# **GitFlow Workflow**

## **What is GitFlow?**
GitFlow is a branching model for Git that provides a structured approach to managing features, releases, and hotfixes. It uses specific branch types with strict rules about how they interact.

### **Core Branches**
1. **`main`/`master`** - Production-ready code (always deployable)
2. **`develop`** - Integration branch for completed features (pre-release state)

### **Supporting Branches**
1. **`feature/*`** - New functionality (temporary)
2. **`release/*`** - Preparation for production (temporary)
3. **`hotfix/*`** - Critical production fixes (temporary)

---

## **Workflow Example with All Branch Types**

### **1. Starting a New Feature**
**Scenario**: Adding user profile management

```bash
# Start from develop branch
git checkout develop
git pull origin develop

# Create feature branch
git checkout -b feature/user-profiles

# Develop the feature (multiple commits)
git add .
git commit -m "Add profile creation UI"
git commit -m "Implement profile saving logic"
git push -u origin feature/user-profiles
```

*Note: There could be many parallel feature branches (feature/search, feature/checkout, etc.)*

---

### **2. Completing the Feature via Pull Request**
```bash
# When feature is ready:
# 1. Push final changes
git push origin feature/user-profiles

# 2. Create Pull Request (PR) from:
#    feature/user-profiles → develop

# 3. After PR approval and merge:
git checkout develop
git pull origin develop  # Get latest with your feature

# 4. Cleanup
git branch -d feature/user-profiles
git push origin --delete feature/user-profiles
```

---

### **3. Preparing a Release**
**Scenario**: Releasing v1.3.0

```bash
# From develop branch
git checkout develop
git pull origin develop

# Create release branch
git checkout -b release/v1.3.0

# Final testing/bug fixing (NO new features)
git commit -m "Fix last-minute profile image bug"

# Create PR: release/v1.3.0 → main AND develop
```

**After PR approval**:
```bash
# Merge to main and tag
git checkout main
git merge --no-ff release/v1.3.0
git tag -a v1.3.0 -m "Release v1.3.0"

# Merge to develop
git checkout develop
git merge --no-ff release/v1.3.0

# Cleanup
git branch -d release/v1.3.0
git push origin main develop --tags
```

---

### **4. Emergency Hotfix**
**Scenario**: Critical login bug in production

```bash
# From main branch
git checkout main
git pull origin main

# Create hotfix branch
git checkout -b hotfix/login-security

# Make emergency fix
git commit -m "Patch SQL injection vulnerability"

# Create PR: hotfix/login-security → main AND develop
```

**After PR approval**:
```bash
# Merge to main and tag
git checkout main
git merge --no-ff hotfix/login-security
git tag -a v1.3.1 -m "Hotfix v1.3.1"

# Merge to develop
git checkout develop
git merge --no-ff hotfix/login-security

# Cleanup
git branch -d hotfix/login-security
git push origin main develop --tags
```

---

## **Visual Branch Timeline**
```
main
├── v1.2.0
├── v1.3.0          (from release branch)
└── v1.3.1          (from hotfix)
    
develop
├── feature/user-profiles (merged via PR)
├── release/v1.3.0  (merged via PR)
└── hotfix/login-security (merged via PR)
```

## **Key Principles**
1. **All merges happen through PRs** for code review
2. **`main` always represents production** (only updated via releases/hotfixes)
3. **Features are isolated** until fully tested
4. **Release branches stabilize** code before production
5. **Hotfixes bypass normal flow** for emergencies

## **Why This Works**
- **Clear separation** of development stages
- **Controlled integration** through PRs
- **Traceable releases** through tags
- **Emergency patching** without disrupting feature work

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
# **GitHub Branch Protection Rules for GitFlow**

To enforce GitFlow properly in GitHub, you need to configure branch protection rules that:
1. Restrict direct pushes to `main`
2. Only allow merges via Pull Requests (PRs)
3. Require approvals for `main` merges
4. Limit which branches can merge to `main` (only `release/*` and `hotfix/*`)

## **Step-by-Step Setup**

### **1. Navigate to Branch Protection Settings**
1. Go to your GitHub repository
2. Click **Settings** → **Branches**
3. Under "Branch protection rules", click **Add rule**

### **2. Configure Protection for `main` Branch**
| Setting | Value | Purpose |
|---------|-------|---------|
| Branch name pattern | `main` | Applies to production branch |
| Require a pull request before merging | ✅ Enabled | All changes must go through PR |
| Require approvals | ✅ Enabled (set to 1 or more) | Ensures code review |
| Dismiss stale pull request approvals | ✅ Enabled | Requires fresh approvals after changes |
| Require approval from code owners | Optional | Extra layer of control |
| Restrict who can dismiss reviews | Optional | Limit to maintainers |
| Allow specified branches to merge | `release/*`, `hotfix/*` | GitFlow enforcement |
| Require status checks to pass | Optional (recommended) | CI/CD requirements |
| Require conversation resolution | ✅ Enabled | All comments must be addressed |
| Require linear history | Optional | Prevents merge commits |
| Include administrators | ✅ Enabled | Even repo admins must follow |

### **3. Additional Recommended Rules**

**For `develop` branch (same settings as above except):**
- Branch name pattern: `develop`
- Allow specified branches to merge: `feature/*`, `bugfix/*`, `hotfix/*`

### **4. Alternative: Using GitHub Actions for Advanced Control**
If you need more complex rules (like requiring specific PR labels), create a `.github/workflows/branch-protection.yml`:

```yaml
name: Enforce GitFlow Merges
on:
  pull_request_target:
    types: [opened, reopened, synchronize]

jobs:
  check-merge-rules:
    runs-on: ubuntu-latest
    steps:
      - name: Verify merge rules
        run: |
          # Only allow release/* and hotfix/* to merge to main
          if [[ "$GITHUB_BASE_REF" == "main" && ! "$GITHUB_HEAD_REF" =~ ^release/.*|^hotfix/.* ]]; then
            echo "::error::Only release/* or hotfix/* branches can merge to main"
            exit 1
          fi
```

## **How This Works in Practice**

### **Allowed Merge Scenario**
1. Developer creates `release/v1.2.0` from `develop`
2. PR created: `release/v1.2.0` → `main`
3. After 1+ approvals and CI passes, merge is allowed

### **Blocked Merge Scenarios**
- ❌ `feature/login` → `main` *(Fails: Not a release/hotfix branch)*
- ❌ Direct push to `main` *(Fails: PR required)*
- ❌ `release/v1.2.0` → `main` with no approvals *(Fails: Approval required)*
