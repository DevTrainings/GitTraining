# Adding the first file to the repository

## Introduction

* Your local repository folder is also your working folder (sandbox).
* You have a local working copy of source code.
* You always have a single working branch active.

## Commands

* Start the _GIT Shell_.
* Switch to your repository:
  * ```cd d:\code\GitTraining1```
* Create a file using your favorite editor:
  * ```notepad README.md```
  * Add content to it:
  * _Hello GIT World!_
  * Save the file
* Check the local repository status:
  * ```git status```
* Add the file to _GIT_ staging area:
  * ```git add README.md```
* Check the local repository status:
    * ```git status```
* And commit the file
  * ```git commit -m 'First commit and comment for it'```

## Comments

* Staging area:
  * Prepares changes for commit.
  * If the file is modified after being added to the staging area you have to add it again.
* Commit
  * ```git commit``` checks the changes from staging area into the local repository.
  * _GIT_ always requires commit message to be specified.
