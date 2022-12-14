# git-tuto

This project resum the most important information from git book. 
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
##### Staging Modified Files
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

##### Short Status

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

##### Ignoring Files
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


##### Viewing Your Staged and Unstaged Changes
If the git status command is too vague for you — you want to know exactly what you changed, not just which files were changed — you can use the git diff command.

![gitdiff](/images/git-diff.png)

That command compares what is in your working directory with what is in your staging area. The result tells you the changes you’ve made that you haven’t yet staged.