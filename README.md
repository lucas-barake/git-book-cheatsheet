# Git & GitHub Book Cheatsheet

![Git Logo](./Images/git-logo.png)

A basic cheatsheet encompassing all of the topics explained in the official [Pro Git Book.](https://git-scm.com/book/en/v2)

<hr>

### Index

- [Git Basics](#git-basics)
- [Git Branching](#git-branching)
- [Git on the Server](#git-on-the-server)
- [Distributed Git](#distributed-git)
- [GitHub](#github)
- [Git Tools](#git-tools)
- [Customizing Git](#customizing-git)
- [Git Internals](#git-internals)

<hr>

## Git Basics

### Initialize a Git Repository

Navigate to the desired project in the CLI and execute the following command:

```
git init
```

This will create a `.git` folder which will contain all of the information regarding the project and begin observing files.

### Add Files to the Staging Area

Staging a file means Git will now track any changes and prepare it for a commit.

```
git add <filename>
```

To stage a file that is **ignored** you can use the `--f` or `--force` option.

```
git add --force <filename>
git add --f <filename>
```

To stage all **new, modified, and deleted** files, you can use the `-A` option (shorthand for `--all`).

```
git add -A
```

To stage all **new and modified** files in the current directory you can use the `.` option.

```
git add .
```

To stage all **modified and deleted** files use the `-u` option (shorthand for `--update`).

```
git add -u
```

### Cloning a Repository

Cloning a repository gets you a copy of an existing Git repository, with a full copy of nearly all data that the server has (hence it will continue to synchronize with the target repository).

To clone a repository you must provide a URL.

```
git clone <url>
```

This will initialize a `.git` directory inside the directory of where you ran the command.

You can specify the target directory by providing the name of the directory after specifying the URL.

```
git clone <url> <directoryname>
```

### Recording Changes to the Repository

A file in your working directory that is being observed by Git can be in one of the two states: `tracked` and `untracked`.

`tracked` means that the file is being watched for any modifications by Git.

`untracked` means that the file is not being watched by Git and is not in your staging area.

#### Git Status

You can check the state of your files by using the `status` command. It displays which files are `staged`, `unstaged`, and `untracked`.

```
git status
```

An example output is the following:

```
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
    modified: README.md
```

This shows which file(s) have been modified but are not in the staging area.

You can use the `-s` or `--short` option to display a less verbose output.

```
git status -s
git status --short
```

This will instead output the following:

```
M README.md
```

Where the `M` indicates that the file has been modified.

When a file is in the staging area, the output would be the following:

```
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
    modified: README.md
```

Alternatively, with `-s` or `--short`:

```
M README.md
```

#### Git Log

The `git log` command, in contrast to the `git status` command, displays the **committed history** only.

```
git log
```

An example output would be the following:

```
commit db45d13a7fde24e15950f20a0b9df247472ab270 (HEAD -> main, origin/main)
Author: lucas <lpatronr@gmail.com>
Date:   Sat Jun 11 22:35:05 2022 -0500

    First commit
```

Similarly to the `git status -s` option, we can do the same with the `--oneline` option.

```
git log --oneline
```

Yielding the following output:

```
db45d13 (HEAD -> main, origin/main) First commit
```

#### Git Diff

You can use the `git diff` command to show all of the changes that are not yet staged.

```
git diff
```

This command will compare what is in your working directory with what is in your staging area.

If you want to see a comparison with the changes that are staged, you can pass the `--staged` or `--cached` option (they are the same).

```
git diff --stage
```

### Commits

When you have files that are already in the `stage` area, you can commit them, hence generating a snapshot of your file at a specific point in time.

You can use the `git commit` command.

```
git commit
```

This will prompt you for a commit message.

There are certain options that you can use when committing a file:

This will commit a snapshot of all of the `staged` changes in the working directory.

```
git commit -a
```

You can also specify the message in oneliner.

```
git commit -m "<message>"
```

You can combine the `-a` and `-m` options into one single option which will commit all of the `staged` changes in the working directory alongside allowing you to provide a message.

```
git commit -am "<message>"
```

You can `reset` the state of a file prior to its latest snapshot (commit) by using the `git reset` command.

```
git reset <file>
```

You can pass in the following options:

- `--soft` to uncommit changes (changes are left staged). This is useful if you regret committing multiple times instead of leaving them in a single commit.
- `--mixed` uncommit + unstage changes (changes are left in working tree). This is useful if you want your staged and committed files to be unstaged
- `--hard` uncommit + unstage + delete changes (nothing will be left). This is useful if you want to restore everything to its previous state.

Think of it this way:

1. Modified the file
2. Added the file to the staging area `git add <file>`
3. Committed the file `git commit -m "<message>"`

- `--soft` will pretend you never committed the file (#3).
- `--mixed` will pretend you never added the file to the staging area (#2).
- `--hard` will pretend you never modified the file (#1).

### Ignoring Files

A `.gitgnore` file will not track any files (hence ignoring them). This, however, affects files that are already **not** tracked.

Each line in the `.gitignore` file will match a pattern. If there is a blank line, it will have no use. Similarly, using a hashtag `#` serves as a comment (though you can put a backlast `\` in front of the first hashtag `#` for patterns that being with a hashtag `#`).

[You can read all of the patterns here](https://git-scm.com/docs/gitignore#_pattern_format).
