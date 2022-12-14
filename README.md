# git-tuto

This project resum important informations from git book. 
https://git-scm.com/book
## Git scenariis 
### What is Git ?
#### Git vs VCS

Git stores and thinks about information in a very different way, and understanding these differences will help you avoid becoming confused while using it.

##### Snaphots, not differences:

![delta](./images/deltas.png)
Storing data as changes to a base version of each file

Git thinks of its data more like a series of snapshots of a miniature filesystem. With Git, every time you commit, or save the state of your project Git takes a pcitore of what all your file like at the moment and stores a reference to that snapshot.
So, when files have not changed, Git reference it from the previous version.
It is tipycally a *stream of snapshot*. Very effecient ! 
![snpashots](/images/snapshots.png)
Storing data as snapshots of the project over time


##### Every Operation Is Local:

```
git clone git@github.com:Guigouu/git-tuto.git
```

You have the entire history of the project right there on your local disk, most operations seem almost instantaneous.

So to Browse history of the entire project, git doesn not need to go out to the server.
Same for the most operations, if you are in a airplane environment you can commit locally and push later. 

##### Git Has Integrity:

Everything in Git in checksummed before it is stored and is then referred to by that checksum. 
![snpashots](/images/git-log.png)

This means it’s impossible to change the contents of any file or directory without Git knowing about it. This functionality is built into Git at the lowest levels and is integral to its philosophy. You can’t lose information in transit or get file corruption without Git being able to detect it.


##### The Three States

- Modified means that you have changed the file but have not committed it to your database yet.

- Staged means that you have marked a modified file in its current version to go into your next commit snapshot.

- Committed means that the data is safely stored in your local database.


```
$ echo 'My Project' > README
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)

    README

nothing added to commit but untracked files present (use "git add" to track)
```
Untracked basically means that Git sees a file you didn’t have in the previous snapshot (commit), 

```
$ git add README
```
### Staging Modified Files
```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)

    new file:   README
```
```
echo "My contribution" >> README

$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
    modified:   README

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   README
```

### Short Status

```
$ git status -s
 M README
A  lib/git.rb
M  lib/simplegit.rb
?? LICENSE.txt
```
- New files that aren’t tracked have a ?? next to them
- New files that have been added to the staging area have an A
- Modified files have an M and so on. 

### Ignoring Files
```
$ cat .gitignore
# Compiled files
*.tfstate
*.tfstate.backup

# Module directory
.terraform/
connection.tf
terraform.tfvars
.idea
.vscode
```
- Blank lines or lines starting with # are ignored.

- Standard glob patterns work, and will be applied recursively throughout the entire working tree.

- You can start patterns with a forward slash (/) to avoid recursivity.

- You can end patterns with a forward slash (/) to specify a directory.

- You can negate a pattern by starting it with an exclamation point (!).


###### Tip:
GitHub maintains a fairly comprehensive list of good .gitignore file examples for dozens of projects and languages at https://github.com/github/gitignore if you want a starting point for your project.


### Viewing Your Staged and Unstaged Changes
If the git status command is too vague for you — you want to know exactly what you changed, not just which files were changed — you can use the git diff command.

![gitdiff](/images/git-diff.PNG)

That command compares what is in your working directory with what is in your staging area. The result tells you the changes you’ve made that you haven’t yet staged.

### Committing Your Changes
Now that your staging area is set up the way you want it, you can commit your changes. 

Remember that anything that is still unstaged — any files you have created or modified that you haven’t run git add on since you edited them — won’t go into this commit.

```
git commit
```
Alternatively, you can type your commit message inline with the commit command by specifying it after a -m flag, like this
```
$ git commit -m "Story 182: fix terraform stack"
```

### Skipping the Staging Area

```
$ git commit -a -m 'Add new benchmar

```
Adding the -a option to the git commit command makes Git automatically stage every file that is already tracked before doing the commit, letting you skip the git add part

/!\ This is convenient, but be careful; sometimes this flag will cause you to include unwanted changes.


### Removing Files

To remove a file from Git, you have to remove it from your tracked files and then commit. 
If you simply remove the file from your working directory, it shows up under the “Changes not staged for commit” (that is, unstaged) area of your git status output:

```
$ rm PROJECTS.md
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    PROJECTS.md

no changes added to commit (use "git add" and/or "git commit -a")
```
Then, if you run git rm, it stages the file’s removal:

```

$ git rm PROJECTS.md
rm 'PROJECTS.md'
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    deleted:    PROJECTS.md
```
The next time you commit, the file will be gone and no longer tracked.

__You may want to keep the file on your hard drive but not have Git track it anymore.__
if you forgot to add something to your .gitignore file and accidentally staged it, like a large log file or a bunch of .a compiled files.
```
$ git rm --cached README
```
### Moving Files

```
$ git mv README.md README
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    renamed:    README.md -> README
```
However, this is equivalent to running something like this:
```
$ mv README.md README
$ git rm README.md
$ git add README
```

### Viewing the Commit History
```
$ git clone https://github.com/schacon/simplegit-progit
```
```
$ git log
commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    Change version number

commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Sat Mar 15 16:40:33 2008 -0700

    Remove unnecessary test

commit a11bef06a3f659402fe7563abf99ad00de2209e6
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Sat Mar 15 10:31:28 2008 -0700

    Initial commit
```

A huge number and variety of options to the git log command are available to show you exactly what you’re looking for. Here, we’ll show you some of the most popular.
One of the more helpful options is -p or --patch, You can also limit the number of log entries displayed, such as using -2 to show only the last two entries.

```

$ git log -p -2
commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    Change version number

diff --git a/Rakefile b/Rakefile
index a874b73..8f94139 100644
--- a/Rakefile
+++ b/Rakefile
@@ -5,7 +5,7 @@ require 'rake/gempackagetask'
 spec = Gem::Specification.new do |s|
     s.platform  =   Gem::Platform::RUBY
     s.name      =   "simplegit"
-    s.version   =   "0.1.0"
+    s.version   =   "0.1.1"
     s.author    =   "Scott Chacon"
     s.email     =   "schacon@gee-mail.com"
     s.summary   =   "A simple gem for using Git in Ruby code."

commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Sat Mar 15 16:40:33 2008 -0700

    Remove unnecessary test

diff --git a/lib/simplegit.rb b/lib/simplegit.rb
index a0a60ae..47c6340 100644
--- a/lib/simplegit.rb
+++ b/lib/simplegit.rb
@@ -18,8 +18,3 @@ class SimpleGit
     end

 end
-
-if $0 == __FILE__
-  git = SimpleGit.new
-  puts git.show
-end
```
```
 git log --stat
```
```
git log --pretty=oneline
```
```
git log --pretty=format:"%h - %an, %ar : %s"
```
```
git log --pretty=format:"%h %s" --graph
```
### Limiting Log Output

```
git log --since=2.weeks
```
```
git log --pretty="%h - %s" --author='Guillaume NAIRI' --since="2022-08-01" --no-merges
```

### Git Basics - Undoing Things
At any stage, you may want to undo something. 
One of the common undos takes place when you commit too early and possibly forget to add some files, or you mess up your commit message. If you want to redo that commit, make the additional changes you forgot, stage them, and commit again using the --amend option:

```
git commit --amend
```
As an example, if you commit and then realize you forgot to stage the changes in a file you wanted to add to this commit, you can do something like this:
```
$ git commit -m 'Initial commit'
$ git add forgotten_file
$ git commit --amend
```

/!\ It will not replace the commit already pushed, but you end up with a single commit — the second commit replaces the results of the first if it is staged locally.
```
git log -p -1
```


### Unstaging a Staged File


You accidentally type git add * and you wanted commit two files separatly:

```
$ git add *
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    renamed:    README.md -> README
    modified:   CONTRIBUTING.md
```

```
echo "MY modification to UNDO" > UNDO.md
git add UNDO.md
git status -s
A UNDO.md
```

```
$ git reset HEAD UNDO.md
Unstaged changes after reset:
M	UNDO.md
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   UNDO.md


$ git status -s
?? UNDO.md
```

### Unmodifying a Modified File


What if you realize that you don’t want to keep your changes to the CONTRIBUTING.md file? How can you easily unmodify it — revert it back to what it looked like when you last committed