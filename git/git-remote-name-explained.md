# Remote name explained (origin)

In Git, "origin" is __a shorthand name for the remote repository that a project was originally cloned from__. More precisely, it is used instead of that original repository's URL - and thereby makes referencing much easier. Note that origin is by no means a "magical" name, but just a standard convention.

Although it makes sense to leave this convention untouched, you could perfectly rename it without losing any functionality.

## The origin Remote

When you clone a repository with git clone, it automatically creates a remote connection called origin pointing back to the cloned repository. This is useful for developers creating a local copy of a central repository, since it provides an easy way to pull upstream changes or publish local commits. This behavior is also why most Git-based projects call their central repository origin.

## Showing your remotes

By default, the ``git remote`` command will list previously stored remote connections to other repositories. This will produce single line output that lists the names of "bookmark" name of remote repos.

	$ git remote
	origin
	upstream
	other_users_repo

Invoking ``git remote`` with the ``-v`` option will print the list of bookmarked repository names and additionally, the corresponding repository URL. The ``-v`` option stands for "verbose". Below is example output of verbose ``gitremote`` output.

	git remote -v
	origin  git@bitbucket.com:origin_user/reponame.git (fetch)
	origin  git@bitbucket.com:origin_user/reponame.git (push)
	upstream    https://bitbucket.com/upstream_user/reponame.git (fetch)
	upstream    https://bitbucket.com/upstream_user/reponame.git (push)
	other_users_repo    https://bitbucket.com/other_users_repo/reponame (fetch)
	other_users_repo    https://bitbucket.com/other_users_repo/reponame (push)

## Adding Remote Repositories

The ``git remote add`` command will create a new connection record to a remote repository. After adding a remote, you’ll be able to use as a convenient shortcut for in other Git commands. For more information on the accepted URL syntax, view the "Repository URLs" section below. This command will create a new record within the repository's ``./.git/config``. An example of this config file update follows:

	$ git remote add fake_test https://bitbucket.com/upstream_user/reponame.git; [remote "remote_test"] 
   	   url = https://bitbucket.com/upstream_user/reponame.git 
   	   fetch = +refs/heads/*:refs/remotes/remote_test/*

## Inspecting a Remote

The show subcommand can be appended to git remote to give detailed output on the configuration of a remote. This output will contain a list of branches associated with the remote and also the endpoints attached for fetching and pushing.

	git remote show upstream
	* remote upstream
   	   Fetch URL: https://bitbucket.com/upstream_user/reponame.git
   	   Push URL: https://bitbucket.com/upstream_user/reponame.git
   	   HEAD branch: main
   	   Remote branches:
    	  main tracked
      	  simd-deprecated tracked
      	  tutorial tracked
   	  Local ref configured for 'git push':
    	  main pushes to main (fast-forwardable)
