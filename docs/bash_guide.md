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
- (file) - determine file type
- (tree) - list contents of directories in a tree-like format
- (history) - GNU History Library

After opening the terminal to first see where you are type pwd command and hit enter. You will see something like:
~~~
[aaheikki:~$] pwd
/home/aaheikki
~~~
Here the prompt is the first thing inside square brackets \[ \]. It might also look something like <code>user_name@device_name:current_working_directory$</code>. Next comes your command pwd and on the new line the output of the pwd command. To see current directory's content type <code>ls</code> command resulting to:
~~~bash
[aaheikki:~$] ls
documents  snap  windows_aaheikki
~~~
To see further into the documents directory you enter them as argument to <code>ls</code> command:
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
[aaheikki:/$] ls /mnt/c/
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
[aaheikki:/$] cd /mnt/c/Users/aaheikki/
[aaheikki:aaheikki$]
~~~
On wsl you can also use Windows commands so to launch Windows file explorer in the current directory from command line:
~~~bash
[aaheikki:aaheikki$] explorer.exe .
~~~
Terminal might be pretty full at this point. You can clear it by pressing Ctrl+l or by typing <code>clear</code> to the command line. At this point you should be able to navigate yourself.

Let us navigate to the home directory by typing the command <code>cd</code> or <code>cd ~</code> to the command line. Then let us see all files using <code>ls -a</code> command:
~~~bash
[aaheikki:~$] ls -a
.   .bash_history  .bashrc      .cache   .gitconfig  .lesshst  .motd_shown  .ssh                       .viminfo   snap
..  .bash_logout   .bashrc.swp  .config  .landscape  .local    .profile     .sudo_as_admin_successful  documents  windows_aaheikki
~~~
Files and directories are made hidden by starting their name with dot. They are used to hide critical and configuration files that do not need manipulation, and to reduce clutter.

Using the <code>file</code> command you can identify witch type of a file is
~~~bash
[aaheikki:~$] file .bashrc
.bashrc: ASCII text
~~~
You should try this on different types of files. If you are on wsl go back to your windows user files. As shortcut you could use <code>history</code> command. You should find the cd command <code>817  cd /mnt/c/Users/aaheikki/</code> and you can copy paste it using Ctrl+Shift+C and Ctrl+Shift+V or by typing <code>!line_number_of_command</code> to execute it.

Another useful command for navigation is <code>tree</code> command. It digs deeper into the file tree and might be nicer when looking for something. Some helpful options are <code>-d</code> to show only directories and <code>-L DEPTH</code> to limit the depth it goes to. To use it with depth 3:
~~~bash
[aaheikki:~$] tree -dL 3
.
├── documents
│   └── test
├── snap
│   └── firefox
│       ├── 7836
│       ├── 7869
│       └── common
└── windows_aaheikki -> /mnt/c/Users/aaheikki/
~~~

### COMMAND --help -h
- COMMAND --help - show quick help
- man - an interface to the system reference manuals (man -k)
- (apropos) - search the manual page names and descriptions (man -k)
- (info) - read info documents

Internet is great place to look for examples and tutorials about many commands, but command line can be used to access extensive documentation. It is sometimes harder to read than others but it is good practice to try first check present documentation provided.

Most often commands have <code>--help</code> or for short <code>-h</code> options that give basic information and options how to use the commands. Let us try to see some options for <code>ls</code>:
~~~bash
ls --help
Usage: ls [OPTION]... [FILE]...
List information about the FILEs (the current directory by default).
Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

Mandatory arguments to long options are mandatory for short options too.
  -a, --all                  do not ignore entries starting with .
~~~
and so on. Here you can read about the options. You could see that <code>-h</code> is not help but stands for <code>--human-readable</code>. It is used typically with <code>-l</code> option used to get long listing. To use commands together they can be chained like so:
~~~bash
[aaheikki:~$] ls -lh
total 8.0K
drwxr-xr-x 3 aaheikki aaheikki 4.0K Feb 11 14:01 documents
drwx------ 3 aaheikki aaheikki 4.0K Feb 13 10:03 snap
lrwxrwxrwx 1 aaheikki aaheikki   22 Feb 13 09:57 windows_aaheikki -> /mnt/c/Users/aaheikki/
~~~
Long formatted option gives us more information about the files and <code>-h</code> transforms units to human readable units. Compare to plain <code>ls -l</code>.

Most commands are provided with manual page that can be accessed with <code>man</code> command. Since it is itself command let us check its manual page by <code>man man</code>:
~~~bash
man man
NAME
       man - an interface to the system reference manuals

SYNOPSIS
       man [man options] [[section] page ...] ...
       man -k [apropos options] regexp ...
       man -K [man options] [section] term ...
       man -f [whatis options] page ...
       man -l [man options] file ...
       man -w|-W [man options] page ...
~~~
To navigate up down one line use arrow keys,to up down one page space bar and *b*. For help type *h*. To search a pattern in manual page type <code>/pattern</code>. You get to the next instance by pressing *n*. To search for commands use <code>man -k pattern1 pattern2 ...</code> or <code>apropos pattern1 pattern2</code>. To see more search options check manual page of <code>man apropos</code>. Sometimes there might not be manual page, but there could be then info document that can be read with <code>info</code> command, so it is good to keep in mind. 










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