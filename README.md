# Git Tutorial

1. login into github and create new repository
2. goto windows d:\workspace and click mouse right key
3. select ***Git Bash Here***

###
	blogw@blogw-PC MINGW64 /d/workspace
	$ git clone https://github.com/blogw/study.git
	Cloning into 'study'...
	remote: Counting objects: 3, done.
	remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
	Unpacking objects: 100% (3/3), done.
	Checking connectivity... done.
###
	$ cd study

	blogw@blogw-PC MINGW64 /d/workspace/study (master)
	$ git add *
	
	blogw@blogw-PC MINGW64 /d/workspace/study (master)
	$ git status
	On branch master
	Your branch is up-to-date with 'origin/master'.
	Changes to be committed:
	  (use "git reset HEAD <file>..." to unstage)
	
	        new file:   solr/img/dynamicfield.png
	        new file:   solr/solr6_install.md
	        new file:   solr/solr6_query.md
	
	blogw@blogw-PC MINGW64 /d/workspace/study (master)
	$ git commit -m 'solr'
	[master 7e63bcb] solr
	 3 files changed, 156 insertions(+)
	 create mode 100644 solr/img/dynamicfield.png
	 create mode 100644 solr/solr6_install.md
	 create mode 100644 solr/solr6_query.md
	
	blogw@blogw-PC MINGW64 /d/workspace/study (master)
	$ git push
	warning: push.default is unset; its implicit value has changed in
	Git 2.0 from 'matching' to 'simple'. To squelch this message
	and maintain the traditional behavior, use:
	
	  git config --global push.default matching
	
	To squelch this message and adopt the new behavior now, use:
	
	  git config --global push.default simple
	
	When push.default is set to 'matching', git will push local branches
	to the remote branches that already exist with the same name.
	
	Since Git 2.0, Git defaults to the more conservative 'simple'
	behavior, which only pushes the current branch to the corresponding
	remote branch that 'git pull' uses to update the current branch.
	
	See 'git help config' and search for 'push.default' for further information.
	(the 'simple' mode was introduced in Git 1.7.11. Use the similar mode
	'current' instead of 'simple' if you sometimes use older versions of Git)
	
	Counting objects: 7, done.
	Delta compression using up to 8 threads.
	Compressing objects: 100% (6/6), done.
	Writing objects: 100% (7/7), 27.86 KiB | 0 bytes/s, done.
	Total 7 (delta 0), reused 0 (delta 0)
	To https://github.com/blogw/study.git
	   9650f30..7e63bcb  master -> master
