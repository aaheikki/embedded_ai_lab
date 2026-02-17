## Introduction to markdown and mkdocs
Objective of documentation guide is to introduce you to

- **markdown** language: used to create formatted text,
- **mkdocs**: application utilizing markdown to create a static website,
- **material-for-mkdocs**: a theme for mkdocs adding modern features to the website. 


### What is markdown?
Markdown is 

- markup language used to add formatting elements to plain text documents.
- plain text document making it portable between applications and operating systems. 
- diverse, it can be used to create notes, documentation, websites, presentations, books and emails. 
- widely used, for example Reddit, GitHub and large language models (LLM) like ChatGPT support and use markdown.


### What is mkdocs?
Mkdocs is a markdown application used for generating static websites geared towards project documentation.

### What is material-for-mkdocs?
Material-for-mkdocs is just a theme for mkdocs and it has some modern features like dark mode and better search.


### Why this combination?
Combination of markdown, mkdocs and material-for-mkdocs is a solution answering documentation problem with key characteristics

- tools are open-source so that anyone can replicate the documentation process.
- tools are simple to learn and use
- tools fit the software development workflow
- integration from other tools has small friction

## Getting started
Tutorial on youtube :material-youtube: [Material for MkDocs: Full Tutorial To Build And Deploy Your Docs Portal](https://www.youtube.com/watch?v=xlABhbnNrfI) by James Willet (27 min) covers the basic usage of markdown, mkdocs and material-for-mkdocs and is highly recommended to get started quickly. In following sections you will be shown minimal syntax to get things running in a short amount of time.


### Using markdown
Basic syntax and examples can be found from [markdownguide.org/basic-syntax/](https://www.markdownguide.org/basic-syntax/). Here are demonstrated a few key syntaxes shortly:

=== "Markdown"
    ~~~markdown
    #### Text
    Here is some normal text, *Italic* and **bold**. 
    
    Paragraphs are ase separated with empty line between.

    Lines breaks are done by adding two spaces at the end of previous line or by <br>
    and subsections are done by adding more # signs.

    ##### Table
    | Label 1 | Label 2  |
    |-|-|
    |Row 1  | Colum 2 |

    Table editors are helpful tool when creating more complex tables.
    
    ##### Code
    Code tabs can be done enclosing the code between three ~ tilde signs or with three ` backticks signs.
    This "Markdown box is results of closing this text as code. 
    ~~~    

=== "Result"
    #### Text
    Here is some normal text, *Italic* and **bold**. 
    
    Paragraphs are ase separated with empty line between.

    Lines breaks are done by adding two spaces at the end of previous line or by <br>
    and subsections are done by adding more # signs.

    ##### Table
    | Label 1 | Label 2  |
    |-|-|
    |Row 1  | Colum 2 |

    Table editors are helpful tool when creating more complex tables.

    ##### Code
    Code tabs can be done enclosing the code between three ~ tilde signs or with three ` backticks signs.
    ~~~
    Here is also example of code block.
    ~~~

    #### More markdown

    Markdown has even more features like

    - Images
    - Links
    - Syntax highlights for codes
    - Emojis
    - High light
    - Sub- and superscripts


### Using mkdocs
Documentation for mkdocs can be found from [mkdocs.org](https://www.mkdocs.org/).
To use mkdocs it is first installed using pip. To contain each coding environment it is good practice to create python virtual environment and activate it:

~~~python
python -m venv .venv
source .venv/bin/activate
~~~
and then installing mkdocs
~~~python
pip install mkdocs
~~~

To create a mkdocs project into your current directory, type on command line
~~~bash
mkdocs new .
~~~
This creates mkdocs.yml configuration file and docs/ directory containing index.md file. Only requirement for configuration file is to have site name by default 'site_name: My Docs'. To get multiple pages you just create more markdown files in docs folder and you can organize them in the docs/ directory inside other directories and mkdocs uses that for navigation bar, or you can specify the navigation in the configuration file. 

To review your site 
~~~bash
mkdocs serve
~~~
opens local server hosting the site at http://127.0.0.1:8000/ which you can access trough your browser. It should watch changes done to your files and update it but if not then you can just stop the server on command line by pressing Ctrl+C and launching it again. 

To build a site type on the command line
~~~bash
mkdocs build
~~~
and it creates site/ directory containing the site which you can then host.

This is a simple solution to get your documentation in markdown as static website. Further you can make pdf files if desired.

### Using material-for-mkdocs
Material-for-mkdocs is a theme built on top of mkdocs. It adds modern touch with better search, dark mode, diagrams and more. Complete documentation can be seen :simple-materialformkdocs: [mkdocs-material](https://squidfunk.github.io/mkdocs-material/) which works also as comparison with just [mkdocs.org](https://www.mkdocs.org/) documentation site.

To get started here is simplest syntax to get material theme working by modifying the mkdocs.yml file to:
~~~
site_name: My Docs
theme:
  name: material
~~~
Now your site uses the material theme. Further as an example is how to use the dark mode. Other wise consult the :simple-materialformkdocs: [mkdocs-material](https://squidfunk.github.io/mkdocs-material/) documentation.

#### Dark mode

To use dark mode modify mkdocs.yml to:
~~~
site_name: My Docs
theme:
  name: material
  palette:
      # Dark mode
    - scheme: slate
      primary: teal
      accent: green
~~~
Here are also primary and accent colors changed, but that is not necessary. Comments in .yml file are done using # sign. To view the color palette or how to use custom colors visit the material's :simple-materialformkdocs: [changing-the-colors](https://squidfunk.github.io/mkdocs-material/setup/changing-the-colors/#configuration) section.

To add toggle between light and dark mode:
~~~
site_name: My Docs
theme:
  name: material
  palette:
      # Dark mode
    - scheme: slate
      primary: teal
      accent: green
      toggle:
        icon: material/brightness-4
        name: Switch to light mode

      # Light mode
    - scheme: default
      primary: light green
      accent: lime
      toggle:
        icon: material/brightness-7
        name: Switch to dark mode
~~~

