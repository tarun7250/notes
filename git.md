GIT
git init . // to initialize working git repo
git init folder_name // create a git repo with name folder_name
git init . —bare // to initialize current folder as bare repo (used in central or remote repos) ssh into remote computer and create a bare repository there *********
git init . -Q
git init . —Quiet //does not print any message
git init . —TEMPLATE=/ablsolute/path/to/template
git init . —SEPARATE_GIT_DIR= //?
git init . —SHARED=TRUE/FALSE …… // unix specific gives access to users 
SVN // subversion software

git clone <repo> —bare // acts as central repo and is not associated with the remote repo*******
git clone <repo> —mirror // —bare is added automatically although it will clone the existing refs and maintain remote branch tracking functionality ********
git clone —template=<template_directory> <repo_location> // creates a clone and applies the template 

//git clone works with three url protocols
//ssh
ssh://[user@]host.xz[:port]/path/to/repo.git/ 
//git // runs on port 9418
git://host.xz[:port]/path/to/repo.git/  
//http
http[s]://host.xz[:port]/path/to/repo.git/  
//Three trees of git -> working area, Staging area, commit history
git add <file> //stage changes in file for commit
git add <directory> //stage change in a folder
????chunk**

git add . // to stage all changes in repo
git reset // used to undo git add command*******
git commit -m “” // add staged files to commit
git commit -am “” // except for untracked files it does stage and commit directly
git commit —amend // rather creating new commit modifies the last commit*******

git stash // takes all the staged and non staged files and saves them away for later use 
//stash remains in local repository
git stash pop // removes stash top and applies on the working directory
git stash apply // applies stash keeping the changes without removing the stash
//git won’t apply stash to untracked(new files) of ignored files by default*****
git stash -u
git stash —include-untracked // tells to take untracked files also
git stash -a // takes ignored files also into account
git stash list // to view all stashes
git stash save “message” // to annotate stash
git stash apply stash@{2} // to apply stashed things
?????????????stash show
git stash branch <branch_name> stash@{2} // creates a new branch applying stash
git stash drop stash@{2} //deletes the particular stash
git stash clear //to delete all the stashes
????????????internal working of git stash git reflog???how dag is made and difference is tracked

//git ignore patterns
* / matches anything 
[0-9] 
[a-z] for specifying ranges
git check-ignore -v debug.log // <file containing the pattern> : <line number of the pattern> : <pattern>    <file name>


git fetch origin/feature_branch // fetches origin feature branch only
git fetch —all <-> git fetch // fetches all branches inside origin/branches
// then can be merged using git merge origin/main(from main) or may be rebased using git rebase main(from origin/main)

git log // will show just the log of the current branch
git log —branches=* // will show the log of all the branches
/// detached  - garbage collected from time to time


//git merge //fast forward 3 way resolving conflicts
git merge branch_to_merge // called while being on the the branch to apply merge, commit can be used instead of branch_to_merge

<<<<<<
same
======

>>>>>>
different



git pull // git fetch + git merge
git pull remote
git pull —rebase remote // remote 


//deleting branch remotely
git branch -D branch_name
git push origin :branch_name

git push <remote name> // pushes in fast forward mode // if not possible then shows error pull solve merge conflicts then again push
git push <remote name> —force // when fast forward is not possible removes any commit that happened and adds 

git status // tells you which files are  untracked staged and not staged

git branch branch-name //creates new branch with branch name
git branch -d branch-name // deletes branch if all changes are merged
git branch -D branch-name // deletes the branch 
git branch -m new-branch-name // renames the branch
git branch —list // list all the local branches
git branch -a // list all the remote branches

// deletes branch from remote repository
git push origin —delete branch-name
git push origin :branch-name


git checkout branch-name //point head on that branch
git checkout -b new-branch //creates a new branch of not there creates a new branch from the existing head
git checkout -b new-branch existing-branch // creates a new branch from existing branch to new branch
git checkout commit-hash // detached head if commit from there may be garbage collected
git checkout remote-branch // after fetch can be used to see the remote branches fetched


git revert HEAD // creates a new commit reverting the last commit
git reset commit —hard // removes the from commit and pushes head and branch back to that commit

// removes files from staging area
git reset 
git reset —mixed 

// git reset then push creates problem git will reject it  revert should be used with it
git revert HEAD commitHash // creates a new commit which has exactly same content as contents in commitHash

//want to change old commit
git checkout commitHash
git commit —amend
git rebase —continue

git reflog // to check all 
//hard
squash in one
reset handsone rebase handsone onto



git rebase —interactive other_branch // rebases current branch to other branch
git rebase —d // deletes the commit
git rebase —p // leaves commit as it is
git rebase —x // 

git reset —soft
