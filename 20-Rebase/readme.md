> Preparation: `git clone https://github.com/DevTrainings/test_rebase.git`

git-rebase
==========

> Reapply commits on top of another base tip

Rebasing branch
---------------

Rebasing is a cool way of integrating changes from one branch into another.

Let's check how it looks:

	$ git log --all --graph --oneline --decorate
	* 4034926 (origin/master, master) f
	* f08314c e
	| * 82bb34d (HEAD -> feature, origin/feature) d
	| * 033af1f c
	|/  
	* cb1bb54 b
	* 46a3735 a
	* 3173651 readme

We see that some commits on master were done, than was create branch `feature` and then more commits were done both on `master` and `feature`.

Now we know that last commits on `master` change some code we were using so our changes would not longer compile. We want to fix this, because resolving stuff like this is better to do sooner than later. We have two options now:

* merge
	* works, but clutters history
* rebase
	* this can reapply our commits in `feature` onto current tip of the `master`

```
> git checkout feature
```

```
> git rebase master
First, rewinding head to replay your work on top of it...
Applying: c
Applying: d
```

```
$ git log --all --graph --oneline --decorate
* f60a099 (HEAD -> feature) d
* 378da49 c
* 4034926 (origin/master, master) f
* f08314c e
| * 82bb34d (origin/feature) d
| * 033af1f c
|/  
* cb1bb54 b
* 46a3735 a
* 3173651 readme
```

We can see that our branch now looks like it was branched from current tip of the master

### Consequences

It's important to keep in mind, that doing rebase rewrites repository history. This means that whoever was using original version of the branch will get conflicts when he tries to update.

> Think before you rebase some published branch. Think if it will cause problems to some people. If yes, don't do it or notify them so they are not surprised.

### Conflicts

Sometimes you can get merge conflict during rebase. You have to resolve them and then continue with `git rebase --continue`. You can also abort with `git rebase --abort`.

Interactive rebase
-----------------

This is useful if you forgot to add something or you want to fix commit message, drop some commits and more. Switch to `rebase_i` branch:

	$ git checkout -b rebase_i
	Switched to a new branch 'rebase_i'
	$ git log --oneline
	1446aad added exclamation mark
	814b1e4 fixed spelling
	538b5f9 msg added
	4034926 f
	f08314c e
	cb1bb54 b
	46a3735 a
	3173651 readme

We can see that we added some message, then fixed spelling and than added exclamation mark (to the end). We want to merge 538b5f9 and 814b1e4 into one commit and drop 1446aad (the exclamation mark).

We use syntax `git rebase -i <commit>` for this, where commit is last commit we know is ok.

	$ git rebase -i 4034926

It will open text editor with content like this:

	pick 538b5f9 msg added
	pick 814b1e4 fixed spelling
	pick 1446aad added exclamation mark

	# Rebase 4034926..1446aad onto 4034926 (3 command(s))
	#
	# Commands:
	# p, pick = use commit
	# r, reword = use commit, but edit the commit message
	# e, edit = use commit, but stop for amending
	# s, squash = use commit, but meld into previous commit
	# f, fixup = like "squash", but discard this commit's log message
	# x, exec = run command (the rest of the line) using shell
	# d, drop = remove commit
	#
	# These lines can be re-ordered; they are executed from top to bottom.
	#
	# If you remove a line here THAT COMMIT WILL BE LOST.
	#
	# However, if you remove everything, the rebase will be aborted.
	#
	# Note that empty commits are commented out

So looking at the command, we can see that we want `f` for the second one and `d` for the third.

	$ git rebase -i 40349
	[detached HEAD 19d675d] msg added
	 Date: Thu Apr 21 01:21:07 2016 +0200
	 1 file changed, 1 insertion(+)
	 create mode 100644 rebase_i
	Successfully rebased and updated refs/heads/rebase_i.
	$ git log --oneline
	19d675d msg added
	4034926 f
	f08314c e
	cb1bb54 b
	46a3735 a
	3173651 readme
	$ cat rebase_i 
	Bye

We can see that rebase was correctly done and `rebase_i` contains correct message.

Notice that hash of `msg added` commit changed, so all consequences from previous section apply.

Lab
---

* Start with cloning [https://github.com/DevTrainings/lab_rebase.git](https://github.com/DevTrainings/lab_rebase.git) repository. 
* Checkout branch `feature`.
* Imagine you just finished your work on branch `feature` and want to prepare it for being merged into `master`. 
* You will likely want to rebase you work onto master. 
* Rebase `feature` branch onto `master` branch using your tool of choice (command line, sourcetree, tortoise-git, whatever you like).

Documentation
-------------

You can check documentation [here](https://git-scm.com/docs/git-rebase).
