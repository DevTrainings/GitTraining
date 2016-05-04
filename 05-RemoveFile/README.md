# Removing a file from a repository

## Introduction

* Removing a file from a repository is done in two steps.
* First you remove the file in the staging area.
* Next you have to commit your changes.
* Directories are not tracked by _GIT_.
  * Once a folder becomes empty it will not appear in your sandbox.
  * This is different from some other source control systems (TFS for example). If you want to keep a folder for some reason, then create a file inside it. Commonly used files are
    ```.gitattribute``` (this has special meaning), ```.gitkeep```,
    ```.placeholder```, or ```.gitignore``` (this has special meaning).

## Commands

* Remove the file in staging area:

```
> git rm .\MyConsoleApp\console.txt
rm 'MyConsoleApp/console.txt'
```

* See how the status on command line changed.
* Since the ```MyConsoleApp``` should be empty it should disappear from
  disk:

```
> ls -l .

    Directory: D:\Code\GitTraining1


Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----         3/17/2016  12:58 PM            MyWindowsApp
-a---         3/17/2016   1:02 PM         45 README.md
```

* Check how the staging area looks like:

```
> git status

On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    MyConsoleApp/console.txt
```

* Commit your changes:

```
> git commit -m 'Removal of console application'
1 file changed, 5 deletions(-)
delete mode 100644 MyConsoleApp/console.txt
```

## Comments

* If you want to undo the file deletion prior to commit, you can use
  following set of commands:

```
> git reset HEAD
Unstaged changes after reset:
D       MyConsoleApp/console.txt
```

* Followed by:

````
> git checkout -- MyConsoleApp/console.txt
```

* Commands above will discard the removal from the staging area and then restore
  the file from _GIT_.
