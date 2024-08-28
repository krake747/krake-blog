---
hide:
  - toc
tags:
  - Git
---

# Git Basics

Installing [https://git-scm.com/](Git) version control.

## Setup

| Command                                    | Purpose                               |
| ------------------------------------------ | ------------------------------------- |
| `git`                                      | list all git commands                 |
| `git config`                               | configure git `--local` or `--global` |
| `git config --global user.name "<name>"`   | configure global user name            |
| `git config --global user.email "<email>"` | configure global user email           |
| `git config --global --list`               | lists `global` git configuration      |

## Git Fundamentals

| Command                        | Purpose                                                              |
| ------------------------------ | -------------------------------------------------------------------- |
| `git init`                     | creating a local repository creates a `.git` folder                  |
| `git status`                   | gives the status or state of git repository                          |
| `git add <filename>`           | add a named file from working directory (wd) to staging              |
| `git add .`                    | adds all files from current wd and subfolder down to staging         |
| `git add -A`                   | adds all files from root wd to staging                               |
| `git commit -m "<message>"`    | add a git message and commit from staging to local repository [^1]   |
| `git log`                      | view git history                                                     |
| `git log --oneline`            | view git history in one line                                         |
| `git reset HEAD~1`             | Will undo last commit and change history as if commit never happened |
| `git revert <SHA>`             | Will undo last commit and keep history (`vim :wq`)                   |
| `git commit --amend --no-edit` | Add changes from staging area to previous commit (changes SHA)       |

[^1]: A commit is like a save point and is identified by a unique SHA hash.

## Git Branching