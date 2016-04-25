git-checkout
============

* Switch branches or restore working tree files

Let's create OS X version after all. This time we'll use `git-checkout`
with `-b` switch, which creates new branch if it doesn't exist already
and checkout the new branch
	git checkout -b my_apple_app

With knowledge from last part we can check if it worked

	$ git branch
	  master
	* my_apple_app

Now we "implement" OS X version and commit it

	$ mkdir MyAppleApp
	$ echo "OS X implementation" > MyAppleApp/osx.txt
	$ git add MyAppleApp
	$ git commit -m "OS X version"

But this version will require more work, so we switch back to master
to do something else

    $ git checkout master
    $ git branch
	* master
	  my_apple_app

Notice that `MyAppleApp` folder is not in the working tree any longer
(because it was committed into another branch):

	$ ls -l .
	total 4
	drwxr-xr-x 2 paladin paladin 60 Mar 20 14:58 MyConsoleApp
	drwxr-xr-x 2 paladin paladin 80 Mar 20 14:58 MyWindowsApp
	-rw-r--r-- 1 paladin paladin 17 Mar 20 14:55 README.md

> If you have local uncommitted changes in file(s) that are different between
> the current branch and the target branch, `git-checkout` will refuse to switch
> branches. You can either commit them or stash them (more on this later)

Now it's time to take a look at second usage for `git-checkout`. Restoring files in working tree. Let's see how `MyConsoleApp/console.txt` looks

	$ cat MyConsoleApp/console.txt 
	Added during git workshop

Do some modifications to the file and check the repository status

	$ git status
	On branch master
	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git checkout -- <file>..." to discard changes in working directory)

		modified:   MyConsoleApp/console.txt

	no changes added to commit (use "git add" and/or "git commit -a")

Now let's throw away those changes because we don't need them.

    $ git checkout MyConsoleApp/console.txt
	$ git status
	On branch master
	nothing to commit, working directory clean

> Important to notice here is that there is no warning before overwriting the changes.
> And in general there is no way to get them back after doing checkout. So be careful.

You can do similar thing for deleted files

	$ rm MyConsoleApp/console.txt
	$ git status
	On branch master
	Changes not staged for commit:
	  (use "git add/rm <file>..." to update what will be committed)
	  (use "git checkout -- <file>..." to discard changes in working directory)

		deleted:    MyConsoleApp/console.txt

	no changes added to commit (use "git add" and/or "git commit -a")
	$ git checkout MyConsoleApp/console.txt
	$ git status
	On branch master
	nothing to commit, working directory clean

More information
----------------

I recommend checking [git-checkout documentation](https://git-scm.com/docs/git-checkout) for more details,
you can try to merge when there is a conflict, checkout exact commit (which detaches a HEAD) and more.
