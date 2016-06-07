# Working with remote repository

## Introduction

Once we have our remote repository configured, we can work with it.

The list of commands below allows to work with remote repository.

Remote repository does not need to be provided by a _GIT_ server, it can
be as well a network share or just a different local folder.

### Upstream

Upstream is a branch in central location. If a branch is configured for upstream some of the commands (like ```git pull```) will not require the name of remote and branch.

Also it is pretty convenient since you may usually see the status of your
working branch indicated in the command line.

Having an upstream is optional and you can change it/remove at any point
in future.

## Commands

### Creating copy of remote repository

* Since we just published our local repository we do not need to create
  a local copy (we can skip `git clone`).
* Process of creating a local repository copy is known as ```clone```.
* Please note that we are leaving alone setup of the authentication here.
```
> git clone https://github.com/DevTrainings/GitTrainingPlayground.git
Cloning into 'GitTrainingPlayground'...
remote: Counting objects: 26, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 26 (delta 2), reused 26 (delta 2), pack-reused 0
Unpacking objects: 100% (26/26), done.
Checking connectivity... done.
```
* Above command will clone remote repository to the local folder ```GitTrainingPlayground```.
* You can specify the local folder name explicitly:
```
> git clone https://github.com/DevTrainings/GitTrainingPlayground.git GitTrainingPlayground2
Cloning into 'GitTrainingPlayground2'...
remote: Counting objects: 26, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 26 (delta 2), reused 26 (delta 2), pack-reused 0
Unpacking objects: 100% (26/26), done.
Checking connectivity... done.
```
* You may be asked to provide credentials for your remote account.

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

First let's update the local index from remote. This command does not affect your working copy - just refreshes the distributed clone of the repository (which is different from TFS).

You can easily compare the differences between local and remote branches.

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

In high level `pull` can be considered as a shortcut for `git pull` and
`git merge` which is performed in a single step.

If you would review first what you are about to merge simple do `git fetch` and then compare remote and local branch.

## Authentication/Credentials

* In the case you work with a remote repository you usually need some
  kind of credentials.
  Two most commonly used authentication mechanisms for _GIT_ are:
  * User name and password.
  * SSH key pair.
* We will here stick to the user name and password. See relevant details
  for your remote repository on how to setup for example SSH.
