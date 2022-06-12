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

This will create a `.git` folder which will contain all of the information regarding the project.

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

## Cloning a Repository

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

## Recording Changes to the Repository

A file in your working directory that is being observed by Git can be in one of the two states: `tracked` and `untracked`.

`tracked` means that the file is being watched for any modifications by Git.

`untracked` means that the file is not being watched by Git and is not in your staging area.
