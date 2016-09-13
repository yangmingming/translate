#Working directory

The working directory is the top-level directory in a [repository](https://www.mercurial-scm.org/wiki/Repository), in which the plain versions of files are available to read, edit and build. Files in the working directory are usually from the tip, but may be from older [revisions](https://www.mercurial-scm.org/wiki/Revision), or modified and not yet committed. The working directory is sometimes called the "working copy."

#目录
1. Manipulating the Working Directory
2. Parent(s)
3. When an update is needed
 
#1. Manipulating the Working Directory

It’s useful to think of the working directory as "the changeset I’m about to commit". If the working directory has no [local modifications](https://www.mercurial-scm.org/wiki/LocalModifications) it is said to be clean.

Use hg revert to discard all local modifications (see [revert](http://www.selenic.com/hg/help/revert)).

Use hg update to bring the working directory into sync with a particular [changeset](https://www.mercurial-scm.org/wiki/ChangeSet) (see [update](http://www.selenic.com/hg/help/update)).

To remove all files from the working directory (not the repository!), you can do

	hg update null

A [branch name](https://www.mercurial-scm.org/wiki/NamedBranches) can be set for the working directory.

Mercurial tracks various information about the working directory (see [DirState](https://www.mercurial-scm.org/wiki/DirState)).

#2. Parent(s)

A working directory has one or two parent revisions. The parent revision (or revisions) will become the parent revisions of the new revision which will eventually be created by a commit of the local modifications.

An hg update will change the parent revision, whereas hg revert will only modify the content of the working directory.

A working directory will only have two parent revisions as the result of a [merge](https://www.mercurial-scm.org/wiki/Merge), but only until that merge has been committed.

Immediately after a commit (or after an update -C), the working directory has exactly one parent revision, namely the newly committed (or updated-to) changeset. This is even the case if the newly committed changeset was a merge.

The command hg parents (without a revision specifier) lists the parent revision(s) of the working directory.

Example output for a single parent (no uncommitted merge):

    $ hg parents
    changeset:   2:86794f718fb1
    tag:         tip
    user:        mpm@selenic.com
    date:        Mon May 05 01:20:46 2008 +0200
    summary:     Express great joy at existence of Mercurial

Example output for two parent revisions (after an uncommitted merge):


    $ hg parents
    changeset:   2:c3844fde99f0
    user:        mpm@selenic.com
    date:        Tue May 06 20:10:35 2008 +0200
    summary:     Add description of hello.c
    
    changeset:   3:86794f718fb1
    tag:         tip
    parent:      1:82e55d328c8c
    user:        mpm@selenic.com
    date:        Mon May 05 01:20:46 2008 +0200
    summary:     Express great joy at existence of Mercurial

#3. When an update is needed

There are several ways to see if an update of your working directory is needed (see related [mailing list thread](http://www.selenic.com/pipermail/mercurial/2006-September/010951.html)):

To see the delta between the working directory and the tip, do:

	hg diff -r tip

To see what patches would be applied to the working directory on an update do:

	hg log -r tip:.

If the working directory is at the tip (that is, no update needed)

	hg id

will write "tip" after the changeset id.

[CategoryGlossary](https://www.mercurial-scm.org/wiki/CategoryGlossary)

refer: [https://www.mercurial-scm.org/wiki/WorkingDirectory](https://www.mercurial-scm.org/wiki/WorkingDirectory)
