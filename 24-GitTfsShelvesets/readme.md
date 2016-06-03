# Git TFS Shelvesets

We can work with TFS shelvesets from git.

## Listing existing shelvesets

List shelvesets, by default just yours using this command

```
$ git tfs shelve-list
```

You can use:

* `--full` to get more informations
* `-u=all` to list shelvesets of all users, not just you

> I have no idea what happens when you have user named `all`.

## Unshelve

```
$ git [-u=user] tfs unshelve shelveset_name branch_name
```

Unshelves shelveset onto new branch, which is automatically created from parent commit of the shelveset.

## Shelve

```
$ git tfs shelve [-m "comment"] shelveset_name
```

This command creates a shelveset with changes on current branch since last commit with is already in TFS. Comment can be set by `-m` option if needed.

## More information

If you really need to use `git-tfs` more then you just learned, you should check documentation at [their github](https://github.com/git-tfs/git-tfs).
