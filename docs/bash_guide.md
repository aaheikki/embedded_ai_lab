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

- pwd
- ls -lha
- cd
- cat, more, less, tail, head
- mv
- cp
- rm
- chmod ugo a +-rwx
- grep  
- vim, nano