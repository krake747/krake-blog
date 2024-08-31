---
hide:
  - toc
tags:
  - Git
---

# Git Basics

Installing [Git]([Git](https://git-scm.com/)) version control.

## Setup

| Command                                    | Purpose                                          |
| ------------------------------------------ | ------------------------------------------------ |
| `git`                                      | List all available Git commands                  |
| `git config`                               | Configure Git settings (`--local` or `--global`) |
| `git config --global user.name "<name>"`   | Set the global Git username                      |
| `git config --global user.email "<email>"` | Set the global Git email address                 |
| `git config --global --list`               | Display the global Git configuration settings    |

## Git Fundamentals

| Command                        | Purpose                                                                |
| ------------------------------ | ---------------------------------------------------------------------- |
| `git init`                     | Initialize a new local repository, creating a `.git` folder            |
| `git status`                   | Display the current status of the repository                           |
| `git add <filename>`           | Add a specified file from the working directory to the staging area    |
| `git add .`                    | Add all files from the current directory and subfolders to staging     |
| `git add -A`                   | Add all files from the root directory to staging                       |
| `git commit -m "<message>"`    | Commit staged changes to the local repository with a message [^1]      |
| `git log`                      | View the commit history                                                |
| `git log --oneline`            | View a condensed version of the commit history                         |
| `git reset HEAD~1`             | Undo the last commit, removing it from history                         |
| `git revert <SHA>`             | Revert a specific commit while preserving the history                  |
| `git commit --amend --no-edit` | Add staged changes to the previous commit without changing the message |

[^1]: A commit is like a save point and is identified by a unique SHA hash.

## Git Branching

| Command                         | Purpose                                                             |
| ------------------------------- | ------------------------------------------------------------------- |
| `git stash`                     | Temporarily save changes without committing                         |
| `git stash list`                | Display all stashed changes                                         |
| `git stash pop`                 | Reapply stashed changes and remove from stash                       |
| `git stash apply`               | Reapply stashed changes without removing from stash                 |
| `git stash -u`                  | Stash changes, including untracked files                            |
| `git clean -f`                  | Force delete untracked files in the working directory               |
| `git clean -fd`                 | Force delete untracked files, directories, and subfolders           |
| `git reset --hard`              | Reset tracked files to the last commit state                        |
| `git checkout -b <branch_name>` | Create and switch to a new branch                                   |
| `git checkout <branch_name>`    | Switch to an existing branch                                        |
| `git merge <branch_name>`       | Merge `<branch_name>` into the current branch                       |
| `git branch --list`             | List all local branches                                             |
| `git branch -d <branch_name>`   | Delete the specified branch (if merged)                             |
| `git branch -D <branch_name>`   | Force delete the specified branch                                   |
| `git cherry-pick <commit>`      | Apply a specific commit from another branch onto the current branch |

What is the `HEAD`? 

`HEAD` refers to the latest commit that your current branch is pointing to. 
It's essentially a reference to the current branch, indicating where you are in the commit history.

## 