# README

Quick git summary

## First-time config after installation

```shell
# associate git commits with your name
$ git config --global user.name "your-name"

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

## Commits

1. [Create a new repo](https://help.github.com/articles/create-a-repo/)

  ```shell
  $ git clone https://github.com/username/repo-name.git
  $ cd repo-name
  ```

2. Create some files in `repo-name` locally.

   ```shell
   $ cd repo-name

   # review changes you've saved, but not yet committed
   $ git diff
   ```

3. Commit to this repo

  ```shell
  $ cd repo-name
  $ git add .
  $ git commit -m "your commit message"
  $ git push
  $ git status
  ```

## Logs

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

## Collaborate

### Tags

```shell
$ cd repo-name

# mark recent commit as important; used to annotate version releases
$ git tag -a v1.0 -m "version 1.0"

# tag a specific commit, say SHA1234
$ git tag -a v1.0 SHA1234 -m "version 1.0"

# see HEAD
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

# To merge with master
$ git checkout master
$ git merge new-branch-name
```

## Undo

```shell
$ cd repo-name

# edit most-recent commit messages or include/change committed files
$ git commit --amend

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
* [Git docs](https://git-scm.com/docs/)
* [GitHub help](https://help.github.com/)
