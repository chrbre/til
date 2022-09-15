# Managing remote repositories

## About remote repositories

A remote URL is Git's fancy way of saying "the place where your code is stored." That URL could be your repository on GitHub, or another user's fork, or even on a completely different server.

You can only push to two types of URL addresses:

- An HTTPS URL like ``https://github.com/user/repo.git``
- An SSH URL, like ``git@github.com:user/repo.git``

Git associates a remote URL with a name, and your default remote is usually called origin.

## Creating remote repositories

You can use the ``git remote add`` command to match a remote URL with a name. For example, you'd type the following in the command line:

	git remote add origin  <REMOTE_URL> 

This associates the name ``origin`` with the ``REMOTE_UR``L.

You can use the command ``git remote set-url`` to change a remote's URL.

## Adding a remote repository

To add a new remote, use the ``git remote add`` command on the terminal, in the directory your repository is stored at.

The ``git remote add`` command takes two arguments:

- A remote name, for example, ``origin``
- A remote URL, for example, ``https://github.com/user/repo.git``

For example:

	$ git remote add origin https://github.com/user/repo.git
	# Set a new remote

	$ git remote -v
	# Verify new remote
	> origin  https://github.com/user/repo.git (fetch)
	> origin  https://github.com/user/repo.git (push)

## Changing a remote repository's URL

The ``git remote set-url`` command changes an existing remote repository URL.

The ``git remote set-url`` command takes two arguments:

- An existing remote name. For example, origin or upstream are two common choices.
- A new URL for the remote. For example:
	- If you're updating to use HTTPS, your URL might look like:
		``https://github.com/USERNAME/REPOSITORY.git``
	- If you're updating to use SSH, your URL might look like:
		``git@github.com:USERNAME/REPOSITORY.git``

__Example__:

In order to change the URL of a Git remote, you have to use the “``git remote set-url``” command and specify the name of the remote as well as the new remote URL to be changed.

	$ git remote set-url <remote_name> <remote_url>

For example, let’s say that you want to change the URL of your Git origin remote.

In order to achieve that, you would use the “set-url” command on the “origin” remote and you would specify the new URL.

	$ git remote set-url origin https://git-repo/new-repository.git

In order to verify that the changes were made, you can use the “git remote” command with the “-v” option (for verbose)

	$ git remote -v
