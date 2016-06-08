Git flows
=========

There is wide array of possible git workflows you and your team can follow.

Centralized Workflow
--------------------

![Centralized Workflow](https://devtrainings.github.io/GitTraining/git-flows/centralized.svg)

This way git is used in the same (or very similar) way as centralized version control system. You have one repository which serves as central point holding all the changes.

> But git has advantages used even in this way. Developers still can have cheap local branches for experimentation.

All developers normally work on `master` branch, do local commits and push when they are done. In case of conflicts `rebase` can (should) be used instead of merge to preserve nice, clean and **linear** history.

> `git pull --rebase origin master` works nicely for updating local repository in case of conflicts while pushing

Feature Branch Workflow
-----------------------

![Feature Branch Workflow](https://devtrainings.github.io/GitTraining/git-flows/feature-branch.svg)

This is extension of previous model with the exception that each new feature lives in its own branch. Multiple developers can easily works on the feature in the feature branch without disturbing `master` with changes.

After everyone agrees work is done, in can be merge into `master`. Good thing for this are pull requests, you can quite easily get back some feedback from the team during them.

Important on this is that feature branches can contain lots of small commits and be cleaned before being merge (`git-rebase`, ...).

> This model is enabled by cheap branching/merging in git.

Gitflow Workflow
----------------

![Gitflow Workflow](https://devtrainings.github.io/GitTraining/git-flows/gitflow.svg)

This workflow is quite similar to Feature Branch Workflow but has strict branching model which streamlines work with bigger projects.

In this flow `master` branch stores official release history, while development is done on branch `develop`. Features still has their own branches, you just merge back into `develop`, which server as integration branch for releases.

When you have enough changes to make a release, you create release branch in which you make sure everything works as expected. Only bug fixes, documentation and other release-related stuff should be added into it now. No new features, no refactoring.

Once ready, merge it into master, mark with proper tag. Don't forget to also merge back into develop if changes we made.

Lastly, you can use hotfix/maintenance branches to to fix important issues. You branch it from last release and after being done merge back into `master` and `develop`.

Here is another pretty picture describing all of this:

![Gitflow detailed](https://devtrainings.github.io/GitTraining/git-flows/gitflow-detailed.svg)

Forking Workflow
----------------

![Forking Workflow](https://devtrainings.github.io/GitTraining/git-flows/forking.svg)

Very different workflow from those previously discussed. Each developer has his own server-side repository. This workflow is less common in enterprise environment but it can still has its uses.

There is one project maintainer (usually team lead), who maintains (since he's the maintainer ;) ) the "canon" repository. This repository represents official product. Each of the other developers works on their own repo and can ask maintainer to pull changes from them.

### Advantages

* maintainer has to get all code into official repository
	* means he can do detailed code review to make sure code follows all guidelines
* able to support incredibly large teams
	* you can have sub-maintainers responsible for parts of the application
		* this is how linux kernel development works

### Disadvantages

* maintainer has to get all code into official repository
	* which means he can be overwhelm by amount of work
	* which means he has to understand every part of the project
		* both can be prevented by reasonable delegation to sub-maintainers

Others
------

There is lot of models how to work with git, some differs only a little, some differs quite a bit.

Credits
-------

Images are from [Git Workflows and Tutorials](https://www.atlassian.com/git/tutorials/comparing-workflows/centralized-workflow), they are used under [Creative Commons Attribution 2.5 Australia License](http://creativecommons.org/licenses/by/2.5/au/). If you are interested in this topic, I recommend to check out the atlassian link, it's quite detailed.
