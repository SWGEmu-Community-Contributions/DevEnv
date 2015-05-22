# Testing
Dev Env Setup Testing

VirtualBox, VMWare, or native install. Edit as needed 
https://www.virtualbox.org/wiki/Downloads 
https://my.vmware.com/web/vmware/free#desktop_end_user_computing/vmware_player/7_0

	8g mem
	32g virtual drive
	max cores
	bridged network

# Install 64 bit OS - Debian 7 + 8, pointLinux, MakuluLinux, CentOS
Current test = Ubuntu 12.04 with Gnome Classic Tweaks
 
	Should work on any debian package distro
	https://www.debian.org/distrib/
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
	sudo apt-get upgrade
=====================
# Import scripts  
=====================
Copy this series of commands into a sudo terminal: Installs git, downloads scripts and installs them. Reboots the system. SAVE ALL WORK FIRST!!!

	sudo apt-get install -y -q git && git clone https://github.com/Scurby/Testing.git && cp -i /home/swgemu/Testing/README.md /home/swgemu/Documents && mkdir bin && cp -i /home/swgemu/Testing/bin/* /home/swgemu/bin/ && mkdir setup && cp -i /home/swgemu/Testing/setup/* /home/swgemu/setup/ && mkdir run && cp -r /home/swgemu/Testing/run/* /home/swgemu/run/ && chmod -v +x /home/swgemu/bin/* && PATH=$PATH:$HOME/bin $$ sudo /sbin/reboot
=====================
# Restart
	
Your system should reboot when you run the commands above. If it does then you have successfully installed the scripts and are ready to proceed with the SWGEmu Dev Env setup.

=====================
# Run setup scripts
=====================
The following scripts are run from the command line. They are numbered in the order I use them. 

1. options - Installs Optional packages

	- xclip 
	- terminator 
	- vim 
	- chromium 
	- quassel
	- git-cola
	- git-review
	- Asks to run 'first' script
        
2. first - Installs required packages and programs

	- gcc, g++, git, gdb, automake, make, libreadline-gplv2-dev
	- libncurses5-dev, libneon27, libaprutil1-dev, libtool
	- openjdk-6-jre, openjdk-6-jre-headless, libgtest-dev, screen
	- Lua-5.1 - Berkely DB 5.0 - MySQL Server and Workbench
	- Asks to run 'start' script

3. extras - Install the following EXTRA packages.
	
	libgtest-dev ctags vim-doc vim-scripts chromium-l10n gawk-doc 
	firmware-crystalhd libqca2-plugin-cyrus-sasl libqca2-plugin-gnupg 
	libqca2-plugin-ossl libqt4-dev qt4-qtconfig phonon-backend-gstreamer 
	phonon-backend-mplayer videolan-doc autoconf2.13 autoconf-archive 
	gnu-standards autoconf-doc libtool gettext g++-multilib 
	g++-4.7-multilib gcc-4.7-doc libstdc++6-4.7-dbg libstdc++6-4.7-doc 
	gdb-doc git-daemon-run git-daemon-sysvinit git-doc git-el git-arch 
	git-cvs git-svn git-email git-gui gitk gitweb openssh-server 
	libtool-doc gfortran fortran95-compiler gcj doc-base krb5-doc 
	krb5-user postgresql-doc-9.1 sqlite3-doc libipc-sharedcache-perl 
	libterm-readkey-perl tinyca python-crypto-dbg python-crypto-doc 
	python-pysqlite2-doc python-pysqlite2-dbg apache2-doc apache2-suexec 
	apache2-suexec-custom httpd-cgi libcgi-fast-perl 

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
Special Thanks to lordkator for the initial FastTrack VM Image and the scripts that this repository is based on. 
- Scurby

**************************************************************************************

Useful Stuff

	git log --pretty=format:'%h was %an, %ar, message: %s' -10

	PATH=$PATH:$HOME/bin

