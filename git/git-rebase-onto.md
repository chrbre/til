# Question: How can we move a complete subbranch from one parent node/branch to another:

__In short__: ``git rebase --onto <newparent> <oldparent>``

__Some explanations__

The correct syntax to rebase ``B`` on top of ``A`` using ``git rebase --onto`` in your case is:

	git checkout B
	git rebase --onto A B^

or rebase ``B`` on top of ``A`` starting from the commit that is the parent of ``B`` referenced with ``B^`` or ``B~1``.

If you're interested in the difference between ``git rebase <branch>`` and ``git rebase --onto <branch>`` read on.

## The Quick: git rebase

``git rebase <branch>`` is going to rebase the branch you currently have checked out, referenced by ``HEAD``, on top of the latest commit that is reachable from ``<branch>`` but not from ``HEAD``.

This is the most common case of rebasing and arguably the one that requires less planning up front.

          Before                           After
    A---B---C---F---G (branch)        A---B---C---F---G (branch)
             \                                         \
              D---E (HEAD)                              D---E (HEAD)

In this example, ``F`` and ``G`` are commits that are reachable from ``branch`` but not from ``HEAD``. Saying ``git rebase branch`` will take ``D``, that is the first commit after the branching point, and rebase it (i.e. change its parent) on top of the latest commit reachable from ``branch`` but not from ``HEAD``, that is ``G``.

## The Precise: git rebase --onto with 2 arguments

``git rebase --onto`` allows you to rebase *starting from a specific commit*. It grants you exact control over what is being rebased and where. This is for scenarios where you need to be precise.

For example, let's imagine that we need to rebase ``HEAD`` precisely on top of ``F`` starting from ``E``. We're only interested in bringing ``F`` into our working branch while, at the same time, we don't want to keep ``D`` because it contains some incompatible changes.

          Before                           After
    A---B---C---F---G (branch)        A---B---C---F---G (branch)
             \                                     \
              D---E---H---I (HEAD)                  E---H---I (HEAD)

In this case, we would say ``git rebase --onto F D``. This means:

Rebase the commit reachable from ``HEAD`` whose parent is ``D`` on top of ``F``.

In other words, change the parent of ``E`` from ``D`` to ``F``. The syntax of ``git rebase --onto`` is then ``git rebase --onto <newparent> <oldparent>``.

Another scenario where this comes in handy is when you want to quickly remove some commits from the current branch without having to do an interactive rebase:

          Before                       After
    A---B---C---E---F (HEAD)        A---B---F (HEAD)

In this example, in order to remove ``C`` and ``E`` from the sequence you would say ``git rebase --onto B E``, or rebase ``HEAD`` on top of ``B`` where the old parent was ``E``.

## The Surgeon: git rebase --onto with 3 arguments

``git rebase --onto`` can go one step further in terms of precision. In fact, it allows you to rebase an arbitrary range of commits on top of another one.

Here's an example:

          Before                                     After
    A---B---C---F---G (branch)                A---B---C---F---G (branch)
             \                                             \
              D---E---H---I (HEAD)                          E---H (HEAD)

In this case, we want to rebase the exact range ``E---H`` on top of ``F``, ignoring where ``HEAD`` is currently pointing to. We can do that by saying ``git rebase --onto F D H``, which means:

Rebase the range of commits whose parent is ``D`` up to ``H`` on top of ``F``.

The syntax of ``git rebase --onto`` with a range of commits then becomes ``git rebase --onto <newparent> <oldparent> <until>``. The trick here is remembering that the commit referenced by ``<until>`` is included in the range and will become the new ``HEAD`` after the rebase is complete.
