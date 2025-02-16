# GIT: Basics

## Starting a new project

This is done once, at the beginning of a project.

```bash
mkdir new_project
cd new_project
git init
```

To retrieve an existing Github repository and download it to your computer you'll need to clone it:

```bash
# Generic command
git clone <github_ssh_clone_url>

git clone git@github.com:username/existing_project.git
cd existing_project
```

## Useful commands

Check the difference between now and last commit:

```bash
# Which files have been changed?
git status

# Which lines have changed since last commit?
git diff
```

How to commit something:

```bash
# First select the files to be commited
git add <file_1_which_has_been_modified_or_created>
git add <file_2_which_has_been_modified_or_created>

# or select all the files in current directory
git add .

# Commit your work with a meaningfull message
git commit -m "Why I did this change"
```

> Reference: [How to write a git commit message](https://chris.beams.io/posts/git-commit/)

Send your code to GitHub:

```
# Generic command
git push <remote> <branch>

# Most of the time we do:
git push origin master
```

Project history:

```
# See the list of all the commits that have been done so far.
git log

# More fancy command (check your ~/.gitconfig)
git lg
```
