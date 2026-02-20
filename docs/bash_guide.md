
## Introduction to bash shell

### Windows sub system for linux
For windows users on powerShell(needs admin rights):
~~~powerShell
wls --install 
~~~
defaults to ubuntu if not then install with:

~~~powerShell
wls.exe --install ubuntu
~~~
reboot necessary.

After reboot launch ubuntu in powerShell by:
~~~powerShell
wls.exe --distribution ubuntu
~~~
or from windows menu

List of other available distributions
~~~powerShell
wls.exe --list --online
~~~
### Basic commands

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