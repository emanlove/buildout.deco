Bootstrapping
=============

Check out the buildout, bootstrap and run it, as usual::

    git clone git@github.com:plone/buildout.deco.git
    [...]
    cd buildout.deco
    python2.6 bootstrap.py 
    [...]
    ./bin/buildout
    [...]

You now have all required packages checked out via git into ``src/``, but they all point to a read-only URL, so you cannot (accidentally or not) push local changes to the plone repository. To get your changes into the plone repositry read on.

Working on packages
===================

The policy is to perform all work on a personal fork. For example, if ``$USER`` wants to work on ``plone.app.PACKAGE``:

  1. Visit ``PACKAGE`` on github (https://github.com/plone/plone.app.PACKAGE) and click the ''fork'' button.
  2. ``cd src/plone.app.PACKAGE``
  3. ``git remote add USER git@github.com:USER/plone.app.PACKAGE``
  4. ``git push -u USER``

Notice, that you **do not need to fork the buildout repository itself**, only the package you want to change.

Now you can work on the package(s), committing as you go along and push (to your fork) simply by issuing ``git push``.

Once you're ready and want your changes to be merged into the plone repository, you should **issue a pull request**. Visit your package on github and click ``Pull request`` and fill out the form. Easy peasy!

Update working packages with upstream changes
=============================================

  1. change into the package
  2. ``git pull origin master``

This fetches the upstream changes and applies them to your currently checked out branch. You can then, optionally, push those updates to your fork with ``git push``.

Merging pull requests
=====================

The easiest way is to perform the merge TTW on github itself. If you want to perform this manually, you need to add the plone repository with a read-write url, like so::

  cd src/plone.app.PACKAGE
  git remote add plone git@github.com:plone/plone.app.PACKAGE

Next, you will also need to add a remote for the fork you want to merge from::

  git remote add USER git@github.com:USER/plone.app.PACKAGE

Now you need to fetch both user's changes::

  git fetch USER

Finally, you can perform the actual merge:

  1. ``git checkout master`` *(merges are always performed on local checkouts of the master branch)*
  2. ``git pull`` *(make sure your local copy is up-to-date)*
  3. ``git merge --no-ff USER/master`` *(merge in the changes from the fork, ``--no-ff`` makes sure that this merge is recorded in the history with a merge commit of its own, which helps keeping the history clean)*
  4. ``git push plone`` *(if/once the merge was successful, push it back to github.)*
