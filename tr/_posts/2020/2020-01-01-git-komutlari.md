---
layout: post
title: "Git Komutları"
date: 2020-01-02 02:38:19 Thursday
author: semih
comments: true
lang: tr
lang-ref: git-commands
categories: [git]
tags: [git, source control management, scm]
---
We have numerous sources and manage it using source control management(SCM) DevOps tools like Git, SubVersion, CVS, TFS, ClearCase, Mercurial. Git is a modern distributed version control system. I am going to tell you most useful Git commands and why we need to use those commands. I will explain each step with examples.
<br/>

There are 3 states of Git.
- Working directory
- Staging area (pre-commit holding area)
- Commit (git repository, history)

<br/>
![Basic Git Workflow Life Cycle](/assets/images/basic-git-workflow-lifecycle.png)

<br/>
### Configuration
If Git is installed in our pc, it tells us the version.
```shell
~ $ git version
   git version 2.17.2
```
git global user name and email configuration
```shell
~ $ git config --global user.name "username"
~ $ git config --global user.email "email"
~ $ git config --global --list
```
<br/>
### Demo App
Now let's make a demo app and run the first commands on git. At first, create a repository on Github with the name of "github-repo". Then, clone this repository into your local workspace folder.

Clone the remote repository into your local folder.
```shell
~ $ git clone https://github.com/semih/github-demo.git
~ $ cd github-demo/
```
Add README.md file and commit it.
```shell
~ $ git init
~ $ git add README.md
~ $ git commit -m "first commit"
```

Push your files that you have added or modified into the remote branch.
```shell
~ $ git remote add origin https://github.com/semih/github-demo.git
~ $ git push -u origin master
```

We have created a file and wrote something into it. We will see the branch that we worked on it and we use the "git status" command to see if there are any changes between the working directory, the staging area, our local repository and remote repository. We have to use "git add <file>..." command to track.
```shell
~ $ echo "Test Git Quick Start Demo" >> start.txt
~ $ ls
.git		README.md	start.txt
~ $ cat start.txt
Test Git Quick Start Demo
~ $ git status
On branch master
Your branch is up to date with 'origin/master'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	start.txt
nothing added to commit but untracked files present (use "git add" to track)
```

After running "git add <file>..." command, git tells us there is a new file in staging area which Git describes as "Changes to be commited". The file is in the staging area awaiting the commit.
```shell
~ $ git add start.txt 
~ $ git status
On branch master
Your branch is up to date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
	new file:   start.txt
```

We execute the "git commit" command and check the status again. As a result, the new file has been moved from staging area into the local repository. Because of there are no other pending changes, Git marks the working directory as clean. But our file is not yet on Github.
```shell
~ $ git add .
~ $ git commit -m "git-commands"
[master 2cd0af0] git-commands
 1 file changed, 1 insertion(+)
 create mode 100644 start.txt
~ $ git status
On branch master
Your branch is up to date with 'origin/master'.
nothing to commit, working tree clean
```

There is one last step we need to do, and that is a push. We need to execute "git push origin master" command. "origin" refers to the Github copy of our repository. "master" refers to branch name in the repository. If we did everything correctly, our new file should be on the Github copy of our repository.
```shell
~ $ git push origin master
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 299 bytes | 299.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/semih/github-demo.git
   785389b..2cd0af0  master -> master
```
<br/>
### Basic Git Commands
- Starting a Project
	- Fresh (no source yet)
	- Existing source locally
	- Github project (fork and clone)
- Basic Workflow (add, commit, push, pull)
- Working with files (rename, move & delete)
- History and Aliases
- Ignoring Unwanted Files

<br/>
#### Starting a Project (Fresh)
Create a new project with "git init command
```shell
workspace $ git init fresh-project
Initialized empty Git repository in /Users/semih/workspace/fresh-project/.git/
workspace $ ls
fresh-project
workspace $cd fresh-project/
fresh-project $ ls -al
total 0
drwxr-xr-x  3 semih  staff   96  7 Oca 00:58 .
drwxr-xr-x  6 semih  staff  192  7 Oca 00:58 ..
drwxr-xr-x  9 semih  staff  288  7 Oca 00:58 .git
fresh-project $cd .git/
.git $ls
HEAD		description	info		refs
config		hooks		objects
```

Git status command tells us that we are on the master branch.
```shell
.git $ cd ..
fresh-project $ git status
On branch master
No commits yet
nothing to commit (create/copy files and use "git add" to track)
```

Git caught the untracked files:
```shell
fresh-project $ mate hipster.txt
fresh-project $ git status
On branch master
No commits yet
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	hipster.txt
nothing added to commit but untracked files present (use "git add" to track)
```

Changes to be committed means this new file "hipster.txt", is now in the Git staging area. We have a file that's waiting to be committed, but it's not committed yet.
```shell
fresh-project $ git add hipster.txt 
fresh-project $ git status
On branch master
No commits yet
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   hipster.txt
```

If we write only "git commit", our editor lists changes to be committed and i can type the commit message on the top lines of file and save it.
```shell
fresh-project $ git commit (file is opening here with our default text editor)
[master (root-commit) 2296291] Adding new file
 1 file changed, 1 insertion(+)
 create mode 100644 hipster.txt
fresh-project $ git status
On branch master
nothing to commit, working tree clean
```
<br/>
#### Starting a Project (Existing source locally)
"git init" command is executed in the project folder.
First of all we see the untracked files. `git add .` command sends files to the staging area, commit them using "git commit" command and push them using "git push" command as well.

```shell
project-folder $ git init
Initialized empty Git repository in /Users/semih/workspace/initializr/.git/
project-folder $ git status
On branch master
No commits yet
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.htaccess
	404.html
	apple-touch-icon.png
	browserconfig.xml
	crossdomain.xml
	css/
	favicon.ico
	fonts/
	humans.txt
	index.html
	js/
	robots.txt
	tile-wide.png
	tile.png
nothing added to commit but untracked files present (use "git add" to track)
project-folder $ git add .
project-folder $ git commit -m "my first commit message"
```
<br/>
#### Starting a Project (Fork and clone)
This part is about how to join an existing project on Github.
Click fork button on the github page (https://github.com/scm-ninja/starter-web)
Finally, the following `git clone` command are executed.

```shell
~ $ git clone https://github.com/semih/starter-web.git
Cloning into 'starter-web'...
remote: Enumerating objects: 39, done.
remote: Total 39 (delta 0), reused 0 (delta 0), pack-reused 39
Unpacking objects: 100% (39/39), done.
~ $ cd starter-web
starter-web $ 
starter-web $ ls
404.html				fonts
README.md				humans.txt
apple-touch-icon-precomposed.png	index.html
crossdomain.xml				js
css					robots.txt
favicon.ico				simple.html
```
<br/>
#### Basic Workflow (stage a file)
* `git add -A`
* `git add -U`

<br/>
#### Basic Workflow (unstage a file)
As known, we move the files to staging area using git add command. Sometimes we shouldn't really move these files or we may have moved it by mistake. All we need to do is using `git reset HEAD <file>...` command to unstage as the terminal says.
Also `git checkout -- <file>...` command cleans the working directory and discard the changes.

<br/>
#### Working with files (delete a file)
`git rm <file>...`
We can undo the deleted file using `git reset HEAD <file>...`
and `git checkout -- <file>...` commands in order.

<br/>
#### Working with files (delete a folder)
`git rm -rf <folder>...`

<br/>
#### Git History
* `git help log`
* `git log`
* `git log --abbrev-commit`
* `git log --oneline --graph --decorate`
* `git log --all --graph --decorate --oneline`
* `git log --since="3 days ago"`
* `git log -- <file>`
* `git log --follow -- <file>`

<br/>
#### Git Aliases
After running this command, `git hist` shortcut should be used.
`git config --global alias.hist "log --all --graph --decorate --oneline"`
And the shortcuts could be checked from .gitconfig file.

`mate ~/.gitconfig`
<br/>
#### Ignoring Unwanted Files and Folders
We don't want to push some files like .DS Store. `ls -al` command lists all files, including the dot files and folders. We have to create a ".gitignore" file, if we don't. We can create it with `mate .gitignore` command and save it. Again we have to write .DS_Store into this file. Afterwards, we add it with `git add .gitignore` command. 

Besides, we can use * statement in the .gitignore file. For example, we might have log files which they have .log extension. If we don't want to push those files, we can extract it with *.log statement. 

or when we have log folder in workspace and we don't want to push any files in the log folder, we should add directly `log/` row in .gitignore file. After running the following commands, it appears that log folder is not pushed.

* `git add .`
* `git status`
* `git commit -am "Excluding log file directory"`


[Download source](/assets/files/BasicWorkflow.pdf)<br/>
If you like this post, please leave a review! <br/>
Hope to see you in the next article...