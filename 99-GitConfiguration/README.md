# Configuration

## Introduction

* _GIT_ stores the configuration in ```gitconfig``` files.
* The configuration file defines the user's name and email which
  is being used during ```git-commit```.
* There are three levels of configuration:
  * system
    * Machine specific, shared with all users.
    * To edit the file in plain text you can use:

```
git config --system --edit
```

  * global
    * User specific, shared by given user for all repositories.
    * Overrides _system_ level.
    * To edit the file in plain text you can use:

```
git config --global --edit
```
  * local
    * Repository specific.
    * Overrides _global_ and _system_ level.
    * To edit the file in plain text you can use:

```
git config --local --edit
```

## E-mail and user name configuration

* Two commands below will set user's email and user name on global level.
* This means that unless the cloned repository has a local override
  these values will be used.
* It is very handy if you work on multiple repositories.
* You can always use ```--local``` instead of ```--global``` to override
  values per repository.
* File should be located as ```.gitconfig``` in your home directory.

```
git config --global user.email "your_email@example.com"
```

```
git config --global user.name "Vladimir Kloz"
```

## Merge tool

### Visual Studio

* It is pretty handy to use a visual merge tool you are used to using.
* For 3-way merge Visual Studio works pretty well.
* Open the global configuration file:

```
git config --global --edit
```

* Copy & Paste lines below to it (obviously adjust paths if/as needed
  to match your VS version/location):

```
[merge]
      tool = vsdiffmerge
[mergetool]
      prompt = false
      keepbackup = false
[mergetool "vsdiffmerge"]
      cmd = '"C:/Program Files (x86)/Microsoft Visual Studio 12.0/Common7/IDE/vsdiffmerge.exe"' "$REMOTE" "$LOCAL" "$BASE" "$MERGED" //m
      trustexitcode = true
```

* Save the file.

### KDiff3

Alternatively, if you want to use something smaller and (imho) better, you can go with KDiff3. Opensource, multiplatform and free.

#### Git for Windows

	$ git config --global mergetool.kdiff3.path "C:/Program Files/KDiff3/kdiff3.exe"
	$ git config --global merge.tool=kdiff3

#### Cygwin

This is little harder. It assumes you have `cyg-wrapper.sh` script in `~/bin`.

	$ git config --global mergetool.kdiff3.path
	$ git config --global mergetool.kdiff3.cmd '~/bin/cyg-wrapper.sh "C:/Program Files/KDiff3/kdiff3.exe" "$LOCAL" "$REMOTE" --output "$MERGED" --base "$BASE"'
	$ git config --global merge.tool kdiff3

#### DiffMerge

Also free.  Basic features.

## Diff tool

* For the comparison (diff) it is good to use a tool you are used to.
* Example below shows how to setup [Winmerge](http://winmerge.org/downloads/) and kdiff3.
* Open the global configuration file:

### Winmerge

```
git config --global --edit
```

* Copy & Paste lines below to it:

```
[diff]
    tool = winmerge
[difftool "winmerge"]
    cmd = winmergeu.exe -e -ub -x -wl -u -maximise -dl "base" -dr "mine" \"$LOCAL\" \"$REMOTE\"
[difftool]
    prompt = false
```

* Save the file.

### KDiff3

#### Git for windows

    $ git config --global difftool.kdiff3.path "C:/Program Files/KDiff3/kdiff3.exe"
	$ git config --global diff.tool=kdiff3

#### Cygwin

Assuming you have `cyg-wrapper.sh` script in `~/bin`.

	$ git config --global difftool.kdiff3.path
	$ git config --global difftool.kdiff3.cmd '~/bin/cyg-wrapper.sh "C:/Program Files/KDiff3/kdiff3.exe" "$LOCAL" "$REMOTE"'
	$ git config --global diff.tool kdiff3

## Default text editor

* Another handy setting can be the default text editor which opens during
  various operations.
* Command below uses _notepad++_ but can be adjusted easily to anything
  else.

```
git config --global core.editor "'C:/Program Files (x86)/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"
```

### Windows GVim from cygwin

Setting up GVim as default editor is trivial, so I'll not get into that. But getting it work under cygwin (meaning you launch from cygwin the windows instance with correct settings) is a bit tricky.

	$ git config --global core.editor 'VIM="C:/Dev/vim" HOME="C:/Users/tv185035" cyg-wrapper.sh "C:/Dev/vim/vim74/gvim.exe"'

Now your GVim should use same settings when started from windows or from git.
