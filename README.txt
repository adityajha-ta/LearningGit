Git stores the files in the form of streams of snapshots. 

Git has three main stages-
	- Modified: Here we make the changes in the files
	- Stages: marked the modified file in its current version to be commited 
	- Commited means data is stored in the local database

Start with 'git config --list --show-origin': lists down all the current settings.

Take an empty repository, start with 'git init': creates a folder ./.git/

Git Internals:

	'Plumbing' commands are low level subcommands whereas 'Porcelain' commands are the user-friendly commands.
	Inside the .git directory the four important entries are:
		- objects directories stores all the content of the database
		- refs directory stores pointers into commit objects in the data
		- HEAD file points to the branch currently checked out
		- index directory stores the staging area information.
	
	Git is a key-value data store, i.e. a map. We can insert any information and Git will return us a unique key to use later to retrieve the data. To store data, there is a blob object which has a unique SHA-1 key. Trees along with blobs store the extensive data of any repository. Tree object stores a pointer to all the blobs and sub-trees within it. We can construct our own tree by first updating the index folder (staging our files), then creating blobs which store the data and has unique addresses and we 'git write-tree' to store these blobs. It stores all the versions of the staged files. Finally, we commit these tracked changes by storing some additional information about the changes -- thus we commit by creating a commit-tree where we can pass the SHA-1 of a single tree and of any preceeding commits.
	
	Instead of remembering the commit address, we can reference the address with something more readable -- comes in the .git/ref directory -- can use --update-refs to update a reference to a new address, it is called when we 'git branch <branch>'. HEAD is the symbolic reference to the branch which is checked out, we can commit the changes to the branch where the HEAD is. When we 'git commit', the parent of the git object is the address where the HEAD points.

	
'git cat-file -p file' inspects the contents of the 'file' object and displays it.
'git diff' shows the difference between the tracked and untracked progress.
'git rm file' to stage the deletion of the file.
'git log -p -2': -p stands for patch, and we'll see comparison b/w the last 2 commits.
'git log --pretty=format' formats the log files in a specific way, might be useful for parsing.
git log has many important functionalities in terms of version control and debugging.
To UNDO a commit, we can 'git commit --ammend'; a change from staged to untracked -- move the HEAD to the file which needs to be unstaged.

'git remote add origin url' used to add a remote repository. There might be other versions of the project present remotely -- use of remote repository.

'git push origin master': pushing the master branch to origin server. Right steps is to first fetch data from the origin server, incorporating it with the current branch and then push.

'git remote show origin': lists down all the remote repos as well as remote branches

[TBD: git tag and git alias]

------------------------------------------------
Git Branching:

A branch in git is a movable pointer to one of the commits. The default branch name is master, with every new commit the master branch moves forward.
'git branch <branch>': creates a new pointer to the same commit where HEAD is. (-d to delete the branch)
'git checkout <branch>': moves HEAD to this branch, we can now commit in this branch
	Before switching branches, its best to not keep any uncommited changes
'git merge <branch>': merges the <branch> with the current branch

	
