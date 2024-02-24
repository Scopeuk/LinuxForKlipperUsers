# Foreword
First and foremost, this is a work in progress and is incomplete, pull requests and feedback welcome

This document aims to help a new user understand the commands they are likely to encounter in setup guides or similar, it necessarily skips over some elements of detail and nuance in favour of clarity.
The intention of this document is not to replace existing guides to instalation or update of klipper, that subject has been covered extensively and well elsewhere. Instead this document aims to let someone unfamiliar with linux understand what the commands guides are giving them to run do.
This is not intended to be a be all and end all guide to any of these commands.
As part of the short cuts taken guidance around system commands and application installation will focus on tools used by debian and it's derivatives (ubunutu, raspberry pi os etc) as these are the most commonly used distributions for new users.

# Structure of Commands
## Running a Command
Commands are in the format below where command is the name of a command, parameter_1, parameter_2 and parameter_3 are parameters or arguments passed to the command
`command parameter_1 parameter_2 parameter_3`
- All commands are executed in the current folder
- Commands can take any number of parameters 0 or more which change their behaviour
	Examples
	`ls` lists the current folder the command  is `ls`
	`ls /home` lists the /home directory the command  is `ls` again but this time we also have a parameter `/home`
	Many commands will take a path or file as a parameter to instruct the command which item to work from, parameters can also modify command behaviour
	`ls -l` the command is `ls` but we give an argument `-l` in this case ls will list extra details
	`ls /dev/serial/by-id/*` This is a fairly common command during initial setup for a klipper machine, the command is `ls` and the parameter is `/dev/serial/by-id/*`. `/dev/serial/by-id/*` is a special directory on the linux file system which contains a file for each serial device connected with a name reflecting what the operating system calls it see [Block Devices] (#Block Devices)
- Parameters may also be refered to arguments or switches. Switch is normally used for parameters of the form -x or --help which change the command behaviour

## Escaping a Running command
In the event you open a command which doesn’t close itself (or runs for a long time) the command can be instructed to stop with the keyboard combination `ctrl + c`

## Case Sensitivity
All linux commands and folder names are case sensitive, this means that file, File and FiLe are all different files and could be in the same directory, as this is for obvious reasons confusing people avoid names like this.
This is of note because whilst ls will list the files in the current directory LS or Ls will result in a command not found error.

## Tab Completion
Whilst using the terminal it is possible to ask for your current command or command part to be finished for you. This is helpful with say long file names where you can type the first two or three letters and then press tab to complete the full name, if there are multiple options hitting tab twice will list all of them.
This does not work with all commands but does work with almost all [file commands](# Finding your way around the file system) and [service commands](# Services).

## Sudo
The sudo command is a powerful utility command which is used to perform tasks with elevated permissions, roughly analogous to run as administrator functionality on windows. sudo does not do anything directly but instead runs the command in its parameters under the "root" user, the top level administrator account for a linux machine.
Typically the sudo command is needed when installing or updating tools, changing configuration files for the operating system or controlling services.

### Example
Running `whoami` will return your username
Running `sudo whoami` will return the username root as the command has been run as the root user.

## Command Chaining
Many commands in guides will chain commands, this is the process of writing a single line which executes multiple commands.
Most of these depend on the "return value" of the commands as they execute, the finer points of what these means is beyond this guide, for our purposes each command reports if it succeeded or failed and the joins can check this
there are multiple  ways to do this but the most common are below
| Join | Purpose |
| ------------ | ------------ |
| && | if the command before && returns success execute the second command |
| &#124;&#124; |  if the command before && returns failure execute the second command |
| ; | run the command before ; and then run the command after ; unconditionally |

### Examples
`cd ~ && git clone https://github.com/dw-0/kiauh.git` run the command `cd ~` and if that is successful then run the command `git clone https://github.com/dw-0/kiauh.git`

# Finding Help
## Help Parameters
Most commands supply a help option usually this is `--help` or `-h` as a parameter
e.g. `ls --help`
## Man Command
`man` is the manual command, man is a command which accesses documentation for other commands, these manual pages can be very verbose and technical but likely include all the detail you could need if doing something unusual
  Usage example
- `man ls` this will launch the manual tool pointed at the entry for the ls command

# Finding your way around the file system
Assuming you have found your way into a terminal via ssh or the device its self the following commands should help with moving between folders or identifying where you are
included here are also the comands for moving, copying and renaming files
## Magic symbols
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
|cp| copy a file from parameter 1 to parameter 2 |
|mv| move a file from parameter 1 to parameter 2 |

## common usage
`cd ..` move up one folder i.e. from /home/me to /home
`cd ~/klipper` move to the folder called klipper in the users home directory, frequently this is where klipper is installed by most people
`mv out/klipper.bin out/firmware.bin` rename the generated firmware image from klipper.bin to firmware.bin, here the comand is assumed to be running from ~/klipper as this is where the firmware build commands normally run from

# Git
Git is a version control system, these are likely unfamiliar terms but for most of our usage this means that the git command can be used to make a copy of a folder from a git repository (like the one klipper is held in https://github.com/Klipper3d/klipper) or update the files in a repository we previously copied. The tool will track files it is made aware of and allow for copies of the "repository" or collection of files to be made and for any changes to be kept in sync, this is how updates made through mainsail or fluid work in the background.
git is a complex tool and can produce errors or issues which will need different resolutions, this is rare when using commands such as clone or creating and initial installation.
a "cheat sheet" for many git commands is available at https://training.github.com/downloads/github-git-cheat-sheet/ and full details are available online. Full usage of git is outside of the scope of this documentation.

git works like other commands documented above although the first parameter passed to git is normally an instruction for the type of action to be undertaken.
In the next few sections we explore a few commonly used git commands
## git clone
This command is used to get a copy of a repository held in git a in the current working folder, most commonly this is used to get klipper(https://github.com/Klipper3d/klipper) or KIAUH (https://github.com/dw-0/kiauh) during an initial installation.
### Example command
`git clone https://github.com/dw-0/kiauh.git`  This command breaks down into three parts, `git` the command we want to run `clone` the operation we want to perform and `https://github.com/dw-0/kiauh.git` this tells git clone where to get the files it should clone. This will create a folder with the repository name kiauh (the last bit after / and before .git) in the current working directory. Additional parameters can be passed to the clone command to tweak its behaviour, these are rarely needed in our use case.

## git pull
This command must be run inside a directory which git created (usually in our case through a git clone command). It will update the local files in the folder to match the latest version it was cloned from.
### Example command
`git pull` This command breaks down as run git with an instruction to pull the latest version of the parent repository. git will then check for changes between your local files and the parent and try to update the files, in the event there is a conflict (a file modified differently both locally and in the parent repository) git will attempt to resolve the issue or if this fail will ask you what to do. It is rate for klipper users to directly perform this operation and it is more typically invoked via one of the klipper web interfaces like Fluid or Mainsail.


# installing tools (apt-get)
the apt and apt-get commands allow for tools and their dependencies to be installed and maintained by the operating system. This can be considered to be a little like an app store in how it behaves
apt and apt-get are two different interfaces to the same tooling, apt is the more modern version but frequently apt-get os called for in example commands.
we will document apt-get here for this reason.
all commands in this section will require "admin" permissions to run successfully, this is done by starting the command with the sudo, super user do command see [sudo](#sudo)

apt-get works like other commands documented above although the first parameter passed to apt-get is normally an instruction for the type of action to be undertaken.

## apt-get update
The command `apt-get update` will update the locally stored index of what tools are available and at what version, it does not make any changes to the installed files

## apt-get upgrade
The command `apt-get upgrade` will update the tools installed and tracked by apt-get (including most of the pre-installed applications) to the latest version in the local database (see [apt-get update](#apt-get update) )
This command will note upgrade code operating system features

## apt-get dist-upgrade
The command `apt-get dist-upgrade` is much like the apt-get upgrade command but it will also update the underlying core operating system files

## apt-get install
The command `apt-get install` is used to install a new tool or library. install accepts a `-y` switch which will make it automatically answer yes to questions to the user.
The most frequent question posed by this tool is "installing this tool will require 30MB of disk space, continue?" so it is frequently added in installation guides.

examples
| Command | Meaning |
| ------------ | ------------ |
| `sudo apt-get install git` | this will instruct apt that the git tool should be installed |
| `sudo apt-get install git -y' | this will instruct apt-get that the git tool should be installed and that any prompts to the user should be answered yes automatically |


# Commands which end in .sh
These are not strictly commands but are instead scripts, scripts are a series of commands which automate tasks for you, commonly tools which we install from git such as Kiauh or Klipper itself.
commonly these commands will have the form `./toolname/script.sh` this is running a script called script.sg which is located in a folder called toolname under the current working folder
## Example
Below we have an example of a sequence from the Kiauh install script
First move to the home directory (~) and then git is used to get Kiauh into the folder kiauh
`cd ~ && git clone https://github.com/dw-0/kiauh.git`
And then run a script that is in that folder
`./kiauh/kiauh.sh` This runs the script by starting in the current folder . then folder kiauh then a script called kiauh.sh, this assumes that the user is still in the directory ~ from the cd command above
A common error to see with script launch commands is to try and launch the command whilst in the wrong directory, look carefully at any instructions for and `cd` commands.

# Where is my hardware
## Block Devices
The linux operating system maps all hardware devices are files, this may seem a little odd if you are used to how windows handles devices, it is not necessary to understand why this is the case or the advantages or disadvantages here.
This affords some advantages in our use case.
The underlying hardware handling on modern linux distribution is performed by a tool called udev. This uses a series of rules to create device files on the disk. All very confusing and "technical" but for us this means that a printer connected by a usb port will appear in the directory `/dev/serial/by-id/` and we can therefore use the `ls` command to look for devices in here, due to the magic of udev these will even frequently have helpful names including klipper or marlin in the device names.

## Useful Commands
| Command | Purpose |
| ------------ | ------------ |
| lsusb | This will list all currently connected usb devices, want to know if your printer is being picked up, run this command, unplug the printer and run it again |
| dmesg | This is a log of things that the operating system is doing, this includes hardware connection and disconnection |
| dmesg -w | this is like the command above but it will watch the output until closed with ctrl + c, try running this command and then plugging in a usb device |  

# Services
Like all operating systems linux uses background services to provide functionality which runs at boot up.
In common use with klipper instalations there are a handful of services which we might interact with.
On most modern linux discributions, including all common klipper host options services are managed through systemd.
The finer details of what all of this means and how it works is not too important however commands come up for starting and stopping services so these are recorded below
Most control of the services are done through the `systemctl` command

## Why?
These commands are not used in normal operation but can be helpful if a machine is not starting properly or during firmware flashing.
A common use case is to stop the klipper service so that a firmware update tool can talk to the serial port used by the control board during an mcu firmware update.

## General Structure
`systemctl` commands are generally structured as `systemctl instruction service`
where 
| Part | Purpose |
| ------------ | ------------ |
| instruction | What you wish to do with the service for instance `start` or `stop` |
| service | The name of the service we want to apply that command to common examples `klipper` `moonraker` |

## Instructions
This is an incomplete list of instructions for systemd and only aims to cover the main options in common use.
| Instruction | Purpose |
| ------------ | ------------ |
| start | Starts a service which is currently stopped |
| stop | Stops a service which is currently running |
| restart | Stops and then (re)starts a service, this is how reloading klipper configuration files works under the hood |
| status | Reports if a service is running, provides some limited information if it stoped unexpectedly |
| enable | changes the default state of the service so that it runs at boot |
| disable | turns the service off at boot (will require manualy starting) |

## Service Names
| Service | What it does |
| ------------ | ------------ |
| klipper | The main part of the klipper firmware and is responsible for turning gcode into machine movement and heating |
| moonraker | The "api server" provides a connection between Klipper above and the common web interfaces below |
| mainsail | Provide the web pages you land on when you access your machine over the network (if you use mainsail) |
| fluidd | Provide the web pages you land on when you access your machine over the network (if you use fluid)

## Example Systemd Commands

| Command | Purpose |
| ------------ | ------------ |
| systemctl status klipper | Check if the klipper service is running |
| systemctl stop klipper | Stop the klipper service |
| systemctl start klipper | Start the klipper service |
| systemctl restart moonraker| Stop and then re(start) the moonraker service |


