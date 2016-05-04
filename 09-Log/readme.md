> Preparation:
> `git clone git@github.com:DevTrainings/premade_log.git`
> `cd premade_log`
> `git checkout my_apple_app`
> `git checkout master`

# Reviewing the repository history

* Show commit logs

You can use `git log` for inspecting history of a repository, individual files or even specific lines in a file! But remember, this text is just a brief introduction into `git-log`, so go see documentation for more details if you need to.

Now, let me just start this with a quick remark that very few of you will likely use `git-log` on a daily basis. But still, it's good to know how to use it.

The simplest form `git log` we already know, so let's try something more compact

```
> git log --oneline
6cfa070 Removal of console application
c72c6d6 My first lab commit 2
b76b4f2 My first lab commit 1
0f412a0 First commit and comment for it
```

We can see history of current branch. Now, you can provide a branch

```
> git log --oneline my_apple_app
5a1710a OS X version
6cfa070 Removal of console application
c72c6d6 My first lab commit 2
b76b4f2 My first lab commit 1
0f412a0 First commit and comment for it
```

Specific file(s)
```
> git log --oneline MyWindowsApp/code.txt
c72c6d6 My first lab commit 2
b76b4f2 My first lab commit 1
```

Or even a folder
```
> git log --oneline MyWindowsApp
c72c6d6 My first lab commit 2
b76b4f2 My first lab commit 1
```

But this is all just iterations of the same, so let's try something more interesting.
```
> git mv MyWindowsApp/code.txt MyWindowsApp/dll.txt
> git commit -m "moved code into dll"
[master eeab96e] moved code into dll
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename MyWindowsApp/{code.txt => dll.txt} (100%)
```

See the history:

```
> git log --follow --oneline MyWindowsApp/dll.txt
eeab96e moved code into dll
c72c6d6 My first lab commit 2
b76b4f2 My first lab commit 1
```

We can see that the file was tracked even across renames! Using `--follow` we can even list history of deleted files:

```
> git log --follow --oneline -- MyConsoleApp/console.txt
6cfa070 Removal of console application
c72c6d6 My first lab commit 2
b76b4f2 My first lab commit 1
```

Now what if we are interested in what happened to file(s) in what commits, but not yet in complete diff? We can use `--name-status` to see changes made to file. Let's try it:

```
> git log --follow --name-status --oneline MyWindowsApp/dll.txt
e2385cf main in dll
M       MyWindowsApp/dll.txt
eeab96e moved code into dll
R100    MyWindowsApp/code.txt   MyWindowsApp/dll.txt
c72c6d6 My first lab commit 2
M       MyWindowsApp/code.txt
b76b4f2 My first lab commit 1
A       MyWindowsApp/code.txt
```

> You can omit the file name, use the branch name, multiple files, the usual.

We can also add `-p` flag and let git list diff for complete history of the file across renames.

```
> git log --follow -p MyWindowsApp/dll.txt
commit eeab96ec34708b47a7567cf78059b25b4edb45a6
Author: Wolf <wolf@wolfsden.cz>
Date:   Wed Mar 30 16:21:43 2016 +0200

    moved code into dll

diff --git a/MyWindowsApp/code.txt b/MyWindowsApp/dll.txt

similarity index 100%
rename from MyWindowsApp/code.txt
rename to MyWindowsApp/dll.txt

commit c72c6d6f4ea5ac79185fc6767426adcf5e1a3700
Author: Wolf <wolf@wolfsden.cz>
Date:   Wed Mar 30 16:03:31 2016 +0200

    My first lab commit 2

diff --git a/MyWindowsApp/code.txt b/MyWindowsApp/code.txt
index e69de29..fc8502f 100644
--- a/MyWindowsApp/code.txt
+++ b/MyWindowsApp/code.txt
@@ -0,0 +1 @@
+Added during git workshop

commit b76b4f226b94066ece47233222a9755e3902c999
Author: Wolf <wolf@wolfsden.cz>
Date:   Wed Mar 30 16:02:47 2016 +0200

    My first lab commit 1

diff --git a/MyWindowsApp/code.txt b/MyWindowsApp/code.txt
new file mode 100644
index 0000000..e69de29
```

> I'm not using `--oneline` here, since without colors it gets kinda dense.

## More information

I recommend checking [git-log documentation](https://git-scm.com/docs/git-log) for more details, there is a **lot** of options for `git log`.
