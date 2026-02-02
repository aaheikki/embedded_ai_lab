### What is Git

Git is a distributed version control system used to track changes in files over time.

- Open-source
- Fast and efficient
- Distributed: every clone contains the full history of the project.
- Branching: enabling parallel work and experimentation


### Installing git
Install instructions can be found from
<a href="https://git-scm.com/install" target="_blank" rel="noopener">
https://git-scm.com/install
</a>. For quick install on command line for debian based linux and windows powershell

=== "Bash (Linux)"
    ~~~bash
    apt install git
    ~~~

=== "PowerShell (Windows)"
    ~~~powershell
    winget install --id Git.Git -e --source winget
    winget list git
    y
    exit
    ~~~

### Running git locally 
To use git you navigate to already existing project folder or a new one you want to track. Project folder could look something like this:

~~~bash
example_project_directory/
├── docs/
├── README.md
├── requirements.txt
├── sub_project_1/
├── sub_project_2/
└── .venv/
~~~

Initialize git with following command:
~~~bash
git init
~~~
This creates and configs .git to track your folders changes. Next add all files using point sign or individual files to be tracked:
~~~bash
git add .
~~~
Make first commit:
~~~bash
git commit -m 'initial commit'
~~~
Both commands can be combined by adding another option to commit:
~~~bash
git commit -am 'initial commit'
~~~
Commits create a snapshot of the files you can return to and branch from. It is good practice to make commits between each completed functioning part of code and describing the change made. After each commit the files you want to add to next commit need to be added again. You can check which files have changes and which ones have been added to next commit: 
~~~bash
git status
~~~

#### Local gitflow
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


### What is GitHub
GitHub is a hosting service for Git repositories. It adds collaboration features on top of git:

- Remote storage for Git repositories
- Sharing code with others
- Pull requests for reviewing and merging changes
- Issue tracking and project discussions
- Access control and visibility (public / private)

For those who want to self host repositories Gitea is one open-source option. 

#### Creating GitHub account and adding SSH Key
Before making a new repository you need to create GitHub account at 
<a href="https:github.com/" target="_blank" rel="noopener">
https:github.com/
</a>.

After logging add ssh public key to access your repositories through your GitHub account. If you do not have generated ssh keys use following command to create private and public key pair to ~/.ssh/id_ed25519 and ~/.ssh/id_ed25519.pub:
~~~bash
ssh-keygen
~~~
On GitHub navigate to:
~~~mermaid
graph LR
A[Settings] --> B[SSH and GPG keys];
B --> C[New SSH Key];
C --> D(Add title describing your device and your public key from id_ed25519.pub);
D --> E[Add SSH Key]
~~~

#### New repository
On GitHub create new repository. Do not add readme file. Then on command line
~~~bash 
git remote add origin git@github.com:username/repo_name.git
~~~
adding your repository and naming it as origin. 

At this point it might be useful to to add .gitignore file defining files you do not want or need to be tracked. For example pythons virtual environment folder .venv/ which uses your local paths and would not work for others.

~~~bash
echo '.venv' >> .gitignore
~~~

Then push your local folder to repository and set it as upstream so that git tracks changes done to the repository.

~~~bash
git push -u origin master
~~~

#### Cloning repository

If you want to clone existing repository. On command line use following command to fetch repository setting it automatically as upstream repository.
~~~bash 
git clone git@github.com:username/repo_name.git
~~~
If you are owner or have writing rights you can start pushing and pulling. 

#### Remote gitflow

When working with repositories same local gitflow is down, but you will have to first pull changes from repository and at the end of session push your changes to the repository.
~~~mermaid
graph LR
Z[Start of session] --> A[git pull]
A --> B[local gitflow];
B --> D[git add; git commit];
D --> B;
B --> C[git push];
C --> E[End of session];
~~~
