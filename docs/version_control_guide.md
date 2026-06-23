## What is Git

Git is a distributed version control system used to track changes in files over time.

- Open-source
- Fast and efficient
- Distributed: every clone contains the full history of the project.
- Branching: enabling parallel work and experimentation

Objective of this guide is to give users simple workflow using git and small introduction to some of its capabilities that are useful in larger and collaboration work. Git has its own comprehensive documentation and guide book [git-scm.com/book/en/v2](https://git-scm.com/book/en/v2)
which should be consulted.

Git comes with build-in GUI tool but also has many third party GUI tools. Also vscode provides basic git functions, but git on command line is same for all environments and has all the available commands so using git on command line is advised, but not necessary.

## Installing git
Follow installation instructions at [https://git-scm.com/install](https://git-scm.com/install).
For quick install on command line for debian based linux

~~~bash
apt install git
~~~

## Running git locally 
To use git you navigate to an already existing project folder or a new one you want to track. The project folder could look something like this:

~~~bash
example_project_directory/
├── docs/
├── README.md
├── requirements.txt
├── sub_project_1/
├── sub_project_2/
└── .venv/
~~~

Initialize git with the following command:
~~~bash
git init
~~~
This creates and configs .git to track your folder's changes. Next add all files using point sign or individual files to be tracked:
~~~bash
git add .
~~~
Make the first commit:
~~~bash
git commit -m 'initial commit'
~~~
Commits create a snapshot of the files you can return to and branch from. It is good practice to make commits between each completed functioning part of code and describing the change made. After each commit the files you want to add to next commit need to be added again. You can check which files have changes and which ones have been added to next commit: 
~~~bash
git status
~~~

### Local gitflow
Once previous loop is completed it is repeated.
~~~ mermaid
graph LR
  A[Git initialization] --> B{Develop};
  B --> C[Completed functioning part];
  C --> D[git add .];
  D --> E[git commit -m 'description']
  E --> B;
~~~

To see previous commits and their ids to reset or to branch from use command
~~~bash
git log
~~~


## What is GitHub
GitHub is a hosting service for Git repositories. It adds some collaboration features on top of git:

- Remote storage for Git repositories
- Sharing code with others
- Pull requests for reviewing and merging changes
- Issue tracking and project discussions
- Access control and visibility (public / private)

For those who want to self host repositories Gitea is one open-source option to look into.

### Creating GitHub account and adding SSH Key
Before making a new repository you need to create GitHub account on
[github.com](https://github.com/).

After logging in add a ssh public key to access your repositories through your GitHub account. If you do not have generated ssh keys use the command line to create a private and public key pair to ~/.ssh/id_ed25519 and ~/.ssh/id_ed25519.pub by typing <code>ssh-keygen</code>. Do not specify a file to save the keys to.

On GitHub navigate to:
~~~ mermaid
graph LR
A[Settings] --> B[SSH and GPG keys];
B --> C[New SSH Key];
C --> D(Add title describing your device and your public key from id_ed25519.pub);
D --> E[Add SSH Key]
~~~

### New repository
On GitHub create a new repository. Do not add readme file. Then on the command line using your username and repository names
~~~bash 
git remote add origin git@github.com:username/repo_name.git
~~~
adding your repository and naming it as origin. 

At this point it might be useful to to add a .gitignore file defining files you do not want or need to be tracked. For example pythons virtual environment folder .venv/ which uses your local paths and would not work for others.

~~~bash
echo '.venv' >> .gitignore
~~~

Then push your local folder to the repository and set it as upstream so that git tracks changes done to the repository.

~~~bash
git push -u origin master
~~~

### Cloning repository

If you want to clone an existing repository. On the command line use following command to fetch the repository setting it automatically as the upstream repository.
~~~bash 
git clone git@github.com:username/repo_name.git
~~~
If you are the owner or have writing rights you can start pushing and pulling. 

### Remote gitflow

When working with repositories the same local gitflow applies, but you will have to first pull changes from the repository and at the end of a session push your changes to the repository for your local files to be up to date and to share your local work.
~~~ mermaid
graph LR
Z[Start of session] --> A[git pull]
A --> B[local gitflow];
B --> D[git add; git commit];
D --> B;
B --> C[git push];
C --> E[End of session];
~~~
Further you could have stable master / main branch from which you have branched a development branch that you and possibly others are working on by then branching from and merging. 

## Branching and Merging
Next is a diagram showing a possible scenario with branches master, develop, feature and hot fix. 
~~~ mermaid
gitGraph
    commit id: "initial"

    branch develop
    checkout develop
    commit id: "setup dev"

    branch feature
    checkout feature
    commit id: "simple change"
    checkout develop
    merge feature id: "merge feature"

    checkout main
    branch hot_fix
    checkout hot_fix
    commit id: "hotfix"
    checkout main
    merge hot_fix id: "merge hotfix"

    checkout develop
    merge main id: "updating develop branch"

    checkout feature
    commit id: "feature progress"
    commit id: "feature complete"
    checkout develop
    merge feature id: "merge feature progress"
    
    checkout main
    merge develop id: "release"
~~~

You and other developers would be working mostly on the develop branch by making individual feature branches and merging them back once finished. In critical cases where a hotfix is needed one could also branch from master and make the necessary changes. Afterwards master could be merged with develop branch to get it up to date or merge develop into master working as new release.

You can branch from the current commit and change to it:
~~~bash
git branch name_new_branch
git checkout name_new_branch
~~~
You would apply your normal gitflow and once ready with changes merge back:
~~~bash
git merge
~~~
Git will merge things automatically in cases when there is no room for guessing between conflicted changes. In situations in which changes are made to same files in different branches git notifies you of files that have conflicts and modifies them to identify which part is from which branch. You would then make changes to the files the way you see best, add them to the next commit and make the commit finishing the merge.

Let's go through a simple example of conflict in merge. We will add a text file in master, branch twice from it and append line to the text file. Then merge the first branch which does not have conflicts and then merge the second branch that will have a conflict with the first branch. Next is a diagram visualizing the example.
~~~ mermaid
gitGraph
    commit id: "initial .txt file"

    branch branch_1
    branch branch_2
    checkout branch_1
    commit id: "append to .txt file first time"

    checkout branch_2
    commit id: "append to .txt file second time"

    checkout main
    merge branch_1 id: "merge 1st branch"
    merge branch_2 id: "merge 2nd branch"
    commit id: "resolving conflicts - finishing the merge"
~~~

Moving on to the command line. In the master branch creating .txt file with some initial text
~~~bash
echo "initial line" > merge_test.txt
git add .
git commit -m 'initial .txt file'
~~~
create two branches, move to them and append new lines to .txt file
~~~bash
git branch branch_1
git branch branch_2
git checkout branch_1
echo "line branch_1" >> merge_test.txt
git add .
git commit -m 'line branch_1'
git checkout branch_2
echo "line branch_2" >> merge_test.txt
git add .
git commit -m 'line branch_2'
~~~
To merge branches move to the master branch and merge
~~~bash
git checkout master
git merge branch_1
~~~
Here there are no conflicts and the merge is done automatically, but in the next one you are requested to resolve the conflicts
~~~bash
git merge branch_2
~~~                 
You get the conflict message:
~~~
Auto-merging merge_test.txt
CONFLICT (add/add): Merge conflict in merge_test.txt
Automatic merge failed; fix conflicts and then commit the result.
~~~
The message already tells us that the conflicts are in merge_test.txt file and to fix the conflicts and to commit the results. The same can also be seen using the git status command. Moving on with the merge, opening the merge_test.txt file we see that git has modified the file to pinpoint the conflicts:
~~~
initial line
<<<<<< HEAD
line branch_1
======
line branch_2
>>>>>> branch_2
~~~
Next step is not just to chose which change to keep, but to **freely modify** the merge_test.txt file to desired state. Like removing both lines and adding completely another one:
~~~
initial line
resolved conflict line
~~~
Then add, commit, and move to the next possible conflict if non merge is completed.
~~~bash
gid add .
git commit -m 'resolved merge_.txt conflict'
~~~

### Reset
If there issues arise in the merge process and there comes a need to abort then:
~~~bash
git merge --abort
~~~
In more general needs for resets and reverts look into git revert, reset and branching from previous commits to see which one suites your scenario.