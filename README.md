# SWGEmu Development Environment setup

****************************************************************************************************************
Special Thanks to lordkator for the initial FastTrack VM Image and the scripts that this repository is based on. 
****************************************************************************************************************

VirtualBox, VMWare, or native install.

	8g mem
	32g virtual drive
	max cores
	bridged network

# Install Debian 64bit Desktop OS 
(or variant)
* Debian - https://www.debian.org/
* pointLinux - http://pointlinux.org/
* MakuluLinux - http://makululinux.com/
* LinuxMint Debian Edition - http://www.linuxmint.com/download_lmde.php
 
### Login info
* username = swgemu
* password = 123456
* root pw = 12345678

### Predefined software selections

	(*)Debian Desktop
	    (*) Gnome
	(*)Print Server
	(*)Standard System Utilities
	
#### Config sudoer as needed 

https://www.digitalocean.com/community/tutorials/how-to-add-delete-and-grant-sudo-privileges-to-users-on-a-debian-vps

# Import scripts

Copy this series of commands into a sudo terminal: Installs git, downloads scripts and installs them.

	sudo apt-get update && sudo apt-get install -y -q git && git clone https://github.com/SWGEmu-Community-Contributions/DevEnv.git && cp -i /home/swgemu/DevEnv/README.md /home/swgemu/Documents && mkdir bin && cp -i /home/swgemu/DevEnv/bin/* /home/swgemu/bin/ && mkdir setup && cp -i /home/swgemu/DevEnv/setup/* /home/swgemu/setup/ && mkdir run && cp -r /home/swgemu/DevEnv/run/* /home/swgemu/run/ && chmod -v +x /home/swgemu/bin/* && PATH=$PATH:$HOME/bin

## Run setup scripts

The following scripts are run from the command line. They are numbered in the order I use them. 

1. options - Installs Optional packages including xclip, vim, quassel, and others. Asks to run 'first' script.
2. first - Installs required packages and programs including Lua, BerkelyDB, and others. Asks to run 'start' script.
3. start - Setup of development environment follows these steps:
   * Choose editor
   * Setup git user.* config
   * Setup ssh key
   * Register on gerrit
   * Test Gerrit setup
   * Clone repos and checkout a local branch of Core3 origin/unstable
   * Symlinks (idlc)
   * Engine library
   * MySQL database checks
   * Server configuration
   * Tre files
   * Asks if you want to build and run the server. 
4. build - simple build script
   * 3 options- build, build config, build clean
5. run_dev - Builds and runs the development server.
   * Using this command to start the server will: 
   * launches the server under gdb on a 'screen'.
   * outputs a screenlog to ~/run/screenlog*
   * use the config.lua in ~/run/conf/ to relace the config.lua in ~/MMOCoreORB/bin/conf.  
   * uses gdb in batch mode and starts with the commands  in ~/run/run_gdb which you can change to your pleasing; (breakpoints, dumps, settings etc.)
6. eclipse - Installs eclipse luna, imports project and sets git team properties.
   * (Requires Egit-properties.tar.gz in /home/setup/ )
   * (Requires indexing exlusions)
7. latest - do a quick git-stash, git-pull, and git-stash-apply so you can get to the latest code w/o loosing local work.

### The following scripts are also useful...
* ack - Nice source grep tool (try: cd ~/workspace/MMOCoreORB/src; ack PlanetManager).
* freeze - Save your devenv state so you can repeat the same tests over and over.
* thaw - allow server to continue from previous state each time you run it.
* extras - Installs EXTRA packages.
* full - options, first, and start scripts combined. *Refactor to here*
* cleanup_for_publish - Strips virtual machine down for distribution, creates version number, resets pwds, etc. **USE WITH CAUTION!!!**
* createdb - mysql table, user, and pwd tool.
  * Ref: (http://jetpackweb.com/blog/2009/07/20/bash-script-to-create-mysql-database-and-user/)
* myip -  display the ip of the VM and login port for quick configuration of the windows client.
* updateip - Get ip address of local eth0 and update galaxy table as needed.
* installed - Package and version check saved to /home/<file>.txt.
* ~~prime - Provides info to set sudo permissions.~~
* ~~bang - dl's and installs these scripts~~
* ~~idlc - idlc install tool~~


**************************************************************************************
#### Useful Stuff
* git log --pretty=format:'%h was %an, %ar, message: %s' -10
* PATH=$PATH:$HOME/bin

**************************************************************************************
#### FIXME's
* openfile {filename} - open file in eclipse
* godmode - sets acct with ID=1 to Admin (15). Run after first acct is created.

**************************************************************************************
