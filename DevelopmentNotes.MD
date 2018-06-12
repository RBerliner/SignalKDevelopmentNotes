##Debug SignalK with Eclipse

Import projects into workspace. (File > Import)
	Select Maven, Existing Maven Project, Next
	Select the pom and Add project to working set, Finish.


##Building project in terminal

Open Terminal in signalk-core-java
rberliner\@BigIA:\~/Dropbox/freeboard/signalk-core-java\$ mvn install

Open Terminal in signalk-server-java
rberliner\@BigIA:\~/Dropbox/freeboard/signalk-server-java\$ mvn -fpomDev.xml Dmaven.test.skip=true install

pomDev.xml is a modified form of the standard pom with the dev profile
as the default. As written, this skips the tests.

Open a third terminal in freeboard-sk, delete bundle.js and run npm start.

Npm start watches for changes in the js files and regenerates bundle.js when necessary.


rberliner\@BigIA:\~/Dropbox/SignalK/signalk-java/signalk-static/freeboard-sk\$npm start


\> freeboardk\@0.0.1 start /home/rberliner/Dropbox/SignalK/signalk-java/signalk-static/freeboard-sk

\> watchify index.js \--exclude mdns \--ignore bufferutil \--ignore utf-8-validate \--outfile bundle.js

The program can be run by opening a terminal in signalk-java

<rberliner@BigIA>:\~/Documents/FreeboardProjects/signalk-java:~\$ mvn -Pdev exec:java

To run the program from a terminal and have it continue to execute when
the terminal is closed:


rberliner@BigIA>:\~/Documents/FreeboardProjects/signalk-java:~\$ nohup mvn -Pdev exec:java &


It may be necessary to delete signalk-java/conf/self.json,
signalk-java/conf/signalk-config.json and
signalk-java/conf/resources.json **before starting**  to get a clean
start.

