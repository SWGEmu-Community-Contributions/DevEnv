# Testing
****************************************************************************************************************
Special Thanks to lordkator for the initial FastTrack VM Image and the scripts that this repository is based on. 
****************************************************************************************************************
Dev Env Setup Testing

VirtualBox, VMWare, or native install.

	8g mem
	32g virtual drive
	max cores
	bridged network

# Install 64 bit OS - Debian 7 + 8, pointLinux, MakuluLinux
Current test = Ubuntu 12.04 with Gnome Classic Tweaks
 
****************
	username=swgemu
	password=123456
	root pw=12345678
****************
Predefined software selections - Default selection

	(*)Debian Desktop
	    (*) Gnome
	(*)Print Server
	(*)Standard System Utilities
# Config sudoer as needed 

https://www.digitalocean.com/community/tutorials/how-to-add-delete-and-grant-sudo-privileges-to-users-on-a-debian-vps

We give users access to the sudo command with the visudo command. If you have not assigned additional privileges to any user yet, you will need to be logged in as root to access this command:

	visudo
	
When you type this command, you will be taken into a text editor session with the file that defines sudo privileges pre-loaded. We will have to add our user to this file to grant our desired access rights.

Find the part of the file that is labeled "Allow members of group sudo to execute any command". It should look something like this:

	# Allow members of group sudo to execute any command
	%sudo   ALL=(ALL:ALL) ALL

	
We give a user sudo privileges by copying the line beginning with "%sudo" and pasting it after. We then change the user "%sudo" on the new line to our new user, like this:

	# Allow members of group sudo to execute any command
	%sudo   ALL=(ALL:ALL) ALL
	%newuser   ALL=(ALL:ALL) ALL
	
We can now save the file and close it. By default, you can do that by typing Ctrl-X and then typing "Y" and pressing "Enter".

# Run Updates

	sudo apt-get update
=====================
# Import scripts  
=====================
Copy this series of commands into a sudo terminal: Installs git, downloads scripts and installs them.

	sudo apt-get install -y -q git && git clone https://github.com/Scurby/Testing.git && cp -i /home/swgemu/Testing/README.md /home/swgemu/Documents && mkdir bin && cp -i /home/swgemu/Testing/bin/* /home/swgemu/bin/ && mkdir setup && cp -i /home/swgemu/Testing/setup/* /home/swgemu/setup/ && mkdir run && cp -r /home/swgemu/Testing/run/* /home/swgemu/run/ && chmod -v +x /home/swgemu/bin/* && PATH=$PATH:$HOME/bin

=====================
# Run setup scripts
=====================
The following scripts are run from the command line. They are numbered in the order I use them. 

1. options - Installs Optional packages including xclip, vim, quassel, and others. Asks to run 'first' script.

2. first - Installs required packages and programs including Lua, BerkelyDB, and others. Asks to run 'start' script.

3. extras - Installs EXTRA packages.

4. start - Initial setup of development environment

	- Choose editor
	- Setup git user.* config
	- Setup ssh key
	- Register on gerrit
	- Test Gerrit setup
	- Clone repos and checkout a local branch of Core3 origin/unstable
	- Symlinks (idlc)
	- Engine library
	- MySQL database checks
	- Server configuration
	- Tre files
	- Asks if you want to build and run the server. 

5. build - simple build script

	- 3 options- build, build config, build clean

6. run_dev - Builds and run the development server and launch it under gdb on a 'screen'

	***NOTE: run_dev uses gdb in batch mode and starts with the commands
	in ~/run/run_gdb which you can change to your pleasing;
	(breakpoints, dumps, settings etc.)
**************************************************************************************
# The following scripts are also useful...

ack - Nice source grep tool (try: cd ~/workspace/MMOCoreORB/src; ack PlanetManager).

full - options, first, and start scripts combined.

prime - Provides info to set sudo permissions.

bang - dl's and installs these scripts

cleanup_for_publish - Strips virtual machine down for distribution, creates version number, resets pwds, etc. USE WITH CAUTION!!!

createdb - mysql table, user, and pwd tool.
(http://jetpackweb.com/blog/2009/07/20/bash-script-to-create-mysql-database-and-user/)

setup - dl and install scripts

godmode - sets acct with ID=1 to Admin (15). Run after first acct is created.

myip -  display the ip of the VM and login port for quick configuration of the windows client.

updateip - Get ip address of local eth0 and update galaxy table as needed.

latest - do a quick git-stash, git-pull, and git-stash-apply so you can get to the latest code w/o loosing local work.

freeze - Save your devenv state so you can repeat the same tests over and over.

thaw - allow server to continue from previous state each time you run it.

installed - Package and version check saved to /home/<file>.txt.

**************************************************************************************
*FIXME* *FIXME* *FIXME*
dropbox - DL and install dropbox

openfile {filename} - open file in eclipse *FIXME*

ide - Choose IDE and/or options

idlc - idlc install tool

eclipse - install eclipse, import project and set git properties. *FIXME*
	(Requires Egit-properties.tar.gz in /home/setup/ )
	(May requires indexing exlusions)

**************************************************************************************


**************************************************************************************

Useful Stuff

	git log --pretty=format:'%h was %an, %ar, message: %s' -10

	PATH=$PATH:$HOME/bin

