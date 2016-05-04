git-reset
=========

> Reset current HEAD to the specified state

Git reset has three forms. &lt;tree-ish&gt; defaults to HEAD in all of them.

git reset [-q] [<tree-ish>] [--] <paths>...
-------------------------------------------

> Can be thought of as opposite for `git-add`.

Resets index entries for all &lt;paths&gt; to their state at &lt;tree-ish&gt;. Important part here is that this form of `git-reset` doesn't affect the working tree or current branch in any form.

We can try it on our current repository. Use this form of reset to return to what `09-Blame/readme.md` looked like before it was added:

	$ git status
	On branch master
	Your branch is up-to-date with 'origin/master'.
	nothing to commit, working directory clean
	$ git log --oneline 09-Blame/readme.md
	a6c2077 fixed english
	194e914 reflected feedback
	f319f65 fixed list
	38c74b7 git blame
	$ git reset 38c74b7~1 09-Blame/readme.md
	$ git status
	On branch master
	Your branch is up-to-date with 'origin/master'.
	Changes to be committed:
	  (use "git reset HEAD <file>..." to unstage)

		deleted:    09-Blame/readme.md

	Untracked files:
	  (use "git add <file>..." to include in what will be committed)

		09-Blame/

Notice that the file is in `Untracked files`, meaning our working tree was not touched.

git reset (--patch|-p) [<tree-ish>] [--] [<paths>...]
-----------------------------------------------------

> Opposite for `git-add -p`.

This allows you to interactively select hunks in the difference between the index and &lt;tree-ish&gt; and then apply them to index.

git reset [<mode>] [<commit>]
-----------------------------

This form resets the current branch head to &lt;commit&gt; and depending on the mode also updates the index or working tree.

* --soft
	* does not touch the index or the working tree, your files will remain as they were and in "Changes to be commited" (index).
	* this is useful if you've forgotten to add something into last commit

	git reset --soft HEAD~1
	git add forgotten_file
	git commit

* --mixed (default)
	* resets the index but not the working tree
	* all your files are the same, they are not touched, but they are not in index anymore, they show up in local changes / untracked files
		* you need to git-add them again before commiting
* --hard
	* resets the index and working tree
	* all changes to tracked files are discarded
	* useful to throw away changes you just don't want to have
		* you screwed up merge and want to try again?
		* your code is completely wrong and you want to start over?

	git reset --hard HEAD~1

	* this throws away last commit and all your tracked files are returned to state they were in
* --merge
	* resets the index and working tree
	* keeps those which are different between the index and working tree
	* if a file that is different between &lt;commit&gt; and the index has unstaged changes, reset is aborted
* --keep
	* resets the index and working tree
	* if a file that is different between &lt;commit&gt; and HEAD has local changes, reset is aborted
