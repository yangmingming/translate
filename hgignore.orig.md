#.hgignore

How to ignore files.

目录  
1. Introduction   
2. How it works  
3. Limitations  
 
#1. Introduction

The .hgignore file sits in the [working directory](https://www.mercurial-scm.org/wiki/WorkingDirectory), next to the .hg folder. It is a file versioned as any other versioned file in the working directory, which is used to hold the content of the ignore patterns that are used for any command operating on the working directory.

Man Page: [hgignore(5)](http://www.selenic.com/mercurial/hgignore.5.html)

#2. How it works

Each path within the repository is presented to the ignore pattern matcher, so it would be presented with something like this:

    code
    code/something
    code/targets
    code/targets/platform
    target
    target/executable
    
This is just like the output of the Unix find command. To match only target at the top level of a repository, you would use this in .hgignore (using the regex syntax):

    ^target$

To match anything called target elsewhere in the repository, you would need to have something like this:

	/target$

The above pattern will ignore files and whole directories (by "pruning" those directories and thus ignoring their contents). If you need to ignore the contents of a directory, which is not in itself particularly useful, you would start with this pattern:

	/target/

Since the above pattern would only appear in paths for files below a directory called target, it would only match those files, not the directory itself. You could then extend this pattern to match specific files, however:

	/target/.*\.o$

This would match all files ending with .o below (within and in subdirectories at any depth of) the target directory.

#3. Limitations

There is no straightforward way to ignore all but a set of files. Attempting to use an inverted regex match will fail when combined with other patterns. This is an intentional limitation, as alternate formats were all considered far too likely to confuse users to be worth the additional flexibility.

refer: https://www.mercurial-scm.org/wiki/.hgignore 