#工作目录

工作目录是[仓库](https://www.mercurial-scm.org/wiki/Repository)中顶级的目录, 其中是文件有效可读、可编辑、可构建的普通版本。工作目录中的文件经常来自于tip，但是也可以来自旧的[修订版本](https://www.mercurial-scm.org/wiki/Revision),或者是修改过但是没有提交的版本。 工作目录有的时候也被称为工作拷贝。

#目录
1. 操控工作目录
2. 继承
3. 当更新有必要时
 
#1. 操控工作目录

非常有必要把工作目录当成一个“将要提交的变更”。如果工作目录没有[本地修改](https://www.mercurial-scm.org/wiki/LocalModifications) 我们就说它是干净的.

使用 hg revert 可以丢弃所有本地修改(参照 [revert](http://www.selenic.com/hg/help/revert)).

使用 hg update 可以是工作目录同步到一个特定的[变更](https://www.mercurial-scm.org/wiki/ChangeSet) (参照 [update](http://www.selenic.com/hg/help/update)).

为了删除工作目录(不是仓库)的所有文件, 你可以

	hg update null

可以为工作目录设置一个[分支名字](https://www.mercurial-scm.org/wiki/NamedBranches) 。
Mercurial可以跟踪关于工作目录的不同信息。 (参考 [DirState](https://www.mercurial-scm.org/wiki/DirState)).

#2. 继承

一个工作目录可以有一个或者两个继承。本地的修改的提交，最终会创建一个新的版本，而继承的版本，将会成为这个新版本的父版本。

执行一次 hg update 可以修改继承修订, 然而 hg revert 仅仅可以修改工作目录下的内容。

[merge](https://www.mercurial-scm.org/wiki/Merge)的结果会导致一个工作目录有两个继承的修订，直到merge被提交。

commit执行之后，会立马执行（或者执行一次 update -C），工作目录就和其中一个继承修订完全相同了，也就是说，最新的commit（或者 update -C）修订。这也是最新的commit修订是一个merge的情况。

命令 hg parents （没有指定特定的修订）列出工作目录下继承的修订。

下面举例输出只有一个继承的情况（没有未提交的merge）：

    $ hg parents
    changeset:   2:86794f718fb1
    tag:         tip
    user:        mpm@selenic.com
    date:        Mon May 05 01:20:46 2008 +0200
    summary:     Express great joy at existence of Mercurial

下面举例输出有两个继承的情况（在一个未提交的merge之后）：


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

#3. 当更新有必要时

有好多种办法可以查看你的工作目录是否有必要进行一次update (相关参考 [mailing list thread](http://www.selenic.com/pipermail/mercurial/2006-September/010951.html)):

为了对比工作目录和tip的区别，可以进行如此操作：

	hg diff -r tip

为了查看工作目录在进行一次update之后打的补丁，可以进行如下操作：

	hg log -r tip:.

如果工作目录就是tip（也就说，不需要update）

	hg id

将会在变更id之后，写上tip。

[CategoryGlossary](https://www.mercurial-scm.org/wiki/CategoryGlossary)

参考: [https://www.mercurial-scm.org/wiki/WorkingDirectory](https://www.mercurial-scm.org/wiki/WorkingDirectory)
