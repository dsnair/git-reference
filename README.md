### First-time Git configuration after installation

```shell
# associate git commits with your name
git config --global user.name "your-name"

# associate git commits with your email
git config --global user.email "your-email"

# color git output
git config --global color.ui auto

# display the original state in a conflict
git config --global merge.conflictstyle diff3

# set-up git with your text editor

# Atom
git config --global core.editor "atom --wait"

# Sublime
git config --global core.editor "'/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl' -n -w"

# view your current configuration
git config --list
```

### Create a new, empty repo

```shell
mkdir your-repo-name
cd your-repo-name
git init
```

## Reference

[Udacity: Version Control with Git](https://www.udacity.com/course/version-control-with-git--ud123)
