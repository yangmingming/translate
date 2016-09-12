#.hgignore
如何忽略文件。
#目录
1. 简介
2. 如何工作
3. 限制

#1. 简介
.hgignore 文件是存放在[工作目录](https://www.mercurial-scm.org/wiki/WorkingDirectory)的一个文件，和.hg文件夹在同一个文件夹【笔者注：即同一级】。它是一个版本控制文件，和其他的版本控制文件一样，它用来通过在工作目录中的命令操作来限制忽略模式对应的文件。

说明文档: [hgignore(6)](http://www.selenic.com/mercurial/hgignore.5.html)

#2. 如何工作
仓库里面的每一个路径都是和呈现在ignore模式匹配一样，所以它可以按照如下的方式呈现：

    code
    code/something
    code/targets
    code/targets/platform
    target
    target/executable

这和Unix下find命令行的输出一样。为了仅仅匹配仓库中顶层的target，你可以在.hgignore中按照如下的方式编写（使用正则语法）

	^target$

为了匹配仓库中其他地方的名为target目标，你需要写成下面的样子：

	/target$

以上的模式将要忽略文件或者整个目录（通过“修建”这些目录从而实现忽略内容的目的）。如果你希望忽略文件夹里面的内容的话，文件夹自身尤其有用，你需要以下面的模式开始：

	/target/

通过上面的模式，仅仅可以出现在路径为低于目录的文件为“target”的情况，他仅仅可以匹配这些文件，而不是目录本身。然而，你接下来可以扩展这个模式来匹配特定的文件，如下：

	/target/.*\.o$

这种模式将匹配所有的以.o结尾包含在target目录之下（包含当前目录和任意层级的多级目录）的文件。

#3.限制

没有直接了当的方式来忽略所有的文件，但是可以是一组文件。尝试使用一个颠倒的正则匹配与其他的正则相结合将会失败。这是一个故意的约束，作为备用的格式是所有的考虑让用户产生疑惑相对于额外的灵活性（ This is an intentional limitation, as alternate formats were all considered far too likely to confuse users to be worth the additional flexibility.）。

转载： https://www.mercurial-scm.org/wiki/.hgignore 