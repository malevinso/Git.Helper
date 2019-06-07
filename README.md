# Git.Helper
Just a simple Site to help me remember stuff

## Typical Workflow

The typical workflow is:

* Fork the main Repo
* Make changes to the Fork
* Create Pull request to merge changes back to main

For this exmample, I will use 2 GitHub Oranizations:

1. mark-demo-org
2. malevinso

I will use malevinso as the "Master" org where the final code  repo will be maintained. I will use mark-demo-org as the "working" org where I will for the main repos from malevinso.

### Connect Github to local 

1. Fork Repo you want to work on 
    * Go to Repo you want to fork (malevinso/Git.Helper)
    * Select the Fork Icon in the upper right
    * Select the organization you want to put the fork (marks-demo-org)
2. Clone the fork to your local Repo
    * ````git clone https://github.com/mark-demo-org/Git.Helper.git```` 
    e.g., for this repo
3. Add the upstream repo:
    * ````git remote add upstream https://github.com/malevinso/Git.Helper.git````
    * Run this command: 
        ````git remote -v```` you sould see:
        ````yaml
        origin  https://github.com/marks-demo-org/Git.Helper.git (fetch)
        origin  https://github.com/marks-demo-org/Git.Helper.git (push)
        upstream https://github.com/malevinso/Git.Helper.git (fetch)
        upstream https://github.com/malevinso/Git.Helper.git (push)
        ````

### Start making some changes

1. We have a file called "README.md" from the orignal repo. Before we make any changes we can run git status to show nothing has changed:
    ````
    λ git status
    On branch master
    nothing to commit, working tree clean
    ````
2. First thing we should do is create a new branch (this makes it much easier to merge the original repo back into local master branch)
    ````
    λ git checkout -b working-branch
    Switched to a new branch 'working-branch'
    ````
    We are now working on a new branch in this case called 'working-branch'


3. Now I will make some changes to the file and you can see:
    ````
    λ git status
    On branch working-branch
    Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)

            modified:   README.md

    no changes added to commit (use "git add" and/or "git commit -a")

    ````
    Notice we have 1 modiied file.

### Push changes back to Fork
1. First we can add the files to prepare a commit
    ````
    λ git add -A

    λ git status
    On branch working-branch
    Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)

        modified:   README.md

    ````
2. Now you can create a commit
    ````
    λ git commit -m "Commit README"
    [working-branch e5597a2] Commit README
    1 file changed, 93 insertions(+), 2 deletions(-)
    rewrite README.md (71%)
    ````
    >Notice the working branch and the SHA(unique id of the commit)

3. Finally we can push them back to the Forked Repo (Keeping the working-branch)
    ````
    λ git push origin working-branch
    Enumerating objects: 8, done.
    Counting objects: 100% (8/8), done.
    Delta compression using up to 6 threads
    Compressing objects: 100% (4/4), done.
    Writing objects: 100% (6/6), 1.67 KiB | 853.00 KiB/s, done.
    Total 6 (delta 1), reused 0 (delta 0)
    remote: Resolving deltas: 100% (1/1), done.
    remote:
    remote: Create a pull request for 'working-branch' on GitHub by visiting:
    remote:      https://github.com/marks-demo-org/Git.Helper/pull/new/working-branch
    remote:
    To https://github.com/marks-demo-org/Git.Helper.git
    * [new branch]      working-branch -> working-branch
    ````


### Create a Pull Request to Request Update to Main Repo

Very simple, just go to the upstream rep that you want to merge into and click New Pull Request

1. make sure you have the correct branch    malevinso/GitHelper (Master) <- marks-demo-org/GitHelper(working-branch)
2. Merge the PR

now we have on the master branch: 
````
commit a46dc0b23bb2f3ecd4036e432ea01004a12991d8 (HEAD -> master, upstream/master, origin/master, origin/HEAD)
Merge: 5d147c4 7063407
Author: malevinso <malevinso@gmail.com>
Date:   Fri Jun 7 11:05:10 2019 -0600

    Merge pull request #1 from marks-demo-org/working-branch

    Commit README

commit 70634070c6af2ffb08c6c48f12d3825e4a273f68
Author: Mark Levinson <malevinso@gmail.com>
Date:   Wed Jun 5 15:28:58 2019 -0600

    Commit README

commit 5d147c471dc7ba128576caa8bdd6ea5e718a4c17
Author: malevinso <malevinso@gmail.com>
Date:   Wed Jun 5 14:37:33 2019 -0600

    Initial commit
````


### Delete the working-branch

git branch -d working-branch
git push origin --delete working-branch


### Update the Local Repo

from the master branch 
git pull upstream


### Update the Fork

from the master branch

git push upstream  

## What if the PR fails? 
E.g., Can't Merge Automatically

>This is where it gets tricky.
    This can  happen when the master branch on the base Repo got updated out from under you. Now we have to "rebase" our changes on top of those new changes and update our PR. 

### Create new use case for this:

  For this use case I created 2 branches:
  1. first-change
  2. second-change

  I will make a change to the README on the first-change and create a PR.

  However, prior to merging the pull request, I will another change, similar to the first on the second-change branch. Create a PR, and merge it.

  Now the first-change PR will probably give us a "Can't automatically merge" error.  

  -- Working on the use case now -- SECOND CHANGE and FIRST CHANGE 

