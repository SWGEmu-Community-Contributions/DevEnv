# Testing
Dev Env Setup Testing

VirtualBox, VMWare, or native install. Edit as needed 
https://www.virtualbox.org/wiki/Downloads 
https://my.vmware.com/web/vmware/free#desktop_end_user_computing/vmware_player/7_0

	8g mem
	32g virtual drive
	max cores
	bridged network

# Install OS - Debian 8 Test
https://www.debian.org/distrib/

	(net install) 64 bit 
	Should work on any debian package distro
****************
	username=swgemu  - TODO make configurable
	password=123456
	root pw=12345678
****************
Predefined software selections - Default selection

	(*)Debian Desktop
	    (*) Gnome
	(*)Print Server
	(*)Standard System Utilities
****************
# Config sudoer as needed 
Run 'prime' 

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
****************
Run Updates

	sudo apt-get update
=====================
# Import scripts  
=====================
Copy this series of commands into a sudo therminal: Installs git, downloads scripts and installs them. Reboots.

	sudo apt-get install -y -q git && git clone https://github.com/Scurby/Testing.git && cp -i /home/swgemu/Testing/README.md /home/swgemu/Documents && mkdir bin && cp -i /home/swgemu/Testing/bin/* /home/swgemu/bin/ && mkdir setup && cp -i /home/swgemu/Testing/setup/* /home/swgemu/setup/ && mkdir run && cp -r /home/swgemu/Testing/run/* /home/swgemu/run/ && chmod -v +x /home/swgemu/bin/* && sudo /sbin/reboot
=====================
# Restart
	
Your OS should reboot when you run the commands above. If it does then you have successfully installed the scripts and are ready to proceed with the SWGEmu Dev Env setup.

=====================
# Run setup scripts
=====================
The following scripts can be run from the command line. They are numbered in the order I use them. They will also output results to /home/install.txt

1. options - Installs Optional packages

	- xclip 
	- terminator 
	- vim 
	- chromium 
	- quassel
	- git-cola
	- git-review
	- first;
        
2. first - Installs required packages and programs

	- gcc, g++, git, gdb, automake, make, libreadline-gplv2-dev
	- libncurses5-dev, libneon27, libaprutil1-dev, libtool
	- openjdk-6-jre, openjdk-6-jre-headless, libgtest-dev, screen
	- Lua-5.1 - Berkely DB 5.0 - MySQL Server and Workbench
	- start;

2b. extras - TODO

3. start - Initial setup of development environment

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
	- build config; run_dev;

4. build - simple build script

	- build config does 'make config' and 'make clean'
	- build clean does 'make clean'

5. run_dev - Build and run the development server and launch it under gdb on a 'screen'

	***NOTE: run_dev uses gdb in batch mode and starts with the commands
	in ~/run/run_gdb which you can change to your pleasing;
	(breakpoints, dumps, settings etc.)
**************************************************************************************
# The following scripts are also useful...

ack - Nice source grep tool (try: cd ~/workspace/MMOCoreORB/src; ack PlanetManager).

full - options, first, and start scripts combined.

prime - Provides info to set sudo permissions.

bang - dl and install scripts

cleanup_for_publish - Strips VM image down for distribution, creates version number, resets pwds, etc.

createdb - mysql table user and pwd tool.

setup - dl and install scripts

godmode - sets acct with ID=1 to Admin (15). Run after first acct is created.

myip -  display the ip of the VM and login port for quick configuration of the windows client.

updateip - Get ip address of local eth0 and update galaxy table as needed.

latest - do a quick git-stash, git-pull, and git-stash-apply so you can get to the latest code w/o loosing local work.

freeze - Save your devenv state so you can repeat the same tests over and over.

thaw - allow server to continue from previous state each time you run it.

installed - Package and version check sent to /home/<file>.txt.

**************************************************************************************
*FIXME* *FIXME* *FIXME*
dropbox - DL and install dropbox

openfile {filename} - open file in eclipse *FIXME*

ide - Choose IDE and/or options

idlc - idlc install tool

eclipse - install eclipse, import project and set git properties. *FIXME*
	(Requires Egit-properties.tar.gz in /home/setup/

**************************************************************************************
Special Thanks to lordkator for the initial FastTrack VM Image and the scripts that this repository was based on. 
- Scurby

**************************************************************************************

Useful Stuff

	git log --pretty=format:'%h was %an, %ar, message: %s' -10

