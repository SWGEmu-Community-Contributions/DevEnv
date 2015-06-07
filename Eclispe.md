# Eclipse Upgrade
**************************************************************************************

***How to Upgrade Eclipse on the Development VM***

	***Thanks Valkyra***

Close Eclipse. Download http://www.eclipse.org/downloads/dow...PACKAGENAME.tar.gz to ~/Downloads

Start a console session and type the below commands one after each other;

	cd Downloads
	tar -xvf eclipse-cpp-PACKAGENAME.tar.gz
	mv ../eclipse ../eclipse-old
	mv ./eclipse ../eclipse

Now open eclipse again as normal and select workspace will come up, just choose 'OK'

Right click on the Project MMOCorb-Testing and select 'properties'
Add the c++ include paths as shown in the linked image

http://i.imgur.com/N4rq7jb.png

Then add the pre-processor macro as shown in

http://i.imgur.com/k2CMtHM.jpg

Click OK and then Apply

Once added, select the project again and right click, then index/rebuild (may take a while)

Close Eclipse and then re-open it, Carry on working as normal but with the newer version

***********************************************************************************************
