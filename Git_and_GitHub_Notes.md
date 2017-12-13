# Git and GitHub

## First, some useful links

* [Markdown Syntax](http://markdown.de/)
* [Markdown Emojis](https://gist.github.com/rxaviers/7360908)
* [GitHub Work Flow](https://gist.github.com/Chaser324/ce0505fbed06b947d962)

## Initial Setup

### Check the configuration

	$ git config -l

### User
Configure user name and email - either per repository or global.

Repository configuration for a GitHub project:

	$ git config user.name Matze2
	$ git config user.email 12542802+Matze2@users.noreply.github.com

### Clone a repository

From the remote fork:

	$ git clone https://github.com/Matze2/cgeo.git

### Remote Repositories
Show remote repositories configured for the local repository:

	$ git remote -v

The remote repository "upstream" is usually an official GitHub repository

	$ git remote add upstream https://github.com/cgeo/cgeo.git

The remote repository "origin" is usually the own fork of an official GitHub
project.

	$ git remote add origin https://github.com/Matze2/cgeo.git

https://stackoverflow.com/questions/9257533/what-is-the-difference-between-origin-and-upstream-on-github

## Sync

### Sync a fork

https://help.github.com/articles/syncing-a-fork/

### Sync the local master branch

	$ git checkout master
	$ git fetch upstream
	$ git merge upstream/master

or better

	$ git rebase upstream/master

You might also want to update the fork repository on github

	$ git push -f origin master

TODO: Unterschied zwischen merge und pull????

### Rebase a local feature branch against master

	$ git rebase master

## Branches

Which remote and local branches are available in this repository:

	$ git branch

Which remote and local branches are available in this repository:

	$ git branch -av

## Diffs

Between master and feature branch:

	$ git diff master 6848_result_highlighting
Shows the diff between the current state of these two branches of the branch when it was forked off master.

	$ git diff master..6848_result_highlighting
	$ git diff master...6848_result_highlighting

Shows the changes of the branch when it was forked off master.

## Pull Request

https://stackoverflow.com/questions/2765421/how-do-i-push-a-new-local-branch-to-a-remote-git-repository-and-track-it-too

### Create a local branch

	$ git branch <issue_id>_description
	$ git checkout <issue_id>_description
Rename the branch (when you are in it)
	$ git branch -m <new name>

### Development

Do your implementation in this branch and commit your changes from time to time.

	$ git commit -a

A commit log which automatically would close the corresponding issue:

	Fix #<issue_id> description

### Rebase the local development branch

	$ git fetch origin
	$ git rebase origin/master

### Push to remote branch in the fork

	$ git push -u origin 6851_copy_waypoint_notes

Passwords are saved in kwallet, section kssaskpass:

* https://github.com -> Matze2
* https://Matze2@github.com -> Passwort

After that it is enough to just push or force-push (e.g. if the commits are
pushed and should be squashed):

	$ git push
	$ git push -f

### Further commits

Commit local changes as before:

	$ git commit -a

and push it.

### Interactive Rebase

If you want to change commit logs or squash single commits together an
interactive rebase is needed. To interactively rebase the last n commits use

	$ git rebase -i HEAD~n

Alternatively, you can find the commit that is base of your branch by running

	$ git merge-base my-branch edx/master

This will return a commit hash which can be used as argument to the rebase
command above.

To rename a commit log mark the commit entries with "r(eword)".
Mark commits that should be squashed with "s(quash)".

After saving another editor opens to change the commit logs or to choose the
common commit comment.

Interactively rebased changes can be pushed to the pull request branch with
force flag.

### Rebase a pull request

https://github.com/edx/edx-platform/wiki/How-to-Rebase-a-Pull-Request

## Foreign Pull Requests

https://help.github.com/articles/checking-out-pull-requests-locally/

### Checkout PR in a new local branch

	$ git checkout master
	$ git fetch origin pull/6848/head:6848_result_highlighting

A new branch 6848_result_highlighting is created with the PR changes.

### Create Branch with PRs and local branches

	$ git branch mybranch
	$ git checkout mybranch
	$ git pull upstream pull/6836/head
	$ git pull upstream pull/6848/head
	$ git pull origin 6851_copy_waypoint_notes

### Create Branch foreign branches
	$ git remote add other_user https://github.com/other_user/cgeo.git
	$ git fetch other_user
	$ git branch other_users_branch
	$ git checkout other_users_branch
	
Check history of other_user's branch.

	$ git log other_user/other_users_branch
	$ git pull other_user other_users_branch
	$ git log
