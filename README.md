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

## **Branching Workflow**

### **1. Create a New Branch**
```bash
git checkout -b new-feature
```

### **2. Make Changes in the Branch**
```bash
echo "New feature content" >> feature.txt
git add feature.txt
git commit -m "Implement new feature"
```

### **3. Switch Back to Main Branch**
```bash
git checkout main
```

### **4. Merge Changes**
```bash
git merge new-feature
```

### **5. Delete Branch (After Merge)**
```bash
git branch -d new-feature
```

---

## **Working with Remote Repositories**

### **1. Connect to GitHub**
```bash
git remote add origin https://github.com/user/repo.git
```

### **2. Push Changes**
```bash
git push -u origin main
```

### **3. Pull Updates**
```bash
git pull origin main
```

---

## **Advanced Scenarios**

### **Undoing Changes**
| Situation | Command |
|-----------|---------|
| Unstage a file | `git reset HEAD file` |
| Discard local changes | `git checkout -- file` |
| Amend last commit | `git commit --amend` |

### **Viewing History**
```bash
git log --oneline --graph  # Compact view with branch visualization
```

---

## **Conclusion**
This guide covers:
- Git fundamentals and setup
- Creating/modifying files
- Branching strategies
- Remote repository workflows
- Common troubleshooting

**Next Steps:**
1. Practice with real projects
2. Learn about `.gitignore`
3. Explore collaborative workflows (Pull Requests)

Master these concepts, and you'll be using Git like a pro! 🚀
