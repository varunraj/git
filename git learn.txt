
BASICS
=======

git init = > Initialize
git status => Show what is in working dir, staging 
git add <file name> => Add a file to staging
git commit -m <message> => commit a file to repo
rm -rf .git => this will remove git repo status and make a non git folder. .git is a hidden folder in the project folder which contains all tracking info.
git commit => this will open up the editor for detailed commit message.
git ls-files => show all files tracked by git
git commit -am <commit message> => express commit. Add untracked files and commit them,


Unstage:
-------
git add * -> staged file
git restore --staged <filename> => file moved back to working dir.
git restore <filename> => remove all changes done to the file in wd and revert back to repo.


View Hostory ( Better option than git log)
------------
git log --oneline --graph --decorate --all  -> History
git config --global alias.hist "log --oneline --graph --decorate --all"  => Created an alias hist

git hist => Show commit hostory in a concise way.
git hist --README.md => Show history of only README.md file.


Delete and Rename file using Git
--------------------------------
git mv example.txt demo.txt => change file name from example to demo using git
git rm demo.txt => remove demo.txt file using git.


Exclude file/folders
---------------------
.gitignore => add file here to exclude.


ADVANCED
=========

Comparing
---------
git hist -> Get history of commits
git diff <commit#> HEAD => Display all diff between latest commit and commit mentioned 
git difftool <commit#> HEAD => open up the compare tool p4merge configured to do graphical compare.

git diff => see what is changed from last commit.

Branching and Merging
---------------------
Branch is timeline of commits
Branch name are labels. Deleting a branch is deleting labels on the timelines

We build a feature on a branch and then merge to main. When possible merge is done automatically.


git branch -> show branches
git checkout -b <name of new branch> -> create a new branch 'updates' and switch
            || We can make changes to files, Then create and switch to a new branch to move all changes there.
git add . -> added changes for staging
git commit -m "branch changes' -> committed changes.
git hist -> HEAD will point to 'updates' last commit.
git difftool main updates => show diff between main and updates branch.

git checkout main -> move back to main
git hist -> show history from main Perspective. HEAD will point to main last commit.

git merge <name of branch to merge>
git merge updates -> This will merge updates branch to main.

Above merge was a ff merge

git hist => we can see HEAD, main and master all point to same last commit.

git branch -d <name of branch > -> This will delete the branch.


Types of merges:
- Fast Forward : No changes to master after branched. => Image 'ff merge'
    - Simple changes    
    - Like never branched. We wont see a seperate branch spinning out.
    - Can be disabled.

- Automatic => Image 'auto merge'
    - Non conflicting merge change detected
    - Preserve both timeline
    - Merge commit on destination. WE will see a parallal branch.

- Manual Merge => image 'manual merge'
    - Automatic merge not possible
    - conflicting merge state
    - Changes saved in merge commit.

** => When both incoming and current file have change on same line
then, we need to open up the configured merge tool and resolve conflict.

-> git merge <bad-branch>
    -> This will fail to ff or auto merge
-> git mergetool -> use the tool to keep base, incoming or current
-> once resolved, then commit the changes.




Special Markers(POinters) and Tags
-----------------------------------
    - HEAD -> Points to last commit of current branch. We can move HEAD

Tags: We can add tags to any commit Points
git tag <mytag>
git tag --list -> can see all tags
git hist -> can see the tag added to latest commit.
git tag -d mytag -> delete tag.

git tag -a v1.0 -m "Release 1.0" -> annotated tag.
git show v1.0 => show annotation also with tag.


Stashing
---------
If we want to keep current work on side and go back to previous state and do another fox

git stash - > move all current updates away to stash
make new changes, and commit
git pop -> bring back all changes that was stashed.


Time Travel
------------

git reset <commid id> --soft => least destructive. Head will be moved to the commit.
                             || this will preserve all file change in staging. 

                             || we can backout changes from here.

git reset <commid id> --mixed => Head is moved all files in wd.
git reset <commid id> --hard  => this will revert repo to the commit. WE can come back to latest commit again by moving head.


Remote Repo :
============
- get clone <remote repo> <local folder> => clone and set remote
- git push origin main => send changes to remote
- git push => by default send to origin main branch

Fetch and Pull
-------------

Make a change in remote repo. Then make changes to local and commit
If you commit now, it will be rejected with a message to 'fetch' first.


- We need to fetch the change and merge or we can pull which does both at once.

- git fetch = > bring the remote chages to local.
- git status => show the mismatch between local and remote.
- git pull or merge -> merge remote changes to local.
- git push -> send local changes to remote.

Good practice to pull remote before push if remote is shared.


GitHub Repo branches
==================== 


Pull with Rebase
----------------

It will rewind the changes from where it diverged from master. Then commit the master changes
to local branch and then add the branch changes on top of it.

- make remote changes and commit
- make local change and commit on same branch

- git fetch 
- git status -> we can see branch is diverged. and asking to pull the changes locally
- git pull --rabase - > it will rewind local changes. Then merge remote changes and then add local changes again.

graph
====

See branch graph locally.

- git log --oneline --graph


Development Branch
==================
in some worflows, we dont actively merge back to main since that represents current production. In this case
we create a dev branch and make that as default. Once it is production grade, we will merge to master.

- Create a develop branch in github. Make that as default from settings.

Tags:
====
tags are ways to create tags in branch history. Mainly done for releases.

git log --oneline -> get history of commits
git tag -a v0.1-alpha -m "Release 0.1 (Alpha)" <commid id> => Created a tag for a commit in from history.
git tag stable main -> quick tag to mark the latest commit on main brach as stable
git tag unstable develop -> quick tag to mark the latest commit on develop brach as unstable

git push origin stable - send stable tags to github.

We can see the stable tag in git release/tag section in github with an option to downnload the code at that commit point.

git push --tags = > send all tags 
git tag - f <tag name> <new commit id > -> move tags to another commit id.
git push --force origin unstable -> send the updated tag to github



