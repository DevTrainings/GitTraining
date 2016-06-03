> Preparation: Just make empty repository with `git init`.

Git-tag
=======

You can tag specific points in history as important. Typical use case is for marking releases.

Create github repository for testing tags and clone it (you already know how to do this).

Creating tags
-------------

There are two kinds of tags

### Lightweight

This type of tag is basically just a pointer to specific commit, it doesn't contain anything special.

	> git tag TAGNAME

That's all, there is nothing more to it.

### Annotated

This type of tag is generally more useful, it can contain message, tagger name, email, date. It can be signed (GPG) and more.You should prefer this kind unless you have some reason not too.

	git tag -a TAGNAME -m MESSAGE

You create an annotated tag by specifying the `-a` option.

Now let's actually use it. Create some file, commit it and then tag it with both lightweight and annotated tag.

	touch file
	git add file
	git commit -m "file"
	git tag lightweight
	git tag -a annotated -m "annotated tag message"

> You can always tag commit later by specifying it's hash at the end of the command.

Listing tags
------------

As simple as

	git tag

	annotated
	lightweight

You can also search for tags matching some pattern

	git tag -l "light*"

	lightweight

Showing tags
------------

This shows you difference between lightweight and annotated tags the best:

### lightweight

	git show lightweight

	commit 82103463d8a94723420375f8a1609fda01082a81
	Author: Wolf <wolf@wolfsden.cz>
	Date:   Wed Apr 27 15:46:01 2016 +0200

		file

	diff --git a/file b/file
	new file mode 100644
	index 0000000..e69de29

### annotated

	git show annotated

	tag annotated
	Tagger: Wolf <wolf@wolfsden.cz>
	Date:   Wed Apr 27 15:46:01 2016 +0200

	annotated tag message

	commit 82103463d8a94723420375f8a1609fda01082a81
	Author: Wolf <wolf@wolfsden.cz>
	Date:   Wed Apr 27 15:46:01 2016 +0200

		file

	diff --git a/file b/file
	new file mode 100644
	index 0000000..e69de29

Sharing tags
------------

`git push` doesn't transfer tags by default. You can either push each tag one by one

	git push origin lightweight

or all tags that are not yet on the server at once

	git push origin --tags

Try it, push the lightweight specifically and then push all the remaining tags (in our case just the annotated) at once. Check via github web interface if it worked.
