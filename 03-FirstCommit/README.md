# Adding the first file to the repository

## Introduction

* Your local repository folder is also your working folder (sandbox).
* You have a local working copy of source code.
* You always have a single working branch active.

## Commands

* Start the _GIT Shell_.
* Switch to your repository:

```
> cd d:\code\GitTraining1
```

* Create a file using your favorite editor (e.g. write some code):

```
> notepad README.md
```

* Add content to it:
* _Hello GIT World!_
* Save the file
* Check the local repository status:

```
> git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        README.md

nothing added to commit but untracked files present (use "git add" to track)
```

* Add the file to _GIT_ staging area:

```
> git add README.md
```

* See the command prompt how that changed.
* Check the local repository status:

```
> git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   README.md
```

* And commit the file:

```
> git commit -m 'First commit and comment for it'
1 file changed, 1 insertion(+)
create mode 100644 README.md
```

## Comments

* _GIT_ is trying hard to give you advices and help you with most obvious
  usecases.
* Staging area:
  * Prepares changes for commit.
  * If the file is modified after being added to the staging area you have to
    add it again.
* Commit
  * ```git commit``` checks the changes from staging area into the local repository.
  * _GIT_ always requires commit message to be specified.
  * If you do not specify ```-m``` parameter your default text editor will be
    opened and you can write your message there.
