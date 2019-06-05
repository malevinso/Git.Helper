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


### Update the Local Repo


### Update the Fork






