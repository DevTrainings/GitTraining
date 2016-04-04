# Working with remote repository

## Introduction

Once we have our remote repository configured we would be able to work with
it.

## Commands

### Publishing a branch

* Let's create a local branch where we will develop a new feature:
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

* Let's publish the branch now
```
> git push origin AddEasterEgg
Counting objects: 4, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 471 bytes | 0 bytes/s, done.
Total 4 (delta 0), reused 0 (delta 0)
To https://github.com/voloda/GitTrainingPlayground.git
 * [new branch]      AddEasterEgg -> AddEasterEgg
```

### Retrieving changes from a remote branch
