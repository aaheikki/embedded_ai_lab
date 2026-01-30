
### What is Git and GitHub


Git is most used version control and we will be implementing git as version control tool and GitHub as our upstream repository. 

### Installing Git
Install instructions can be found from their web site
<a href="https://git-scm.com/install" target="_blank" rel="noopener">
https://git-scm.com/install
</a> or quick install for debian based linux and windows powershell

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
|── sub_project_2/
└── .venv/
~~~

Initialize git with following command:
~~~bash
git init
~~~
Add all files to be tracked:
~~~bash
git add .
~~~
Make first commit:
~~~bash
git commit -m 'initial commit'
~~~
Commits work as timestamps you can return to in case of over the head bugs. It is good practice to make commits between each completed functioning part of code and describing the change made. After each commit the files you want to add to next commit need to be added again. You can check which files have changes and which ones have been added to next commit: 
~~~bash
git status
~~~
### Gitflow




### Uploading local git folder to new repository
Initialize git with following command:
~~~bash
git init
~~~

At this point it might be useful to to add .gitignore file defining files you do not want or need to be tracked. For example pythons virtual environment folder .venv/ which contains your local paths and would not work for others.

~~~bash
echo '.venv' >> .gitignore
~~~


=== "Bash (Linux / macOS)"

    ~~~bash
    git clone https://github.com/example/repo.git
    cd repo
    ~~~

=== "PowerShell (Windows)"
    
    ~~~powershell 
    git clone https://github.com/example/repo.git
    cd repo
    ~~~
