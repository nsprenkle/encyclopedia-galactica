# Git

## Big Ideas

Git is a version control system used to track changes to a project over time.

Project changes are captured in commits which form a snapshot of current state including files/directories and versions.

Commits chain together in a tree structure where each commit is a node in the tree  which references previous, or parent, commits. This gives us the notion of a "history" where we can track previous project states.

> Behind the scenes: every element in git is referenced by a hash of the element's data. The hash points to a location in the `.git` directory folder structure where the compressed element resides. The data is just compressed text so it is possible to browse the data structures directly if you're curious. You shouldn't have to do this unless you've done something terribly wrong.

Git is also distributed which means you get a full-fledged copy of the repository on your own machine to work with. This is in contrast to tools like SVN where there is one central server and repository; in SVN you act only as a client, sending or receiving changes to the server. A distributed system has many benefits but it is important to note that changes will only exist on your copy of the repository unless you explicitly propagate changes elsewhere.

Git allows us to work with our files as they existed at any point during the commit history by checking out a commit. This replaces the files in our working tree/directory, in our file system where we normally interact with files. Git is pretty smart about making sure you don't lose work, so it will typically warn you if you try to wipe out unsaved changed in your working tree.

Branches are a feature of git which let us isolate different areas of work. 

> Behind the scenes: everything in git is referenced by its hash value. A hash is a fixed length string computed by running the contents of a file through an algorithm.

## Workflows

### Fork & Merge
  1. Fork
     1. Fork the upstream repo
     2. Clone the repo locally
  2. Develop
     1. Develop, commit, push
  3. Integrate
     1. Integrate upstream changes by pulling from the upstream branch and pushing back to the fork
     2. Commit and push again to origin if changes were made during the integration phase
  4. Review & publish (GitHub)
     1. Create a pull request for pulling your branch into EBSCOIS
     2. Code reviewAccepted: merge code and delete branchChanges requested: make changes and proceed from develop step
  5. Synchronize
    a. Propagate changes from EBSCOIS to local and fork

## Resources

• [Git Book at git-scm](https://git-scm.com/book/en/v2), basically the bible on Git.