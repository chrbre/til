# How do I rename a branch in git

## locally

1. Switch to the branch you want to rename
2. ``git branch -m new-branch-name``

	or of you are on the main branch:

	``git branch -m old-branch new-branch``

## Remote

First change the name of the locale branch. Then:

1. Push the <new_name> local branch and reset the upstream branch:

	``git push origin -u <new_name>``

2. Delete the <old_name> (!)__remote__(!) branch:

	``git push origin --delete <old_name>``
