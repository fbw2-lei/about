# unix basic commands and their use

## basic commands

all key combinations involving numbers, use the number keys above the letters (avoid num pad)

opening a terminalwindow with `Ctrl+ Alt + T`

clearing the terminal window

`$ clear`

show the history of previous terminal commands with history

`$ history`

autocomplete filenames of the directories you can use the tab-key (between shift-hold and caret ^)

`$ cd Do`(+ tab key) -> autocomplete to cd Documents/

Commands can be chained with `&&` (double ampersand symbols) shift+6

Output of commands can be redirected as input to other commands or filenames with `>>` 
(double greater than) > is located between left Shift and Y-key

example:
`$ ll >> listing.txt`

> this will redirect the output of the ll command (file details, 1 line per file) to the textfile listing.txt

### output strings

you can write text to standard output (terminalwindow) with echo

`$ echo "something" `


### moving around

changing password for current user:

$ passwd 

changing directories / cd

$ cd 

navigating to a specific directory

$ cd <directoryname>

navigating to the parent directory

$ cd .. 

navigating back to the last current directory

$ cd -

navigating back home with tilde (Alt Gr + `+`)

$ cd ~

getting to the root (/) of the filesystem

$ cd /

## navigation , to list directories and files

printing the content of current directory to standard output

$ ls 

list files as rows (one row per file/directory)

$ ls -l

-l provides  additional information about files:

filetype; filepermissions; links; owner (username); group; filesize; modification; timestamp; name

### file permissions

1st letter indicates general filetype
d - directory
l - (symbolic) link
- - regular files

filepermisson in unix 
  * have 3 access levels (user, group, other) and per level 
  * have 3 flags indicating what users of this level are allowed to do:

rwx (read, write, execute permission)

so reading a list of flags from ls -l like this:

-rwxrw-r-- 

break it into components like this

first letter indicates file type (d-directory, l-link, - common)
- minus indicates a regular file

then break into the access levels 3 symbols per level
owner: rwx
group: rw-
other: r--

so the owner can read, write and execute this file
users of the group the file belongs to can read and write, but not execute
others can only read.

changing priviledges to files:

$ chmod <flags> filename

<flags> is 3 decimal numbers representing a combination of binary flags for any access group
(4) read permission
(2) write permission
(1) execute permission

e.g. read + write only : 4 + 2 = 6
e.g. read + execute only: 4 + 1 = 5

access groups follow the order : owner, group, other

e.g. 755 means: all rights for owner and read+execute for group and other

### hidden files

usually start with a dot character e.g. .bash_history

to view them use -a with ls command

$ ls -a

combine parameters -l -a 

$ ls -l -a

shortcuts

$ ll (= ls -l -a)

## creating, reading, modifying files

use touch to create (bunches of) files

$ touch <filename> <anotherfilename>

for existing files, touch updates the last-modified timestamp

simple text editor inside the terminal

$ nano

menu at the bottom, commands with ^<letter> has to be execute with Ctrl+<letter>
commands with M-<letter> has to be executes with Alt+<letter>

e.g. ^O (Ctrl+O) "write out" - to save the file to disk
e.g. ^X (Ctrl+X) to exit the nano editor

writing the content of files to standard output / terminal

$ cat <filename>

does not stop to output a file, also when the content does not fit the screen

$ less <filename>

allows us to read a file pagewise (Page up and down keys) or linewise (Cursur up+down)
exit less command with q 

## getting help


### from help command
get a list of common shell basic commands

$ help 

get help to a specific command

$ help <commandname>

e.g. help cd displays the help to cd command containing all parameters available

### from a command itself

use a commands built-in help page (usually working) with --help parameter

$ <command> --help

e.g. cd --help


### from the manual

manual pages for other commands that are not basic shell commands 

$ man <command>

e.g. the help for chmod can be read with `man chmod`

manual pages can be read pagewise with page up and down keys
exit man with q-key

## creating directories

$ mkdir <dirname(s)>

you can create more than one at once

## removing files

$ rm <filename>

removing empty directories need an additional parameter -d

$ rm -d <directoryname>

removing non-empty directories recursively with parameter -r

$ rm -r <nonemptydirname>

alternatively you can use rmdir as dedicated command to remove directories

$ rmdir <emptydirname>


## moving files

change the location of a file to another directory

$ mv <filename(s)> <directory>

## copying files

make a copy of source files to a target directory

$ cp <source(s)> <target>

## symbolink links

create a shortcut to another directory

$ ln -s <targetdirectory> <linkname>

e.g. ln -s /home/andre/Documents/introductions intro


## installing software to unix systems

usually we use package managers like apt (advanced package tool)

$ apt --help

### checking available packages (based on our system, and trusted repositories)

$ apt list [<searchstring>]

### list installed packages

$ apt list --installed

### install additional software packages

e.g. inkscape (vecor graphic drawing program)

$ sudo apt install inkscape

it will search for dependent packages and offer to resolve the dependencies and install everything that is needed

### un-installing packages

$ sudo apt remove <packagename>

### clean system from unused packages

$ sudo apt autoremove

### check for updates of installed packages

$ apt list --upgradable

### upgrading a package

$ sudo apt upgrade <packagename>

## executing commands as another (e.g. root) user

the command is sudo (superuser do)

$ sudo <command> 

we will be asked to input our password

## check for running processes

$ top
quit it with q key

## kill running processes

by their process id (PID) 

$ kill <process id>

by their name 

$ killall <process name>

## disabling slack app on your computer

disable it in snap package manager (for 3rd party packages)

$ snap disable <package>


# Version Control System GIT

git is the name of the software, it's a command line tool, we use it on the terminal

(maybe you need to install it on a fresh mashine (e.g. apt install git)

intention is to keep track of changes inside a "repository"

## vocabulary

repository - track / collection of all versions/changes to a project/directory 

commit - a single change to the repository that is made in a single step (always identifiable to a user, contains a description) 

branch - a set of changes made to a project
default branch : always there , named master 

## initializing an empty repository

$ git init

-> creation of a .git subdirectory (this contains all needed information for git to keep track of your changes)

## check the status of the repository compared to working directory

$ git status

## setting up git 

$ git config --global user.name "username"

for teaching at DCI program this should equal your github.com account name

$ git config --global user.email "me@you.com"

## introducing the files/directories to keep track of (called "Staging")

telling git, to record changes to specific (or all) files/directories

`$ git add **filename(s)**`
`$ git add -A`

## commiting changes to a repository

`$ git commit -m "comment to describe, what changed"` 

## chaining staging and committing in one line

`$ git add -A && git commit -m "comment"`

or alternatively create a subcommand alias

`$ git config --global alias.**aliasname** '!git add -A && git commit'`

execute that alias

`$ git **aliasname** -m "commitment comment"`

## creating new branches

`$ git branch **newbranchname**`
`$ git checkout **branch**`

you can combine branching and checkout in one command

`$ git checkout -b **newbranch**`

## connecting to a remotely hosted repository

`$ git remote add **remote-lable** **remote-URL**`

remote-URL is usually a github.com link (to the .git file)

## cloning from a remote repository

`$ git clone **URL**`

will ask you for username / password, if the repo is private

this by default keeps a remote configuration to have label `origin` contected to URL, so you can use origin as label for pushing and pulling

## pushing local changes to remote repository

`$ git push **remote-label** **master**`

after cloning, your default label of the remote repository is `origin`







