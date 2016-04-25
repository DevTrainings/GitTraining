# Remote Repository Lab

Now let's have some fun with a remote repository:

* Make clone of the repository: [https://github.com/DevTrainings/test_remote.git](https://github.com/DevTrainings/test_remote.git)
* Create own repository on your favorite server named _test\_remote\_private_.
* Change remote _origin_ URL to your new repository.
* Publish the cloned repository into your own repository.
* Now clone the repository from your account into second folder _test\_remote\_private\_2_.
* Make this second clone active.
* To file _Changelog.txt_ add text _Starting 16.3 release_
* Commit the file and publish it to your _origin_.
* Make the first clone active.
* Update your local repository with remote changes.
* Verify that your both clones synchronized properly.
* You can also use existing remote branches to play around a little bit.

# Comments

* Commands used in this lab are:
  * ```git clone```
  * ```git remote```
  * ```git push```
  * ```git add```
  * ```git checkout```
  * ```git pull```
* Make sure that your published repository contains also following branches
  and tags:
  * Branches:
    * Release_16.1
    * Release_16.2
  * Tags:
    * build-16.1.1.0
    * build-16.1.2.0
    * build-16.2.1.0
