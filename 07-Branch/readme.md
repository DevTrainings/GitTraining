> Preparation: `git clone https://github.com/DevTrainings/premade_branch.git`

# Branching

* List, create or delete branches

We are continuing on repository from part 04, so let's list branches
we have:

```
> git branch
* master
```

We can see one branch called `master` with asterisk marking currently
active branch. Create a new branch:

```
> git branch my_aple_app
```

Check which branches we currently have:

```
> git branch
* master
  my_aple_app
```

Oh, we made a mistake in spelling! But don't worry, we can fix that with

```
> git branch -m my_aple_app my_apple_app
```

We just renamed the branch to fix it:

```
> git branch
* master
  my_apple_app
```

And you know what? Let's not do OS X version of our application, since we don't know how to switch into it (yet!) anyway, so let's delete it:

```
> git branch -d my_apple_app
Deleted branch my_apple_app (was 1126614).
```

So, to sum up what we've just learned

* git branch [--list]
	* list branches
* git branch _BRANCH_NAME_
	* create branch named _BRANCH_NAME_ from current HEAD
* git branch -m _OLD_BRANCH_NAME_ _NEW_BRANCH_NAME_
	* rename branch
* git branch -d _BRANCH_NAME_
	* delete branch

# More information

I recommend checking [git-branch documentation](https://git-scm.com/docs/git-branch) for more details,
you can use `git-branch` to manage/list remote branches as well, set upstream for branch, create new branch from specific commit and more. All of that is out of scope of this tutorial.
