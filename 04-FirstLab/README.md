# First lab

* Perform tasks below.
* Watch the _PowerShell_ command line how it changes.
* Use ```git status``` to see what is going on.

# Task

* Create in your repository following folders and files.
* For these files put some content in them per your preference:
  * MyConsoleApp
    * console.txt
  * MyWindowsApp
    * windows.txt
    * code.txt
* Add all files into _GIT_ repository as a single commit
  * As a check-in message use text: _My first lab commit 1_
* Now add a line to each of files in repository:
  * _Added during git workshop_
* Commit all changes as a single commit
  * As a check-in message use text: _My first lab commit 2_

# Changelog

* Now run the command below:
  * ```git log```
* If you did everything correctly you should get output similar to this:

```
D:\code\GitTraining1 [master]> git log
commit a7ac772f12f8030cce31d1e982320e462b146239
Author: Kloz, Vladimir <Vladimir.Kloz@ncr.com>
Date:   Thu Mar 17 13:02:34 2016 +0100

    My first lab commit 2

commit fdbb6c2330be1da8e931265dd68424fcddef89fb
Author: Kloz, Vladimir <Vladimir.Kloz@ncr.com>
Date:   Thu Mar 17 13:01:39 2016 +0100

    My first lab commit 1

commit f2e6ba3a6b66e326a936198ea424aea3cf19c79f
Author: Kloz, Vladimir <Vladimir.Kloz@ncr.com>
Date:   Thu Mar 17 12:56:25 2016 +0100

    First commit and comment for it
```

# Comments

* When adding contents of a folder you do not have to add individual files.
* Folders are not individual part of repository.
