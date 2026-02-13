Objective of documentation guide is to introduce you to

- **markdown** language: used to create formatted text,
- **mkdocs**: application utilizing markdown to create a static website,
- **material-for-mkdocs**: a theme for mkdocs adding modern features to the website. 


## What is markdown?
Markdown is 

- markup language used to add formatting elements to plain text documents.
- plain text document making it portable between applications and operating systems. 
- diverse, it can be used to create notes, documentation, websites, presentations, books and emails. 
- widely used, for example Reddit, GitHub and large language models (LLM) like ChatGPT support and use markdown.


## What is mkdocs?
Mkdocs is a markdown application used for generating static websites geared towards project documentation.

## What is material-for-mkdocs?
Material-for-mkdocs is just a theme for mkdocs and it has some modern features like dark mode and better search.


## Why this combination?
Combination of markdown, mkdocs and material-for-mkdocs is a solution answering documentation problem with key characteristics

- tools are open-source so that anyone can replicate the documentation process.
- tools are simple to learn and use
- tools fit the software development workflow
- integration from other tools has small friction


## Using markdown
Basic syntax and examples can be found from [markdownguide.org/basic-syntax/](https://www.markdownguide.org/basic-syntax/). Here is demonstrated a few key syntaxes shortly:

=== "Markdown"
    ~~~markdown
    ### Text
    Here is some normal text and *Italic* and **bold**. 
    
    Paragraphs are ase separated with empty line between.

    Lines breaks are done by adding two spaces at the end of previous line or by <br>
    and smaller headings are gotten by adding more # signs.

    #### Table
    | Label 1 | Label 2  |
    |-|-|
    |Row 1  | Colum 2 |

    Table editors are helpful tool when creating more complex tables.
    
    #### Code
    Code tabs can be done enclosing the code between three ~ tilde signs or with three ` backticks signs.
    This "Markdown box is results of closing this text as code. 
    ~~~    

=== "Result"
    ### Text
    Here is some normal text and *Italic* and **bold**. 
    
    Paragraphs are ase separated with empty line between.

    Lines breaks are done by adding two spaces at the end of previous line or by <br>
    and smaller headings are gotten by adding more # signs.

    #### Table
    | Label 1 | Label 2  |
    |-|-|
    |Row 1  | Colum 2 |

    Table editors are helpful tool when creating more complex tables.

    #### Code
    Code tabs can be done enclosing the code between three ~ tilde signs or with three ` backticks signs.
    ~~~
    Here is also example of code block.
    ~~~

    ### More markdown

    Markdown has even more features like

    - Images
    - [Links](http://aaheikki.github.io/embedded_ai_lab)
    - Syntax highlights for codes
    - Emojis
    - High light
    - Sub- and superscripts


## Using mkdocs
    Again here will be just brief guide and more comprehensive guide can be found from [mkdocs.org](https://www.mkdocs.org/).
    To use mkdocs it is first installed using pip. To contain each coding environment it is good practice to create python virtual environment and activate it:

    ~~~python
    python -m venv .venv
    source .venv/bin/activate
    ~~~
    and then installing mkdocs
    ~~~python
    pip install mkdocs
    ~~~

## Using material-for-mkdocs
