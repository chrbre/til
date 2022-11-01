# How can I add a file to the last commit

	git add the_left_out_file
	git commit --amend --no-edit

The ``--no-edit`` flag allows to make an amendment to the commit without changing the commit message.

**Warning**

You should never amend public commits that you already pushed to a public repository, because amend is actually removing the last commit from the history and creating a new commit with the combined changes from that commit and new added when amending.
