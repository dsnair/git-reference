# README

Quick git summary

## First-time Git Configuration after Installation

```shell
# associate git commits with your name
$ git config --global user.name "your-name"

# associate git commits with your email
$ git config --global user.email "username@email.com"

# color git output
git config --global color.ui auto

# display the original state in a conflict
git config --global merge.conflictstyle diff3

# set-up git with your text editor
# 1. Atom
git config --global core.editor "atom --wait"

# 2. Sublime
git config --global core.editor "'/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl' -n -w"

# review your current configuration
$ git config --list
```

## Commits

1. [Create a new repo](https://help.github.com/articles/create-a-repo/)

```shell
$ git clone https://github.com/username/repo-name.git
$ cd repo-name
```

2. Commit to this repo

Create some files in `repo-name`

```shell
$ git add .
$ git commit -m "your commit message"
$ git push
$ git status
```

## Logs

```shell
$ cd repo-name

# see SHA, author, date, commit messages
$ git log

# see 1st 7 SHA characters and commit messages only
$ git log --oneline

# see SHA, author, date, commit messages, summary of file names that were modified and # of lines added/removed in them
$ git log --stat

# see SHA, author, date, commit messages, what exact lines were added/removed in all files
$ git log --patch

# git log --patch output for only a single SHA, say 1234567
$ git show 1234567
```

## Reference

* [Udacity: Version Control with Git](https://www.udacity.com/course/version-control-with-git--ud123)
* [Git docs](https://git-scm.com/docs/)
