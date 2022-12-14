# git-tuto

This project resum the most important information from git book. 
https://git-scm.com/book
## Git scenariis 
### What is Git ?
#### Git vs VCS

Git stores and thinks about information in a very different way, and understanding these differences will help you avoid becoming confused while using it.

Snaphots, not differences:

![delta](./images/deltas.png)
Storing data as changes to a base version of each file

Git thinks of its data more like a series of snapshots of a miniature filesystem. With Git, every time you commit, or save the state of your project Git takes a pcitore of what all your file like at the moment and stores a reference to that snapshot.
So, when files have not changed, Git reference it from the previous version.
It is tipycally a *stream of snapshot*. Very effecient ! 
![snpashots](/images/snapshots.png)
Storing data as snapshots of the project over time


Every Operation Is Local:

"""
git clone git@github.com:Guigouu/git-tuto.git
"""

You have the entire history of the project right there on your local disk, most operations seem almost instantaneous.

So to Browse history of the entire project, git doesn not need to go out to the server.
Same for the most operations, if you are in a airplane environment you can commit locally and push later. 

Git Has Integrity:

Everything in Git in checksummed before it is stored and is then referred to by that checksum. 
![snpashots](/images/git-log.png)