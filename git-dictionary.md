## Dictionary – terms as git uses them

**remote branch**: the actual branch that exists on remote

**remote-tracking branch**: a local pointer to the state of the remote branch when you last connected to it

**remote-tracking branch name**: name by which you locally refer to remote-tracking branch; \<remote\>/\<branch\>

**tracking branch**: a local branch that has an assigned remote branch to track

**working tree**: local working directory; contains the files from your current branch as well as untracked files

**index**: staging area that holds a snapshot of your changes that will be included in the next commit


## Graph theory
[Reference](https://think-like-a-git.net/sections/graph-theory.html)

Graph theory is a way of encoding information about two aspects of a map: places to go (**nodes**), and ways to get there (**edges**).
A directed graph has arrows that tell you the relation (edge) is one-way; below, the relation is "follows" or "is subsequent to":

![reachability-example](https://github.com/user-attachments/assets/0757f710-3623-4093-ae23-d3d6104f9f37)

A git commit consists of two things: (1) a pointer to the state of your code at some moment in time, and (2) zero or more pointers to "parent" commits. 
A git commit is a node in a graph, and each one of those nodes can point to other nodes that came before them.

![graphs-and-git](https://github.com/user-attachments/assets/c47415b1-de9e-4733-a8b3-233d2665f6dc)

A **reference** is a pointer to a commit. There are a few kinds of references, and the difference between them is how and when they move (move = ID of the commit that it points to is updated).
One consists entirely of a file in .git/refs/ that contains the 40-byte identifier of the commit that the reference points to.
  - _Local branch references_ are specific to your local repository. Commands that affect them include `commit`, `merge`, `rebase`, and `reset`.
  - _Remote branch references_ are specific to the remote repository. Commands that affect them include `fetch` and `push`.
  - _Tag references_ never move, which makes them useful for marking specific versions of a software package or what exactly was deployed at some point.
  - HEAD always points to the most recent commit in the current branch. It moves when you make a commit. In a _detached HEAD_ state, HEAD points to a specific commit rather than to the latest commit on a branch.


A commit's ID (SHA-1 hash) contains several pieces of information: the contents of the commit, and the IDs of it(s) parent commit(s).
References make commits reachable so that you can get back to them and, when git does its cleaning, it doesn't delete them. 
(Eventually, Git will decide that it's time to run garbage collection. (You can trigger this process yourself, using git gc.) Starting from every branch and every tag, Git walks back through the graph, building a list of every commit it can reach. Once it's reached the end of every path, it deletes all the commits it didn't visit.)

Because branches are references, and references point to commits, creating a branch is essentially a way to create a checkpoint at a certain commit.
