# README

## First-time config after installation

```shell
# associate git commits with your name
$ git config --global user.name "your name"

# associate git commits with your email
$ git config --global user.email "username@email.com"

# save login credentials
$ git config --global credential.helper store
# git config --global credential.helper cache

# files to ignore in every git repo on your computer
$ git config --global core.excludesfile ~/.gitignore

# set-up git with your text editor
  # 1. Atom
$ git config --global core.editor "atom --wait"
  # 2. Sublime
$ git config --global core.editor "'/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl' -n -w"

# color git output
$ git config --global color.ui auto

# display the original state in a conflict
$ git config --global merge.conflictstyle diff3

# review your current configuration
$ git config --list
```

## 1. Create New Repo

### On GitHub

[Create a new repo](https://help.github.com/articles/create-a-repo/)

```shell
$ git clone https://github.com/username/repo-name.git
$ cd repo-name
```

Create some files in _repo-name_ locally.

 ```shell
 # review changes you've saved, but not yet committed
 $ git diff

 $ git add .
 $ git commit -m "your commit message"
 $ git push

 $ git status
 ```

### From Command Line

[Create a new empty repo](https://help.github.com/articles/create-a-repo/). Don't initialize with a README and license.

```shell
$ mkdir repo-name
$ cd repo-name

# convert this directory into a Git repo
$ git init
```

Create some files in _repo-name_ locally.

`git remote` allows you to manage and interact with remote repositories. `origin` is an alias for the full URL path to the remote repo https://github.com/USER_NAME/REPO_NAME.git. To view this full path, `git remote -v`.

```shell
$ git add .
$ git commit -m "your commit message"

# create an alias 'origin' that points to a project on GitHub
$ git remote add origin https://github.com/USER_NAME/REPO_NAME.git

# push local changes to origin's master branch & add upstream tracking reference for every branch (-u)
$ git push -u origin master

# origin/master means that local branch is tracking master branch on remote origin
$ git log --oneline --graph --all
```

## 2. File management

```shell
$ cd repo-name

# remove file locally and from remote repo
$ git rm file-name

# remove file from remote repo, but not locally
$ git rm --cached file-name

$ git commit -m "your commit message"
$ git push
```

## 3. Logs

```shell
$ cd repo-name

# see SHA (commit ID), author, date, commit messages, current HEAD
$ git log
# git log --decorate

# list SHA (7-characters), commit messages, current HEAD
$ git log --oneline

# see SHA, author, date, commit messages, current HEAD, modified files and # of lines added/removed in them
$ git log --stat

# see SHA, author, date, commit messages, current HEAD, what exact lines were added/removed in all files
$ git log --patch

# git log --patch output for only a single 7-characters SHA, say SHA1234
$ git show SHA1234
```

## 4. Version Control

### Tags

```shell
$ cd repo-name

# mark recent commit as important; used to annotate (-a) version releases
$ git tag -a v1.0 -m "version 1.0"

# tag a specific commit, say SHA1234
$ git tag -a v1.0 SHA1234 -m "version 1.0"

# see HEAD and branches
$ git log --oneline

# delete tag
$ git tag -d v1.0
```

### Branches

Branches allow you to test a different version of your code without affecting the master.
If you like this version, merge all branches together. If you dislike it, delete those branches.

```shell
$ cd repo-name

# list all branches in a repo; * indicates the active branch
$ git branch

# create a new branch  
$ git branch branch-name

# switch to a specific branch to make commits there
$ git checkout branch-name

# create and switch to a new branch starting at the most recent commit in master (fast forward merging).
# This copies the entire state (committed/uncommitted files) of the master branch to the new branch.
$ git checkout -b branch-name master

# create and switch to a new branch starting at a previous commit (divergent merging)
$ git checkout -b branch-name2 SHA1234

# shift the tip of branch-name to the most recent commit on master
$ git rebase master branch-name

# view branches (--graph) all at once (--all)
$ git log --oneline --graph --all

# delete a local branch
$ git branch -d branch-name

# delete a remote branch
$ git push origin --delete remote-branch-name
```

### Merge

1. Merge a Branch with Master

  ```shell
  $ cd repo-name

  # find out where the HEAD is pointing
  $ git log --oneline

  # To merge a branch with master
  $ git checkout master
  $ git merge new-branch-name
  $ git push
  ```

2. Merge project-a into project-b with its history

  ```shell
  $ cd path/to/project-b
  $ git remote add project-a https://github.com/USERNAME/project-a.git
  $ git fetch project-a
  $ git merge --allow-unrelated-histories project-a/master # or whichever branch you want to merge
  $ git remote remove project-a
  ```

## 5. Collaborate

### Push/Pull

```shell
# push local repo's changes up to remote origin's master branch
$ git push origin master

# pull changes down from remote origin's master branch to local branch
$ git pull origin master
```

### Fetch

If the remote origin has some changes that the local repo doesn't have and vice-versa, then do a `git fetch`. It pulls changes from remote origin's branch, but (unlike git pull) it _does not_ automatically merge the local branch with the remote tracking branch after receiving the changes. This is to prevent a merge conflict. After receiving remote changes, commit your local changes and then manually merge the local branch with the remote tracking branch. Now that the local repo has all the changes, push them to the remote origin.

```shell
$ git fetch origin master
$ git add .
$ git commit -m "your commit message"
$ git merge origin/master
$ git push origin master
```

### Fork

Fork makes an identical copy of a _remote_ repo. This copy is also a _remote_ repo and you're it's owner. Whereas, cloning makes an identical copy of a _remote_ repo onto a _local_ machine.

`origin` = connection between local repo and remote forked repo  
`upstream` = connection between local repo and remote source repo that was forked

1. Sync Forked Repo Locally

  ```shell
  $ cd repo-name

  # create connection between local repo and source repo that was forked
  $ git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git

  # fetch branches and commits from upstream repo
  $ git fetch upstream

  # switch to local master branch
  $ git checkout master

  # merge changes from upstream/master to local master
  $ git merge upstream/master
  ```

2. Update Forked Repo on GitHub

  ```shell
  $ git push origin master
  ```
  
When you fork a repo with multiple, remote branches

```shell
$ git branch -a
$ git checkout branch-name
```
shows all remote branches and allows you to checkout one of them to begin work locally. 

### Logs

```shell
# see how many commits each contributor made
$ git shortlog

# -n sorts # commits numerically (rather than alphabetically by contributor name)
# -s prints total # commits for each contributor (rather than individual commit messages)
$ git shortlog -s -n

# filter commits by author name
$ git log --author="author name"

# filter by commits referencing specific words
$ git log --grep="search words"
```

## 6. Edit Commits

```shell
$ cd repo-name

# move commit/content to working directory; default
$ git reset --mixed SHA1234  # or, git reset --mixed HEAD~n
$ git push -f origin master

# move commit/content to staging index, where n is ancestral ref from HEAD
$ git reset --soft SHA1234  # or, git reset --soft HEAD~n
$ git push -f origin master

# erase commit/content
$ git reset --hard SHA1234  # or, git reset --hard HEAD~n
$ git push -f origin master # needs force push (-f) since deleting content

# stash away local dirty changes, do something, release stash
$ git stash --include-untracked
$ git stash pop

# edit last commit message or include/change last committed files
$ git commit --amend -m "your commit message"

# squash/combine n commits together; -i interactive
$ git rebase -i HEAD~n
$ git push -f

# (make a new commit to) reverse a commit/content
$ git revert SHA1234
```

## Reference

* [Udacity: Version Control with Git](https://www.udacity.com/course/version-control-with-git--ud123)
* [Udacity: Github & Collaboration](https://www.udacity.com/course/github-collaboration--ud456)
* [Git docs](https://git-scm.com/docs/)
* [GitHub help](https://help.github.com/)
