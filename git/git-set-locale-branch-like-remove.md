# How to set your locale branch exactly like remote

Setting your branch to exactly match the remote branch can be done in two steps:

    git fetch origin
    git reset --hard origin/master

If you want to save your current branch's state before doing this (just in case), you can do:

    git commit -a -m "Saving my work, just in case"
    git branch my-saved-work

Now your work is saved on the branch "my-saved-work" in case you decide you want it back (or want to look at it later or diff it against your updated branch).

Note that the first example assumes that the remote repo's name is "origin" and that the branch named "master" in the remote repo matches the currently checked-out branch in your local repo.
