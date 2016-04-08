# Working with remote repository

## Introduction

Once we have our remote repository configured we would be able to work with it.

The list of commands below allows to work with remote repository.

## Commands

### Publishing a branch

* Let's create a local branch where we will develop a nice new feature:
```
> git checkout -b AddEasterEgg
Switched to a new branch 'AddEasterEgg'
```

* Let's do some changes to it:
```
> echo "Happy Easters!" > MyWindowsApp\EasterEgg.txt
> git add MyWindowsApp\EasterEgg.txt
> git commit -m 'Adding the Easter Egg'
[master a0bc533] Adding the Easter Egg
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 MyWindowsApp/EasterEgg.txt
```

* Let's publish the branch now.
```
> git push -u origin AddEasterEgg
Counting objects: 4, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 471 bytes | 0 bytes/s, done.
Total 4 (delta 0), reused 0 (delta 0)
To https://github.com/voloda/GitTrainingPlayground.git
 * [new branch]      AddEasterEgg -> AddEasterEgg
```

### Checking out a remote branch

It may be handy to see the list of branches including remote ones first.

First let's update the content of the local repository from remote:
```
> git fetch origin
```

Now see the list
```
> git branch -a
GitRm
Remote
ToolsConfiguration
* master
origin/master
remotes/origin/GitRm
remotes/origin/Remote
remotes/origin/ToolsConfiguration
remotes/origin/f_11
remotes/origin/Fixes
remotes/origin/master
```

If the remote branch does not conflict with any local branch, you can
simply use:

```
> git checkout Fixes
Branch Fixes set up to track remote branch Fixes from origin.
Switched to a new branch 'Fixes'
```

Or alternatively you can specify remote name too (```origin``` in this
case):
```
> git checkout -t origin/Fixes
Branch Fixes set up to track remote branch Fixes from origin.
Switched to a new branch 'Fixes'
```

### Retrieving changes from a remote branch

If your branch was set to track a remote branch you can use:
```
> git pull
```

Alternatively, if your branch for some reason does not track its remote
counterpart or you would pull changes from another branch you can specify
details:
```
> git pull origin Remote
```
