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

## Initialize Git
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

- `Tracked` - files that Git knows about and are added to the repository
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
git status
git add --all
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
+ If you are having trouble remembering commands or options for commands, you can use `git help`.

+ There are a couple of different ways you can use the help command in command line:

**git command -help** -  See all the available options for the specific command
**git help --all** -  See all possible commands

# Git Branch

+ In Git, a branch is a new/separate version of the main repository.

Let's say you have a large project, and you need to update the design on it.

Make copies of all the relevant files to avoid impacting the live version
Start working with the design and find that code depend on code in other files, that also need to be changed!
Make copies of the dependant files as well. Making sure that every file dependency references the correct file name
`EMERGENCY!` There is an unrelated error somewhere else in the project that needs to be fixed ASAP!
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

## New Git Branch
Let add some new features to our *index.html* page.

We are working in our local repository, and we do not want to disturb or possibly wreck the main project.

So we create a new branch:
```sh
git branch dev_hello-world
```
Now we created a new branch called "dev_hello-world"

Let's confirm that we have created a new branch:

**Example**
git branch
  dev_hello-world
* master
We can see the new branch with the name "dev_hello-world", but the * beside master specifies that we are currently on that branch.

checkout is the command used to check out a branch. Moving us from the current branch, to the one specified at the end of the command:

```sh
git checkout dev_hello-world
```
Switched to branch 'dev_hello-world'
Now we have moved our current workspace from the master branch, to the new branch

Open your favourite editor and make some changes.

For this example, we added an image (img_hello_world.jpg) to the working folder and a line of code in the `index.html` file:
```sh
<!DOCTYPE html>
<html>
<head>
<title>Hello World!</title>
<link rel="stylesheet" href="bluestyle.css">
</head>
<body>

<h1>Hello world!</h1>
<div><img src="img_hello_world.jpg" alt="Hello World from Space"
style="width:100%;max-width:960px"></div>
<p>This is the first file in my new Git Repo.</p>
<p>A new line in our file!</p>

</body>
</html>
```

```sh
git add --all
git status
```
+ We are happy with our changes. So we will commit them to the branch:
```sh
git commit -m "Added image to Hello World"
```
+ Now we have a new branch, that is different from the master branch

## Switching Between Branches
+ Now let's see just how quick and easy it is to work with different branches, and how well it works.
+ We are currently on the branch hello-world-images. We added an image to this branch, so let's list the files in the current directory:

`ls`
`README.md` `bluestyle.css` `img_hello_world.jpg` `index.html`     
+ We can see the new file img_hello_world.jpg, and if we open the html file, we can see the code has been altered. All is as it should be.

+ Now, let's see what happens when we change branch to master
```sh
git checkout master
```
+ The new image is not a part of this branch. List the files in the current directory again:
**ls**
+ `img_hello_world.jpg` is no longer there! And if we open the html file, we can see the code reverted to what it was before the alteration.

See how easy it is to work with branches? And how this allows you to work on different things?

### Emergency Branch
Now imagine that we are not yet done with hello-world-images, but we need to fix an error on master.

I don't want to mess with master directly, and I do not want to mess with hello-world-images, since it is not done yet.

So we create a new branch to deal with the emergency:
```sh
git checkout -b emergency-fix
```
Switched to a new branch 'emergency-fix'
Now we have created a new branch from master, and changed to it. We can safely fix the error without disturbing the other branches.

Let's fix our imaginary error:

```sh
<!DOCTYPE html>
<html>
<head>
<title>Hello World!</title>
<link rel="stylesheet" href="bluestyle.css">
</head>
<body>

<h1>Hello world!</h1>
<p>This is the first file in my new Git Repo.</p>
<p>This line is here to show how merging works.</p>

</body>
</html>
```
+ We have made changes in this file, and we need to get those changes to the master branch.

Check the status:
```sh
git status
```
```sh
git add index.html
```

# Merge Branches
+ We have the emergency fix ready, and so let's merge the `master` and `emergency-fix branches`.
+ First, we need to change to the master branch:
```sh
git checkout master
```
+ Now we merge the current branch (master) with emergency-fix:
```sh
git merge emergency-fix
```
+ Since the emergency-fix branch came directly from master, and no other changes had been made to master while we were working, Git sees this as a continuation of master. So it can "Fast-forward", just pointing both master and emergency-fix to the same commit.
+ As master and emergency-fix are essentially the same now, we can delete emergency-fix, as it is no longer needed:
```sh
git branch -d emergency-fix
```
# Merge Conflict
Now we can move over to hello-world-images and keep working. Add another image file (img_hello_git.jpg) and change index.html, so it shows it:
```sh
git checkout hello-world-images
```
```sh
<!DOCTYPE html>
<html>
<head>
<title>Hello World!</title>
<link rel="stylesheet" href="bluestyle.css">
</head>
<body>

<h1>Hello world!</h1>
<div><img src="img_hello_world.jpg" alt="Hello World from Space" style="width:100%;max-width:960px"></div>
<p>This is the first file in my new Git Repo.</p>
<p>A new line in our file!</p>
<div><img src="img_hello_git.jpg" alt="Hello Git" style="width:100%;max-width:640px"></div>

</body>
</html>
```
Now, we are done with our work here and can stage and commit for this branch:

```sh
git add --all
git commit -m "added new image"
```
+ We see that index.html has been changed in both branches. Now we are ready to merge hello-world-images into master. But what will happen to the changes we recently made in master?
```sh
git checkout master
git merge hello-world-images
```
+ The merge failed, as there is conflict between the versions for index.html. Let us check the status:
 ```sh 
git status
```
+ This confirms there is a conflict in index.html, but the image files are ready and staged to be committed.
+ So we need to fix that conflict. Open the file in our editor:
+ Now we can stage index.html and check the status:
 ```sh 
git add index.html
git status
```

+ The conflict has been fixed, and we can use commit to conclude the merge:
 ```sh
git commit -m "merged with hello-world-images after fixing conflicts"
```
+ And delete the hello-world-images branch:
 ```sh
git branch -d hello-world-images
```
+ Now you have a better understanding of how branches and merging works. Time to start working with a remote repository!

# Git GitHub Getting Started
https://www.github.com/
## Create a Repository on GitHub
+ Now that you have made a GitHub account, sign in, and create a new Repo:
+ Push Local Repository to GitHub
+ Since we have already set up a local Git repo, we are going to push that to GitHub:
```sh
git remote add origin 
```
**git remote add origin URL** specifies that you are adding a remote repository, with the specified `URL`, as an `origin` to your local Git repo.

+ Now we are going to push our master branch to the origin url, and set it as the default remote branch:
```sh
git push --set-upstream origin master
```
+ Now, go back into GitHub and see that the repository has been updated:

# Pulling to Keep up-to-date with Changes
## Pulling to Keep up-to-date with Changes
+ When working as a team on a project, it is important that everyone stays up to date.
+ Any time you start working on a project, you should get the most recent changes to your local copy.

With Git, you can do that with `pull`.

**Pull** is a combination of 2 different commands:

+ **fetch**
+ **merge**
Let's take a closer look into how fetch, merge, and pull works.

## Git Fetch
`fetch`gets all the change history of a tracked branch/repo.

So, on your local Git, `fetch` updates to see what has changed on GitHub:

```sh
git fetch origin
```
Now that we have the recent changes, we can check our status:

```sh
git status
```
We are behind the origin/master by 1 commit. That should be the updated `README.md` , but lets double check by viewing the log:

```sh
git log origin/master
```
+ That looks as expected, but we can also verify by showing the differences between our local master and `origin/master`:

```sh
git diff origin/master
```
That looks precisely as expected! Now we can safely merge.

## Git Merge
+ merge combines the current branch, with a specified branch.
+ We have confirmed that the updates are as expected, and we can merge our current branch (master) with origin/master:
```sh
git merge origin/master
```
Check our status again to confirm we are up to date:
## Git Pull
+ But what if you just want to update your local repository, without going through all those steps?
+ pull is a combination of fetch and merge. It is used to pull all changes from a remote repository into the branch you are working on.
+ Make another change to the Readme.md file on GitHub.
```sh
git pull origin
```


