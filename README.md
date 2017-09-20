# README

Quick git summary

## First-time config after installation

```shell
# associate git commits with your name
$ git config --global user.name "your name"

# associate git commits with your email
$ git config --global user.email "username@email.com"

# color git output
$ git config --global color.ui auto

# display the original state in a conflict
$ git config --global merge.conflictstyle diff3

# set-up git with your text editor
  # 1. Atom
$ git config --global core.editor "atom --wait"
  # 2. Sublime
$ git config --global core.editor "'/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl' -n -w"

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

# look for origin/master. It means that local branch is tracking master branch on remote origin
$ git log --oneline --graph --decorate --all
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

# see SHA (commit ID), author, date, commit messages
$ git log

# list SHA (7-characters) and commit messages
$ git log --oneline

# see SHA, author, date, commit messages, modified files and # of lines added/removed in them
$ git log --stat

# see SHA, author, date, commit messages, what exact lines were added/removed in all files
$ git log --patch

# git log --patch output for only a single 7-characters SHA, say SHA1234
$ git show SHA1234

# see SHA, author, date, commit messages, current HEAD
$ git log --decorate
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
$ git log --oneline --decorate

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
$ git branch new-branch-name

# switch to a specific branch to make commits there
$ git checkout new-branch-name

# create and switch to a new branch starting at the same location as master (fast forward merging)
$ git checkout -b new-branch-name master

# create and switch to a new branch starting at a previous commit (divergent merging)
$ git checkout -b new-branch-name2 SHA1234

# view branches (--graph) all at once (--all)
$ git log --oneline --decorate --graph --all

# delete a branch
$ git branch -d new-branch-name2
```

### Merges

```shell
$ cd repo-name

# find out where the HEAD is pointing
$ git log --oneline --decorate

# To merge a branch with master
$ git checkout master
$ git merge new-branch-name
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

If the remote origin has some changes that the local repo doesn't have and vice-versa, then do a `git fetch`. It pulls changes from remote origin's branch, but (unlike git pull) it _does not_ automatically merge the local branch with the remote tracking branch after receiving the changes. This is to prevent a merge conflict. After receiving remote changes, manually merge the local branch with the remote tracking branch. Now that the local repo has all the changes, push them to the remote origin.

```shell
$ git fetch origin master
$ git merge origin/master
$ git push origin master
```

### Fork

1. Sync Fork Locally

  ```shell
  $ cd repo-name

  # list remote repo for the fork
  $ git remote -v

  # specify new remote upstream repo that the fork will be synced with
  $ git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git

  # verify upstream repo
  $ git remote -v

  # fetch branches and commits from upstream repo
  $ git fetch upstream

  $ git checkout master

  # merge chages from upstream/master to your local master
  $ git merge upstream/master
  ```

2. Update Fork on github

  ```shell
  $ git push origin master
  ```

## 6. Undo

```shell
$ cd repo-name

# edit most-recent commit messages or include/change committed files
$ git commit --amend -m "your commit message"

# (make a new commit to) reverse a commit/content
$ git revert SHA1234

# move commit/content to working directory; default
$ git reset --mixed HEAD~n

# move commit/content to staging index, where n is ancestral ref from HEAD
$ git reset --soft HEAD~n

# erase commit/content
$ git reset --hard HEAD~n
```

## Reference

* [Udacity: Version Control with Git](https://www.udacity.com/course/version-control-with-git--ud123)
* [Udacity: Github & Collaboration](https://www.udacity.com/course/github-collaboration--ud456)
* [Git docs](https://git-scm.com/docs/)
* [GitHub help](https://help.github.com/)
