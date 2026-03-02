## Why bash?
To make the project documentation easier to follow and to write, bash is chosen as the default shell program. Bash is readily available on UNIX systems like like different Linux distributions and MacOS. Windows users are advised to install wsl2 that allows the use of Linux distributions and so bash within Windows. 

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
- (find) - search for files in a directory hierarchy
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
There are some files that have limited access but we can see familiar file names like 'Program Files', 'Program Files (x86)', Users and Windows. Next you should locate your username and files inside the Users directory. Use ls to see what users there are and cd to navigate to your user files. As a tip you can use *Tab* to auto complete your arguments if there are no other options available. For example trying to type <code>ls /mnt/c/'Docume</code> and tab you should get <code>ls /mnt/c/'Documents and Settings'</code>
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

Another useful command for navigation is <code>tree</code> command. It digs deeper into the file tree and might be nicer when looking for something. If it is not installed you can install it with <code>sudo apt install tree</code>. Some helpful options are <code>-d</code> to show only directories and <code>-L DEPTH</code> to limit the depth it goes to. To use it with depth 3:
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

With these you should have some tools to find commands and help, but keep in mind it is many times easier to see from internet how others have done it first and then afterwards it is faster to check manual and help pages to see what were the options and argument orders.



### Read files
- cat - concatenate files and print on the standard output
- less - opposite of more
- (tail) - output the last part of files
- (head) - output the first part of files
- (grep) - print lines that match pattern
- (|) - pipe the standard output of command to standard input of next command


To plainly print content of a file to terminal <code>cat</code> command is used. It just plainly spits out all of the files content to terminal so bigger files are not practical to read with it. For reading those <code>less</code> is recommended it has similar navigation as man page so to quit press *q*. If you check the manual page or help you will see reference to <code>more</code> command which is kind of between cat and less. It displays the content on the terminal, but one page at the time. Also check <code>tail</code> and <code>head</code> commands.

The <code>grep</code> command is used to find patterns in a file. It can also be used with pipe (|) to take as input another commands output. You are recommended to test <code>grep</code> and even test piping something into it like:
~~~bash
[aaheikki:~$] history | grep mnt
   35  cd /mnt
  116  cd /mnt
  128  ln -s /mnt/c/Users/aaheikki/ ~/windows_aaheikki
~~~
This gives you history lines with "mnt". 


### Manipulating directories and files
- mkdir - make directories 
- mv - move (rename) files
- cp - copy files and directories
- rm - remove files or directories
- (ln) - make links between files -s symbolic not hard link
- nano - Nano's ANOther editor, inspired by Pico
- (vim) - Vi IMproved, a programmer's text editor
- (echo) - display a line of text
- (>) - rewrite file
- (>>) - append to file
- sudo - allows a permitted user to execute a command as the superuser or another user.
- chmod - change access permissions



Let us return to the home with <code>cd ~</code>, make a new directory and go to it:
~~~bash
[aaheikki:~$] mkdir playground
[aaheikki:~$] cd playground
[aaheikki:playground$]
~~~
Lets make more directories
~~~bash
[aaheikki:playground$] mkdir dir1 dir2 dir3
[aaheikki:playground$] ls
dir1  dir2  dir3
~~~
Move directories dir2 and dir3 to dir1
~~~bash
[aaheikki:playground$] mv dir2 dir3 dir1
[aaheikki:playground$] ls
dir1
[aaheikki:playground$] ls dir1/
dir2  dir3
~~~
Make dir 4 and copy it to dir3
~~~bash
[aaheikki:playground$] mkdir dir4
[aaheikki:playground$] cp dir4 dir1/dir3/
cp: -r not specified; omitting directory 'dir4'
[aaheikki:playground$] cp -r dir4 dir1/dir3/
[aaheikki:playground$] tree
.
├── dir1
│   ├── dir2
│   └── dir3
│       └── dir4
└── dir4
~~~
Note that option <code>-r</code> was needed. Check what it says in help. Then let us cp dir1 to dir4
~~~bash
[aaheikki:playground$] cp -r dir1/ dir4/
[aaheikki:playground$] tree
.
├── dir1
│   ├── dir2
│   └── dir3
│       └── dir4
└── dir4
    └── dir1
        ├── dir2
        └── dir3
            └── dir4
~~~
Then let us finish by removing them.
~~~bash
[aaheikki:playground$] rm -r dir1 dir4
[aaheikki:playground$] tree
.

0 directories, 0 files
~~~
It is to be noted that you should be careful with the remove <code>rm</code>. There are no backups by default and Linux assumes you know what you are doing. So do check the options and make sure to test how it works before deleting anything of importance. 

To access your windows files more easily you could do a soft link pointing to you user files:

~~~bash  
[aaheikki:~$] ln -s /mnt/c/Users/aaheikki/ ~/windows_aaheikki
documents  playground  snap  windows_aaheikki
[aaheikki:~$] ls -l ~/
total 12
drwxr-xr-x 3 aaheikki aaheikki 4096 Feb 11 14:01 documents
drwxr-xr-x 2 aaheikki aaheikki 4096 Feb 26 13:23 playground
drwx------ 3 aaheikki aaheikki 4096 Feb 13 10:03 snap
lrwxrwxrwx 1 aaheikki aaheikki   22 Feb 13 09:57 windows_aaheikki -> /mnt/c/Users/aaheikki/
~~~
That created soft link named <code>windows_aaheikki</code> that pointing to <code>/mnt/c/Users/aaheikki/ directory</code>. Soft links cab be made to point to files also. So soft link is kind of another door to what ever it is pointing at.



#### Editing file content
Text editors are used to edit text! Nano is more beginner friendly resembling Windows text editor. Vim is a bit trickier but has powerful tools and is by default on installed many Linux distributions so it good idea to check introduction to vim. The Linux Command Line book covers vim on page 150. They are used by typing the command and the file you want to edit or create <code>nano text</code>. Type something and then to exit press Ctrl+X, it asks you to save or abort changes, press y to save and then Enter to exit. To copy paste so said normally you need to use Ctrl+Shift+C and Ctrl+Shift+V inside the terminals. Terminals also have their own short keys to cut, paste go to lines. Do see these from online guides or using manual or help pages.

Display on command line what you wrote:
~~~bash
[aaheikki:playground$] cat text
line 1
~~~
Make another file with <code>echo "line 2" > text2<code>. The <code>echo</code> command prints your string on the terminal and <code>></code> writes it into a file. If there exist file with the same name this overwrites it. To append text to file use <code>>></code>. Let us try this with <code>cat</code> command:
~~~bash
cat text2 >> text
[aaheikki:playground$] cat text
line 1
line 2
~~~
To add multiple files:
~~~bash
[aaheikki:playground$] cat text text2 >> text3
[aaheikki:playground$] cat text3
line 1
line 2
line 2
~~~
Note that you should add filename extensions according to their type by adding to the names end \[.txt .zip .png .xz .deb .iso\] and so on. Linux itself considers them as part of name, but other application use them.

#### File permissions
Let us look more closely what does the <code>ls -l</code> command show us.
~~~bash
[aaheikki:playground$] ls -l
total 12
-rw-r--r-- 1 aaheikki aaheikki 14 Feb 26 13:48 text
-rw-r--r-- 1 aaheikki aaheikki  7 Feb 26 13:47 text2
-rw-r--r-- 1 aaheikki aaheikki 21 Feb 26 13:49 text3
~~~

We will only cover the first section <code>-rw-r--r--</code>, but the Command Line book recommended covers these fields in more detail on page permission topic on page 15. The first character line "-" indicates that the file is regular file, <code>d</code> indicating it is directory and <code>l</code> indicating a link The next nine characters "rwx-"describes  read, write and execute permissions of user, group and others. Just line indicates no permission. The book covers permissions and their manipulation in detail on page 93. 

Simple way to change permissions is using <code>chmod</command>. Let us add execute permission for user and taking read permission away from others for text2 file:
~~~bash
[aaheikki:playground$] chmod u+x text2
[aaheikki:playground$] chmod o-r text2
[aaheikki:playground$] ls -l
total 12
-rw-r--r-- 1 aaheikki aaheikki 14 Feb 26 13:48 text
-rwxr----- 1 aaheikki aaheikki  7 Feb 26 13:47 text2
-rw-r--r-- 1 aaheikki aaheikki 21 Feb 26 13:49 text3
~~~
Set read, write and execute permission for all for text3 file
~~~bash
[aaheikki:playground$] chmod a=rwx text3
[aaheikki:playground$] ls -l
total 12
-rw-r--r-- 1 aaheikki aaheikki 14 Feb 26 13:48 text
-rwxr----- 1 aaheikki aaheikki  7 Feb 26 13:47 text2
-rwxrwxrwx 1 aaheikki aaheikki 21 Feb 26 13:49 text3
~~~
But it is not good practice to have higher permissions than necessary. There is also other way to set permissions witch is about mapping each "rwx" combination to number [0-7] and then the code would be <code>chmod 175 file_name</code>. Both work but the one showed is might be more intuitive to remember in practice.


#### (Zip)
- (xz, unxz) - compress or decompress .xz and .lzma files
- (zip, unzip) - package, compress or decompress zip archive files
As a heads up here are two often used compression commands that you will find useful. Use <code>man -k</code> or <code>apropos</code> to search for other compression tools that might be already installed.



### Package management
- apt - provides a high-level commandline interface for the package management system.
- .deb - deb is the software package format for the Debian Linux distribution and its derivatives.
- (dpkg) - package manager for debian.

Important difference between Linux distributions is the packaging systems. Ubuntu based on Debian .deb and <code>apt</code> is package tool for managing packages.
There is <code>apt search pattern</code>, but it might be easier to find packages that meet your needs from the internet and then install them using <code>apt install package_name</code> if that is an option or by downloading .deb file and then using <code>apt deb file_name.deb</code> or <code>dpkg -i file_name.deb</code>  to install it. The <code>dpkg</code> is low level package management, but mostly you get around with apt.

To keep your system up to date you just need to use <code>apt update; apt upgrade</code>. The <code>Sudo</code> command might be necessary with both. This should be done frequently and there are ways to automate this and other tasks by writing shell scripts. This should be enough and a bit more to get you started using the bash.