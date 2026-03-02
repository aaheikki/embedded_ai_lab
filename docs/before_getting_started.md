## Command Line

- The command line is the primary interface for development tools like version control and ssh connection.
- It is not desirable to allocate resources for GUI in embedded systems.
- **Bash** is chosen as the default shell program because:
    - It is on default on most UNIX systems like Linux and MacOS.
    - It is also available for Windows user by installing wsl.
    - Documentation is easier to follow and write for all.

If you are not familiar with any command line then follow [bash guide](bash_guide.md).

## Version Control

- **Version control** is the practice of tracking and managing changes in files and software projects.
    - Tracking changes lets you revert to earlier working states if new bugs or issues appear during development.
- **Branching and merging** allow developers to work independently without interfering with each other.
    - Team members can develop features, test ideas, or prototype solutions in isolated branches.
    - When the work is stable, it can be merged cleanly into the main branch.
    - Even for individuals, branching avoids creating multiple copies of project folders and manually tracking them.
- **Git** is widely used version control system.

If you are not familiar with version control follow [version control guide](version_control_guide.md).

## Code Documentation

- **Inline comments** explain specific parts of the code.
    - **Structure:** Writing code with clear structure and meaningful comments makes it easier to navigate and debug.
    - **Reasoning:** Documenting non-obvious design choices prevents repeating old mistakes and helps future contributors understand why something was done in a certain way.

- **Project / User documentation** outside the codebase acts as a guide and reference for users and developers much like table of content.
    - **Building on top:** Clear documentation makes it easy to understand what already exists, so new features do not reinvent previous work.
    - **Collaboration:** New collaborators can become productive quickly while maintaining consistency across the project.
    - **User adoption:** People are more likely to use and contribute to systems that are understandable and well explained.
    - **Markdown and mkdocs:** Markup language and application fore generating documentation sites.

If you are interested in markdown and mkdocs follow [documentation guide](documentation_guide.md).
