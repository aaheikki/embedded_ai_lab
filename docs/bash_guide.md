## Why bash?
To make the project documentation easier to follow and to write, bash is chosen as the default shell program. Bash is readily available on UNIX systems like like different Linux distributions and MacOS. Windows users are advised to install wsl2 that allows the use of Ldinux distributions and so bash within Windows. 

### Why Linux?
Even though Linux has small market share on desktops and laptops, Linux dominates when running web servers. Linux also is relevant in embedded systems, being the choice of operating system. Like in usage of Single Mother Board Computers (SMBC) like Raspberry Pi, the Raspberry OS is a Linux based operating system itself and other Linux distributions can be used as normal operating system or to strip down the system so that it runs just the necessary software saving computation and energy. 

### Windows sub system for Linux
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

In following sections you will be shown in each section first essential commands to get started and a few useful commands placed inside brackets () to add a bit on top.

### Navigation
- pwd - print name of current/working directory
- ls - list directory contents
- cd - change the shell working directory
- (tree) - list contents of directories in a tree-like format
- (file) - determine file type

After opening the terminal to first see where you are type pwd command and hit enter. You will see something like:
~~~
[aaheikki:~$] pwd
/home/aaheikki
~~~
Here the prompt is the first thing inside square brackets \[ \]. It might also look something like user_name@device_name:current_working_directory$. Next comes your command pwd and on the new line the output of the pwd command. To see current directory's content type ls command resulting to:
~~~bash
[aaheikki:~$] ls
documents  snap  windows_aaheikki
~~~
To see further into the documents directory you enter them as argument to ls command:
~~~bash
[aaheikki:~$] ls documents/
test
~~~
If you have just installed wsl, your /home/username directory might be completely empty. Let us move to top of the file tree by using the cd command and then typing ls to see what there is:
~~~bash
[aaheikki:/$] cd /
[aaheikki:/$] ls
bin                boot  etc   init  lib.usr-is-merged  lost+found  mnt  proc  run   sbin.usr-is-merged  srv  tmp  var        wslEblNiP  wsldKLike
bin.usr-is-merged  dev   home  lib   lib64              media       opt  root  sbin  snap                sys  usr  wslBgKpLc  wslImiAle  wsldjCFle
~~~
Here we do not go into the file system hierarchy, but those who are interested the book mentioned earlier covers briefly the usage of common directories on page 20. 

But let us go and find our files we have on Windows. Those are located in mnt/ directory which will also contain other storage devices mounted manually. Before using cd let us check the content with ls:

~~~bash
[aaheikki:/$] ls mnt/
c  wsl  wslg
~~~
Here c is my local disk. You might have different name or multiple storage devices. Let us see what is inside:

~~~bash
[aaheikki:/$] ls mnt/c/
ls: cannot access 'mnt/c/DumpStack.log.tmp': Permission denied
ls: cannot access 'mnt/c/hiberfil.sys': Permission denied
ls: cannot access 'mnt/c/pagefile.sys': Permission denied
ls: cannot access 'mnt/c/swapfile.sys': Permission denied
'$Recycle.Bin'                    'Documents and Settings'   PerfLogs               Recovery                     Windows        swapfile.sys
'$WINRE_BACKUP_PARTITION.MARKER'   DumpStack.log            'Program Files'        'System Volume Information'   hiberfil.sys   uef
 Config.Msi                        DumpStack.log.tmp        'Program Files (x86)'   Teams.txt                    inetpub
 Dell                              Intel                     ProgramData            Users                        pagefile.sys
 ~~~
There are some files that have limited access but we can see familiar file names like 'Program Files', 'Program Files (x86)', Users and Windows. Next you should locate your username and files inside the Users directory. Use ls to see what users there are and cd to navigate to your user files
~~~bash
[aaheikki:/$] cd mnt/c/Users/aaheikki/
[aaheikki:aaheikki$]
~~~
On wsl you can also use Windows commands so to launch Windows file explorer in the current directory from command line:
~~~bash
[aaheikki:aaheikki$] explorer.exe .
~~~


### COMMAND --help -h
- COMMAND --help - show quick help
- man - an interface to the system reference manuals (man -k)
- (apropos)  - search the manual page names and descriptions 
- (info) - read info documents

### Read files
- less - opposite of more
- (more) - display the contents of a file in a terminal
- (cat) - concatenate files and print on the standard output
- (grep)  - print lines that match pattern
- (|) - pipe the standard output of command to standard input of next command
- (>) - rewrite file
- (>>) - append to file

### Manipulating files and directories
- mkdir - make directories 
- mv - move (rename) files
- cp - copy files and directories
- rm - remove files or directories
- chmod change access permissions ( chmod a +-rwx)
- (ln) - make links between files -s symbolic not hard link


#### Text editors
- nano - Nano's ANOther editor, inspired by Pico
- (vim) - Vi IMproved, a programmer's text editor

#### (Zip)
- (zip) - package and compress (archive) files
- (unzip) - list, test and extract compressed files in a ZIP archive

### Package management
- apt - provides a high-level commandline interface for the package management system.
- (snap) - install, configure, refresh and remove snaps. Snaps are packages that work across many different Linux distributions.