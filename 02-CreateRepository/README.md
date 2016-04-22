# Create repository

## Introduction

* For the initial purpose we will consider only a local repository.
  * We will not use concurrent access to the repository in the beginning.
  * _Repository can be published later without any issues_.
* Let's consider that we have our local sandbox in folder **d:\code**.
* We would create a repository **GitTraining1**.


## Commands

* Start _Git Shell_.
* Create a local folder where your repository will reside:
  * ```mkdir d:\code\GitTraining1```
* Switch to created folder:
  * ```cd d:\code\GitTraining1```
* Initialize _GIT_ repository:
  * ```git init```

## Comments

**Congratulation** - you have your first _GIT_ repository.

* The commands above initialized **GitTraining1** repository in the local path
  **d:\code\GitTraining1**.
  * This folder contain **.git** subfolder with _GIT_ internal data.
    * The distributed copy of the whole directory is here.
  * This also serves as a local working copy where you edit source code.
* See the _PowerShell_ command line (contains branch name and perhaps
  additional details about repository status).
