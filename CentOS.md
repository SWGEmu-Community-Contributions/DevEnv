# CentOS 6.6 x86_64 SWGEmu Core3 Compile Guide

Courtesy of Aso 
http://www.swgemu.com/forums/showthread.php?t=161787

This guide assumes that you have a general knowledge of Linux operating systems and have a Desktop installed on the server.

Note: For this guide, we will be using /home/swgemu/Git/ as our code directory. You can use whatever directory you want, but paths in this guide will need to be modified.

#Section 1. Installing the Dependencies needed for Core3 to compile & run

***1.1 Dependencies installed with YUM
Execute the following commands in the terminal:
	
	yum install gcc-c++.x86_64 make.x86_64 gdb.x86_64 automake.noarch subversion.x86_64 git.x86_64 lua lua-devel.x86_64 mysql-server mysql-devel.x86_64 java-1.8.0-openjdk.x86_64
	/sbin/chkconfig --add mysqld
	/sbin/chkconfig mysqld on
	service mysqld start

***1.2 Installing the Berkeley Database
Download Berkeley Database here: 

http://download.oracle.com/berkeley-db/db-5.0.32.NC.tar.gz

Extract db-5.0.32.NC.tar.gz.

Execute the following commands in the terminal:
	
	cd /path/to/db-5.0.32.NC/build_unix
	../dist/configure
	make
	make install

*1.3 Creating the necessary symbolic links

Execute the following commands in the terminal:
	
	ln -s /usr/local/BerkeleyDB.5.0/lib/libdb-5.0.so /usr/lib64/libdb-5.0.so
	ln -s /usr/lib64/mysql/libmysqlclient.so /usr/lib64/libmysqlclient.so
	ln -s /usr/lib64/mysql/libmysqlclient.so.16 /usr/lib64/libmysqlclient.so.16

*1.4 Downloading and installing Eclipse

Download Eclipse IDE for C/C++ Developers here: 

https://www.eclipse.org/downloads and install.

*1.5 Uploading your TRE files

Core3 needs the Star Wars Galaxies client TRE files to operate. Upload them to your server environment in a directory of your choosing.

# Section 2. Obtaining the code and compiling in Eclipse

*2.1 Obtaining the code

Obtaining Core3 Source Code:
	
	In eclipse, click on file and select Import...
	Expand Git and select Projects from Git. Click next.
	Select Clone URI and click next.
	In the URI box, enter: "http://gerrit.swgemu.com/Core3". Click Next.
	Select the unstable branch. Click next.
	In the Directory box, enter: /home/swgemu/Git/Core3. Click Next.
	The Core3 Source code will checkout. Once that is done, click next and then finish.

Obtaining the Public Engine Source Code:
	
	In eclipse, click on file and select Import...
	Expand Git and select Projects from Git. Click next.
	Select Clone URI and click next.
	In the URI box, enter: "http://gerrit.swgemu.com/p/PublicEngine.git". Click Next.
	Select the Master branch. Click next.
	In the Directory box, enter: /home/swgemu/Git/PublicEngine. Click Next.
	The Public Engine Source code will checkout. Once that is done, click next and then finish.

*2.2 Preparing to compile

Preparing the Public Engine for compile:
	
	In Eclipse under Project Explorer, expand MMOEngine and then expand lib.
	Inside the lib directory, create a new directory called unix.
	Copy libengine3.a in the linux64 directory to the unix directory you just created.

Setting the CLASSPATH:
	
	In Eclipse under Project Explorer, right click on MMOCoreORB and click properties at the bottom.
	On the side menu, select C++ Make Project.
	Select the Environment tab and click new to add a new environment variable.
	In the Name box, enter CLASSPATH. In the Value box, enter /home/swgemu/Git/PublicEngine/MMOEngine/bin/idlc.jar. Click Ok, then click Ok again to close the properties window completely.

Editing configure.ac for CentOS paths

In Eclipse under Project Explorer, expand MMOCoreORB and open configure.ac

Inside configure.ac at line 59 to 62, replace:
	
	SYSTEM_INCLUDES="" 
	SYSTEM_LIBS="-lrt -ldl -pthread"
	USER_INCLUDES_PATH="/usr/local/include"
	USER_LIBS_PATH="/usr/local/lib"
With:
	
	SYSTEM_INCLUDES="" 
	SYSTEM_LIBS="-lrt -ldl -pthread"
	USER_INCLUDES_PATH="/usr/include"
	USER_LIBS_PATH="/usr/local/lib64"

Creating the necessary symbolic links and permissions for Eclipse:

Execute the following commands:
	
	ln -s /home/swgemu/Git/PublicEngine/MMOEngine /home/swgemu/Git/Core3/MMOEngine
	ln -s /home/swgemu/Git/PublicEngine/MMOEngine/bin/idlc /usr/local/bin/idlc
	chmod 755 /home/swgemu/Git/PublicEngine/MMOEngine/bin/idlc

*2.3 Compiling the Core3 server
	
	In Eclipse under Project Explorer, right click on MMOCoreORB. Mouse over Make Targets and select Build.
	Select configure and then click Build. Run this step twice.
	After you have run configure twice, hover over Make Targets again and select Build.
	Select All and then click build.

At this point Core3 should be fully built. 

# Section 3. Setting up MYSQL, configuring Core3, and running the server

*3.1 MYSQL database setup

Execute the following commands in the terminal:
	
	mysql -u root -p
	source /home/swgemu/Git/Core3/MMOCoreORB/sql/swgemu.sql;
	source /home/swgemu/Git/Core3/MMOCoreORB/sql/updates/	deletedcharacters_add_dbdeleted.sql;
	source /home/swgemu/Git/Core3/MMOCoreORB/sql/updates/account_ips.sql;
	CREATE USER 'YOUR DB USERNAME'@'localhost' IDENTIFIED BY 'YOUR DB PASSWORD';
	GRANT ALL PRIVILEGES ON swgemu.* TO 'YOUR DB USERNAME'@'localhost';
	FLUSH PRIVILEGES;
	use swgemu;
	UPDATE galaxy SET galaxy_id='YOUR GALAXY ID', name='YOUR SERVER NAME', address='YOUR IP' WHERE galaxy_id=2;

*3.2 Configure Core3

	Open /home/swgemu/Git/MMOCoreORB/bin/config/config.lua.
	Inside config.lua, edit the config values to match your settings. (Database Information, TRE file location, and other desired server settings.)

*3.3 Running the Core3 Server

Execute the following commands in the terminal:
	
	cd /home/swgemu/Git/MMOCoreORB/bin
	./core3

Congratulations! At this point you should have a running SWGEmu Core3 server.
