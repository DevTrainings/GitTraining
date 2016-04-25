.gitignore
==========

* Specifies intentionally untracked files to ignore

If you have some files you don't want to track in the git repository, for example object files, you can exclude them using file `.gitignore`. Git looks for that file in following locations:

* $HOME/.config/git/ignore
	* put global stuff here (backup files created by text editor etc.)
* $GIT_DIR/info/exclude
	* put repository specific but not to be shared files here
* .gitignore
	* git looks for this file in current directory and any parent up to the root of the work tree
	* put things everyone should ignore here

Syntax
------

* use `#` at the start of a line for comments
* trailing spaces ignored unless escaped
* if you need to include previously excluded file, use `!` for that
	* it's not possible to re-include a file if parent directory was excluded
* patterns ending with slash (`/`) match only directories
* if pattern doesn't contain slash (`/`), it's used as shell glob pattern
* double asterisk `**` may have special meaning:
	* leading followed by a slash (`**/foo`) matches in all directories
	* trailing (`foo/**`) matches everything inside
	* slash + double asterisk + slash (`bar/**/foo`) matches zero or more directories
