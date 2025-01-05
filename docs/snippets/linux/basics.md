---
hide:
    - toc
tags:
    - Git
---

# Linux Basics

## Essential Commands

### List Directory Contents

| Command  | Purpose                                          |
| -------- | ------------------------------------------------ |
| `ls`     | Lists the contents of the current directory      |
| `ls -sS` | Lists files sorted by size and shows their sizes |
| `ls -l`  | Displays detailed information about files        |
| `ls -a`  | Shows hidden files (files starting with a dot)   |
| `ls -lh` | Lists files with human-readable sizes            |

### Change Directory

| Command                 | Purpose                           |
| ----------------------- | --------------------------------- |
| `cd <name>`             | Navigate to a specified directory |
| `cd ..`                 | Move up one directory level       |
| `cd -`                  | Switch to the previous directory  |
| `cd ~`                  | Return to the home directory      |
| `cd /path/to/directory` | Jump directly to an absolute path |

### Print Working Directory

| Command | Purpose                             |
| ------- | ----------------------------------- |
| `pwd`   | Displays the current directory path |

### Print to Standard Output

| Command                   | Purpose                                             |
| ------------------------- | --------------------------------------------------- |
| `echo <text>`             | Prints the specified text                           |
| `echo $PWD`               | Displays the current directory environment variable |
| `echo $USER`              | Displays the current user's username                |
| `echo "Hello" > file.txt` | Writes text to a file                               |

### Make a Directory

| Command                                 | Purpose                              |
| --------------------------------------- | ------------------------------------ |
| `mkdir <directory_name>`                | Creates a new directory              |
| `mkdir -p <path/to/dir>`                | Creates nested directories as needed |
| `mkdir -p projects/{project1,project2}` | Creates structured directories       |

### Create a New File

| Command                     | Purpose                                   |
| --------------------------- | ----------------------------------------- |
| `touch <file_name>`         | Creates an empty file                     |
| `touch existing_file.txt`   | Updates the timestamp of an existing file |
| `touch file1.txt file2.txt` | Creates multiple files at once            |

### Remove Files or Directories

| Command                              | Purpose                                         |
| ------------------------------------ | ----------------------------------------------- |
| `rm <file_name>`                     | Deletes a specified file                        |
| `rm -i`                              | Prompts for confirmation before deletion        |
| `rm -rf <directory_name>`            | Forcefully deletes a directory and its contents |
| `rm *.log`                           | Deletes all `.log` files in the directory       |
| `find . -name "*.tmp" -exec rm {} +` | Deletes files by criteria                       |

### Read File Contents

| Command                                            | Purpose                                  |
| -------------------------------------------------- | ---------------------------------------- |
| `cat <file_name>`                                  | Displays the contents of a file          |
| `cat <file_name> -n`                               | Displays file contents with line numbers |
| `cat file1 file2 > combined.txt`                   | Combines multiple files into one         |
| <code>cat /var/log/syslog &#124; grep error</code> | Example of searching for logs            |

### Copy Files or Directories

| Command                     | Purpose                         |
| --------------------------- | ------------------------------- |
| `cp <source> <destination>` | Copies a file to a new location |
| `cp -r src_dir dest_dir`    | Copies directories recursively  |
| `cp -u <file> backup/`      | Copies only newer files         |

### Move or Rename Files

| Command                                      | Purpose                 |
| -------------------------------------------- | ----------------------- |
| `mv <source> <destination>`                  | Moves or renames a file |
| `mv <file1> <file2> <destination_directory>` | Moves multiple files    |
| `mv old_dir new_dir`                         | Renames a directory     |
| `mv *.txt documents/`                        | Organizes files by type |

### Show Command Path

| Command           | Purpose                          |
| ----------------- | -------------------------------- |
| `which <command>` | Shows where a command is located |

### Change File Permissions

| Command                  | Purpose                   |
| ------------------------ | ------------------------- |
| `chmod <options> <file>` | Modifies file permissions |

### Change File Ownership

| Command                        | Purpose                               |
| ------------------------------ | ------------------------------------- |
| `chown <owner>:<group> <file>` | Changes the owner and group of a file |

### Execute Commands as Superuser

| Command          | Purpose                                       |
| ---------------- | --------------------------------------------- |
| `sudo <command>` | Runs a command with administrative privileges |

### Search Text in Files

| Command                 | Purpose                          |
| ----------------------- | -------------------------------- |
| `grep <pattern> <file>` | Searches for a pattern in a file |

### Stream Editor

| Command                           | Purpose                |
| --------------------------------- | ---------------------- |
| `sed 's/pattern/replace/' <file>` | Replace text in a file |

### Get Absolute File Path

| Command           | Purpose                              |
| ----------------- | ------------------------------------ |
| `realpath <file>` | Displays the absolute path of a file |
