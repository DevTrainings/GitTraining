> Preparation:

> `git clone https://github.com/DevTrainings/test_merge_conflict.git`

> `cd test_merge_conflict`

> `git checkout bar`

> `git checkout cherry-pick`

> `git checkout foo`

> `git checkout master`

# Merging changes

## Merge

> Join two or more development histories together

We will start with warning from documentation:

> Warning: Running git merge with non-trivial uncommitted changes is discouraged: while possible, it may leave you in a state that is hard to back out of in the case of a conflict.

This repository looks like this (run it yourself to have it in colors ;) ):

```
> git log --all --graph --oneline --decorate
* c5d665f (HEAD -> master, origin/master, origin/HEAD) fixed readme a bit
| * 4909911 (origin/cherry-pick, cherry-pick) merge conflict in file
| * e7f0e30 added file for cherry_pick
|/  
* 286a273 added readme
| * c5c3da1 (origin/foo, foo) file2 for demonstration of cherry-pick
| * c361f2e foo
|/  
| * bfb5647 (origin/bar, bar) bar
|/  
* 25f7328 file
```

We will ignore `cherry-pick` branch for now, we will get to it later. We have file `file` in the root folder

```
> ls -l .
total 8
-rw-r--r-- 1 paladin paladin  10 Apr 11 10:38 file
-rw-r--r-- 1 paladin paladin 154 Apr 11 11:08 readme.md

```
```
> cat file
.
.
.
.
.
```

The file `file` was changed in both branches `bar` and `foo` and we want to get those changes back into the master. We will start with `bar`

```
> git merge bar
Merge made by the 'recursive' strategy.
 file | 4 ++--
 1 file changed, 2 insertions(+), 2 deletions(-)
```

> Running git merge with non-trivial uncommitted changes is discouraged: while possible, it may leave you in a state that is hard to back out of in the case of a conflict.

This command produces no conflicts, since no changes we made to `file` after branching into `bar`. So after this merge, we can see that repository looks like this:

```
> git log --all --graph --oneline --decorate
*   05dbdf3 (HEAD -> master) Merge branch 'bar'
|\  
| * bfb5647 (origin/bar, bar) bar
* | c5d665f (origin/master, origin/HEAD) fixed readme a bit
| | * 4909911 (origin/cherry-pick, cherry-pick) merge conflict in file
| | * e7f0e30 added file for cherry_pick
| |/  
|/|   
* | 286a273 added readme
|/  
| *d c5c3da1 (origin/foo, foo) file2 for demonstration of cherry-pick
| * c361f2e foo
|/  
* 25f7328 file
```

```
> cat file
.
bar
.
.
bar
```

We can see that branch `bar` was merged into `master`. Now it's time to do the same with `foo`.

```
> git merge foo
Auto-merging file
CONFLICT (content): Merge conflict in file
Automatic merge failed; fix conflicts and then commit the result.
```

We have a conflict! We need to somehow resolve it.

> You can always abort merge with `git merge --abort`. `--abort` can be used in most situations when dealing with merge (`git-rebase`, `git-cherry-pick`, ...).

### Text editor way

In case of conflict, git puts changes into a file like this:

```
> cat file
.
<<<<<<< HEAD
bar
.
.
bar
=======
foo
.
foo
.
>>>>>>> foo
```

The `=======` separates two versions while `HEAD` being current branch and `foo` the merged branch (`foo`). All you have to is to modified the file into what you want it to look like, so I'll do for example this:

```
> cat file
.
foobar
.
foo
bar
```

After you are done with manual merge, you need to mark conflict as resolved and commit the merge:

```
> git add file
> git commit -m "Merge branch 'foo'"
[master b702845] Merge branch 'foo'
```

Let's check it out:

```
> git log --all --graph --oneline --decorate
*   b702845 (HEAD -> master) Merge branch 'foo'
|\  
| * c5c3da1 (origin/foo, foo) file2 for demonstration of cherry-pick
| * c361f2e foo
* |   05dbdf3 Merge branch 'bar'
|\ \  
| * | bfb5647 (origin/bar, bar) bar
| |/  
* | c5d665f (origin/master, origin/HEAD) fixed readme a bit
| | * 4909911 (origin/cherry-pick, cherry-pick) merge conflict in file
| | * e7f0e30 added file for cherry_pick
| |/  
|/|   
* | 286a273 added readme
|/  
* 25f7328 file
```

We now have merge both `bar` and `foo` into the master, in the process we resolved conflict between them.

### Mergetool way

> Now is probably a good time to check if you have GUI tools configured. `99-GitConfiguration` will help you with that.

We throw away the last commit (the merge of `foo`), so we can do it again, this time using merge tool.

```
> git reset --hard HEAD~1
HEAD is now at 05dbdf3 Merge branch 'bar'
```

> `git reset --hard` basically throws away everything after specified commit and `HEAD~1` is shorthand for `one-before-last` commit

Now do the merge

```
> git merge foo
Auto-merging file
CONFLICT (content): Merge conflict in file
Automatic merge failed; fix conflicts and then commit the result.
```

```
> git mergetool
```

Now resolve conflict in your favorite mergetool you configured and commit the result.

## Cherry-pick

> Apply the changes introduced by some existing commits

We want to pick specific change from branch `cherry-pick`. We don't want whole branch, just single commit.

```
> git checkout cherry-pick
Switched to branch 'cherry-pick'
Your branch is up-to-date with 'origin/cherry-pick'.
```

```
> ls
cherry_pick_this_file  file  readme.md
```

```
> git log --name-status cherry_pick_this_file
commit e7f0e306d0b5639bb6f56b1897e6dfdf319d39b7
Author: Wolf <wolf@wolfsden.cz>
Date:   Mon Apr 11 10:37:49 2016 +0200

	added file for cherry_pick

A       cherry_pick_this_file
```

We want to merge file `cherry_pick_this_file` into `master`. We found out that it was added in commit e7f0e306d0b5639bb6f56b1897e6dfdf319d39b7. We can therefore try to merge it into `master`.

```
> git cherry-pick e7f0e306d0b5639bb6f56b1897e6dfdf319d39b7
[master 145a1b2] added file for cherry_pick
Date: Mon Apr 11 10:37:49 2016 +0200
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 cherry_pick_this_file
```

```
> ls -l .
cherry_pick_this_file  file  file2  readme.md
```

We've got the `cherry_pick_this_file` without merging changes done to `file`.

> `git-cherry-pick` is crazy useful for applying hot-fixes to multiple branches. You can develop it on one branch (e.g. Baseline) and then `cherry-pick` just that one commit into maintenance branches.

## Documentation

Check out [documentation](https://git-scm.com/docs/git-cherry-pick) for some useful options.
