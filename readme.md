**Table of Contents**

[TOCM]

[TOC]

# Structure of Commands
commands are in the format below where command is the name of a command the parameters are parameters or arguments passed to the command
`command parameter_1 parameter_2 parameter_3`
- all commands are executed in the current folder
- commands can take any number of parameters 0 or more which change their behaviour or instruct how they should behave
	examples
	`ls` lists the current folder the command  is `ls`
	`ls /home` lists the /home directory the command  is `ls` again but this time we also have a parameter `/home`
	many commands will take a path or file as a parameter to tell it what to work from but also allow arguments to modify behaviour
	`ls -l` the command is `ls` but we give an argument `-l` in this case ls will list extra details
#	Finding Help
	most commands supply a help option usually this is `--help` or `-h` as a parameter
	e.g. `ls --help`
	the man command
- man "manual" this is a tool which documents other tools, these help pages can be very verbose and technical but likely include all the detail you could need
- man ls this will launch the manual tool pointed at the entry for the ls command
	

# Fnding your way around
##Magic symbols
| Symbol | Meaning |
| ------------ | ------------ |
|~|    the current users home directory typically this will be /home/klipper or /home/pi (the last part is your user name)|
|. |   a relative link to the current folder|
|..|   a relative link to the parent folder |
## Commands
| Command | Meaning |
| ------------ | ------------ |
|pwd| "print working directory" shows where you currently are|
|whoami| tells you your current username|
|cd| "change directory" lets you move to another folder, accepts absolute and relative paths|
|ls| lists the contents of the current folder|
