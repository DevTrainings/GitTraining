Git tfs - getting a repository
==============================

> git-tfs is a two-way bridge between TFS and git

Git-tfs allows you to fetch TFS commits into a git repository and later push your updates back to TFS. Since this is quite a big topic, it's split into multiple chapters.

Getting git-tfs
---------------

Multiple ways to get git-tfs:

* download from the [release page](https://github.com/git-tfs/git-tfs/releases)
* using chocolatey: `choco install gittfs`
* Github desktop has git-tfs integrated

You have to make sure that `git-tfs.exe` is in your path.

Getting repository
------------------

Here you have two options. You can either directly clone TFS repository/branch or just clone git repository someone cloned from TFS for you. I strongly recommend second approach. That's how we are set, we have main TFS repository and multiple autosynchronized git repositories from it.

### Clone TFS

You should list remote branches with

	git tfs list-remote-branches http://tfs:8080/tfs/DefaultCollection

and after that clone what you want

	git tfs clone http://tfs:8080/tfs/DefaultCollection $/some_project

> Important note: Each developer who does this will likely get different hashes for commits, so resulting git repositories won't be able to work together!

### Clone existing git TFS clone

> Recommended method

You just clone existing git repository using

	git clone repository

after that, you need to initialize git tfs using

	git tfs bootstrap

This will quickly configure clone git repository for use with the original TFS repo.

Updating
--------

In case you have (the recommended) auto synchronazing TFS---Git repository, you can just use `git pull`. Otherwise you can use

	$ git tfs pull [-r]

Fetches TFS changesets and merges (or rebase with `-r`) then on current branch.

What next?
----------

Either approach you used, you now have fully working git repository. See `21-GitTfsShelvesets` for more.
