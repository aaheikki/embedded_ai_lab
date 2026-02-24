## Why bash?
To make the project documentation easier to follow and to write, bash is chosen as the default shell program. Bash is readily available on UNIX systems like like different Linux distributions and MacOS. Windows users are advised to install wsl2 that allows the use of linux distributions and so bash within Windows. 

### Why Linux?
Even though Linux has small market share on desktops and laptops, Linux dominates when running web servers. Linux also is relevant in embedded systems, being the choice of operating system. Like in usage of Single Mother Board Computers (SMBC) like Raspberry Pi, the Raspberry OS is a Linux based operating system itself and other Linux distributions can be used as normal operating system or to strip down the system so that it runs just the necessary software saving computation and energy. 

### Windows sub system for linux
On windows To install wsl and ubuntu using the powerShell(needs admin rights):
~~~powerShell
wsl --install 
~~~
Ubuntu is supposed to be installed as default but to check that ubuntu is installed type on the command line:
~~~powerShell
wsl --list
~~~
If you can't see ubuntu then install it with:
~~~powerShell
wsl.exe --install ubuntu
~~~
reboot is necessary.

After reboot launch ubuntu in powerShell by:
~~~powerShell
wsl.exe --distribution ubuntu
~~~
or from windows menu.

You can see the list of other available distributions and try them also out with:
~~~powerShell
wsl.exe --list --online
~~~

## Using bash
*The Linux command line* by William shots is a great introduction book. It is meant as an exercise book so that you would be reading the book and trying the examples out yourself. It starts from zero and gradually increases the tools and nuances using the tools to also show the cool and powerful stuff that is enabled by command line usage. The book can be downloaded freely from [https://linuxcommand.org/tlcl.php](https://linuxcommand.org/tlcl.php) as pdf file. The website also provides more compact introduction to the command line on Linux.
In following sections you will be shown a few basic commands to get started on navigating directories and manipulating the files.

- pwd - print name of current/working directory
- ls - list directory contents
- cd - change the shell working directory
- cat - concatenate files and print on the standard output
- more - display the contents of a file in a terminal
- less - opposite of more
- man - an interface to the system reference manuals
- mv - move (rename) files
- cp - copy files and directories
- rm - remove files or directories
- chmod change access permissions ( chmod a +-rwx)
- grep  - print lines that match pattern
- zip - package and compress (archive) files
- unzip - list, test and extract compressed files in a ZIP archive
- vim - Vi IMproved, a programmer's text editor
- nano - Nano's ANOther editor, inspired by Pico
