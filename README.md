# What is Git?
Git is a popular version control system. It was created by Linus Torvalds in 2005, and has been maintained by Junio Hamano since then.

## It is used for:

- Tracking code changes
- Tracking who made changes
- Coding collaboration
# Why Git?
- Over 70% of developers use Git!
- Developers can work together from anywhere in the world.
- Developers can see the full history of the project.
- Developers can revert to earlier versions of a project.
# What is GitHub?
- Git is not the same as GitHub.
- GitHub makes tools that use Git.
- GitHub is the largest host of source code in the world, and has been owned by Microsoft since 2018.

Git Install
You can download Git for free from the following website: https://www.git-scm.com/
```bash
git --version
```
Configure Git
Now let Git know who you are. This is important for version control systems, as each Git commit uses this information:
```bash
git config --global user.name "w3schools-test"
git config --global user.email "test@w3schools.com"
```
Creating Git Folder
Now, let's create a new folder for our project:

```bash
mkdir myproject
cd myproject
```

Initialize Git
Once you have navigated to the correct folder, you can initialize Git on that folder:
```bash
git init 
```
You just created your first Git Repository!

Note: Git now knows that it should watch the folder you initiated it on.

Git creates a hidden folder to keep track of changes.

```bash
vi index.html
```

```bash
<!DOCTYPE html>
<html>
<head>
<title>Hello World!</title>
<link rel="stylesheet" href="bluestyle.css">
</head>
<body>

<h1>Hello world!</h1>
<p>This is the first file in my new Git Repo.</p>

</body>
</html>
```
**ls** will list the files in the directory. We can see that _index.html_ is there.

Then we check the Git _status_ and see if it is a part of our repo:
```bash
git status
```
Now Git is aware of the file, but has not added it to our repository!

Files in your Git repository folder can be in one of 2 states:

- Tracked - files that Git knows about and are added to the repository
- Untracked - files that are in your working directory, but not added to the repository
 When you first add files to an empty repository, they are all untracked. To get Git to track them, you need to stage them, or add them to the staging environment.
```bash
git add index.html
```
```bash
git status
```
## Git Add More than One File  (bluestyle.css)
```bash
body {
background-color: lightblue;
}

h1 {
color: navy;
margin-left: 20px;
}
```
+ Now add all files in the current directory to the Staging Environment:
```bash
git statusgit add --all
```
+ Using --all instead of individual filenames will stage all changes (new, modified, and deleted) files.

## Git Commit
+ Since we have finished our work, we are ready move from stage to commit for our repo.
+ Adding commits keep track of our progress and changes as we work. Git considers each commit change point or "save point". It is a point in the project you can go back to if you find a bug, or want to make a change.
+ When we commit, we should always include a message.
+ By adding clear messages to each commit, it is easy for yourself (and others) to see what has changed and when.
```bash
git commit -m "First release of Hello World!"
```
