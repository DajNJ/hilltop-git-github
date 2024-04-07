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
## Git Commit Log
To view the history of commits for a repository, you can use the log command:
```bash
git log
```

## Git Help
+ If you are having trouble remembering commands or options for commands, you can use Git help.

+ There are a couple of different ways you can use the help command in command line:

**git command -help** -  See all the available options for the specific command
**git help --all** -  See all possible commands

# Git Branch

+ In Git, a branch is a new/separate version of the main repository.

Let's say you have a large project, and you need to update the design on it.

Make copies of all the relevant files to avoid impacting the live version
Start working with the design and find that code depend on code in other files, that also need to be changed!
Make copies of the dependant files as well. Making sure that every file dependency references the correct file name
EMERGENCY! There is an unrelated error somewhere else in the project that needs to be fixed ASAP!
Save all your files, making a note of the names of the copies you were working on
Work on the unrelated error and update the code to fix it
Go back to the design, and finish the work there
Copy the code or rename the files, so the updated design is on the live version
(2 weeks later, you realize that the unrelated error was not fixed in the new design version because you copied the files before the fix)

With Git:

With a new branch called new-design, edit the code directly without impacting the main branch
EMERGENCY! There is an unrelated error somewhere else in the project that needs to be fixed ASAP!
Create a new branch from the main project called small-error-fix
Fix the unrelated error and merge the small-error-fix branch with the main branch
You go back to the new-design branch, and finish the work there
Merge the new-design branch with main (getting alerted to the small error fix that you were missing)
Branches allow you to work on different parts of a project without impacting the main branch.

When the work is complete, a branch can be merged with the main project.

You can even switch between branches and work on different projects without them interfering with each other.

Branching in Git is very lightweight and fast!

New Git Branch
Let add some new features to our index.html page.

We are working in our local repository, and we do not want to disturb or possibly wreck the main project.

So we create a new branch:

Example
git branch hello-world-images
Now we created a new branch called "hello-world-images"

Let's confirm that we have created a new branch:

Example
git branch
  hello-world-images
* master
We can see the new branch with the name "hello-world-images", but the * beside master specifies that we are currently on that branch.

checkout is the command used to check out a branch. Moving us from the current branch, to the one specified at the end of the command:

Example
git checkout hello-world-images
Switched to branch 'hello-world-images'
Now we have moved our current workspace from the master branch, to the new branch

Open your favourite editor and make some changes.

For this example, we added an image (img_hello_world.jpg) to the working folder and a line of code in the index.html file:
