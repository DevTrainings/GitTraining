# Overview

> Git is a distributed revision control system with an emphasis on speed, data integrity, and support for distributed, non-linear workflows.

It is great and all, but what does it mean? Here are some points people have a hard time understanding about git:

* everything related to git repository is stored in `.git` folder in root of your project; you can just copy project folder and git repository will travel with it
* from technical standpoint, there is no central repository, all repositories are equal
* usually there is one `upstream`, but which repository it is depends on agreement between project members
* this has some (maybe) unexpected side effects
	* you cannot restrict read access to specific files, folders, branches; if you want someone to clone from you, he has to be able to get everything
	* everyone has complete history of the project

## All repositories are equal

* while you do clone from somewhere, you are not restricted to pushing/pulling from there
* For example, you have a colleague who made some useful class but it's not ready to be pushed upstream yet? Don't worry, you can pull it directly from him

## Restricting access

* you cannot restrict **read** access to files, directories or branches
	* this can sometimes be problem in corporate environment for direct migration from SVN/TFS to git
* it **is** possible to restrict **write** access
	* git has ability to be extended by hooks, so you can restrict write and/or check other stuff
		* for example, you can verify that commit contains WIT number or other content and reject it otherwise

## Everyone has complete history

* this is very important point
* I'm sure it happened to you at least once. You commit password into source control
	* if someone already cloned/pulled from you, all you can do is change it
	* committing new version without the password won't help you, because everyone has complete history, each and every commit, in the local repository
* Remember this also when you are going to commit some huge file (`.pdb` or something) and later down the line you notice  that your repository is huge
	* deleting the file and committing the deletion won't help (unless you rewrite history and remove the file completely from all commits, see below)
	* the file is part of the repository forever
* **history can be rewritten** but you will break every repository that cloned from you and they will have to re-clone losing every local branch
	* in other words, **don't ever rewrite history unless you know what you are doing**

## Commit and History integrity

* unlike TFS or SVN, there are no revision numbers in git, git uses SHA-1 hashes to mark commits instead
* each file in your repository is represented by its SHA-1 checksum
* part of checksum-ed git commit is checksum of previous commits, so it forms cryptographically secure line from root commit to current state
	* this means that if you have repository at the same commit as someone else and no local changes, you can be (pretty) sure you have the exact same files

## What is a branch in git?

* a branch is really just a pointer to a commit
* the difference between a branch and a tag is that the branch is updated to a new commit when you commit into it
* each branch isn't separate folder like in SVN/TFS
* you can have only one branch checked-out at the moment since it reflects the state of all files of the git repository for that workspace

## GIT Vision

* Commit early and often.
  * Benefit of doing so is that you can always return back to point where it makes sense (or perhaps just check the status 2 hours ago).
* Make it nice later.
  * Once you are done with your changes you can make them nicer before publishing.
  * _GIT_ strength is that you can reorganize commits later before making them public or sending them for code review.

## This Training

* We will start with the GIT command line interface to give you understanding of _GIT_.
* We will do a brief overview of visual tools later.
