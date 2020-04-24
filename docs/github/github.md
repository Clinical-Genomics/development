# Quick reference guide to Github

## Purpose

This document offers an overview of the most important commands of git and it is intended to be a quick start guide to work with git repositories.

## Download and setup

### Download and install Git for Linux

If you are working on a Debian-based version of Linux you can install the basic Git tools via APT:

```bash
sudo apt-get install git-all
```

Here are instructions on how to [install Git under other Linux distributions.](https://git-scm.com/download/linux)

### Download and install Git for OSX

The latest version of Git for Mac can be downloaded [here](https://git-scm.com/download/mac), use this binary installer to get an up-to date version of he software.

If you are installing on a Mac with OS X 10.9 you can install Git from command line with Homebrew (get Homebrew [here](https://brew.sh)) by typing:

```bash
brew install git
```

## Configure username and email

The first time you are using git from command line you should set up a username and a password. To ease the authentication for each action, go to your local repository and type in the following commands:

```bash
git config user.email "you@example.com"
git config user.name "YourUsername"
```

If you are working locally (your computer only), you could also add the `--global` flag to set these values for all your repositories.


## Create a new repository

There are several ways to create a new local repository.

### Create a new repository from scratch

Create a directory with the name of the new repository and enter it from the command line. To initialize the repository type:

```git
git init
```

This command will create a .git subfolder.

### Clone a repository from a project in the clinical-genomics GitHub organisation

```git
git clone https://github.com/clinical-genomics/development.git
```

Where the url which can be obtained from the web page of your local fork, by clicking on the "clone or download" green button.
The git clone command then creates a folder with the project and pulls the latest data from your fork in it.

## Git data transport structure and commands

The following image shows the structure of the git commands and spaces:

![Overview](http://images.osteele.com/2008/git-transport.png)

Your workspace is the folder that holds the actual working files while the "index" is the space is a staging area where you add your changes before committing them to the local repository or `HEAD`. To send the changes to your remote repository you use the "push" command.

Here is a link to a page explaining the common Git terminology: [https://help.github.com/articles/github-glossary](https://help.github.com/articles/github-glossary)

## Create a new branch or feature for your work
To create a new branch, from command line move to the main folder containing your project and type:

```git
git checkout -b name_of_your_feature
```

If everything went fine then you'll get the following message: "Switched to a new branch name_of_your_feature". This means you are already inside the new feature. To make sure that you are in the right branch type:

```git
git branch
```

Whenever you want to move to another branch/feature the command is:

```git
git checkout [my-branch]
```

## Make changes and commit them to your local repository

Before committing any changes to your local repository, and finally to the remote repository, make sure you were working on the branch created.
After you are satisfied with your code you can start to commit to the remote repository.

To check that there are actually changes to add and commit, type:

```git
git status
```

This command will give you info on the status of your working directory comparing it with the local and remote repositories.

To update the local repository to the latest status, by fetchin and merging remote changes, type:

```git
git pull
```

The you can start adding your changes to the index with the command:

```git
git add filename_to_send_to_index
```

The process of adding a file to the index is also called staging. Be sure to add all the files you want to include to the index.
Before merging the changes you can preview them with the command:

```git
git diff source_branch target_branch
```

Calling the "diff" command without arguments will list all the differences between the index and your workspace, i.e. all the files that you could add to the index.

To commit changes from the index to the local repository (HEAD), type:

```git
git commit
```

Alternatively you can add and commit the files to the local repository in only one command:

```git
git commit -a
```

> ProTip
>
> Don't use `git commit -a` unless you're 100% sure of what you're doing. It gives you less control over the single steps of the workflow and the files you really want to commit.
Before using it, make sure everything is under control by using the `git status` and `git diff` commands. Prevent commiting tmp files your editor makes!

To include a description of the commit use the -m flag. Leaving it out is fine and will drop you into an `$EDITOR`.

```git
git commit -m "Example of a commit message"
```

It is possible to close a GitHub issue by referencing it in a commit message or pull request. The issue will be closed when the code is merged to the default branch

```git
git commit -m "Fixes #36"
```

For more examples on how to close issues using keywords see this [guide][issue-closing].

## Pushing changes to your remote repository

After "git add" and "git commit", or "commit -a", your changes are in the HEAD of your local repository. To send them to the remote repository use the command "push":

```
git push
```

## .gitignore

This is a special file that's usually part of every repo. Here you can tell git which files it should exclude from version control. Examples include private files with sensitive data, temporary log files, and large files used for testing.

GitHub hosts a [brief guide][gitignore] about the format. There's also a great resource for finding [templates][gitignore-templates] for every language to use as starting points.

## Github usage references

 - [Github short guide](https://guides.github.com/activities/hello-world)
 - [Github book](https://git-scm.com/book/en/v2)
 - [GitHub help page](https://help.github.com)
 - [Glossary](https://help.github.com/articles/github-glossary)

[gitignore]: https://help.github.com/articles/ignoring-files
[gitignore-templates]: https://www.gitignore.io
[issue-closing]: https://help.github.com/articles/closing-issues-using-keywords
