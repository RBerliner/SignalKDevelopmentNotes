##Developing SignalK 

These notes may help others to start working on SignalK themselves – there is a bit of a learning curve with servers, maven, git, github.... These instructions were prepared for Ubuntu-linux but can probably be applied to Windows with some adjustments.

signalk-java is the java form of the system and it is contained in 4 projects (repositories) on github and that can be found at https://github.com/SignalK

## Install the Tools ##


###Install git.  
```
$ sudo apt-get update  
$ sudo apt-get install git
$ git –version  
git version 2.7.4  
```


###Install maven.  
```
$ sudo apt-get install maven  
$ mvn -version
Apache Maven 3.3.9   
Maven home: /usr/share/maven   
Java version: 1.8.0_111, vendor: Oracle Corporation   
Java home: /usr/lib/jvm/java-8-oracle/jre   
Default locale: en_US, platform encoding: UTF-8   
OS name: "linux", version: "4.4.0-71-generic", arch: "amd64", family: "unix"  
```

## Create the local repositories. ##

1. Start by creating a directory SignalK. Open the SignalK directory in the Terminal.  
2. In any browser, go to https://github.com/SignalK  
3. Once you are there you will be faced with a number of different repositories. Too many to understand all at one time. Select the signalk-core-java repo.
4. On the right hand side of the page there will be a green box. When you click the box, the Clone with HTTPS box will open. Click on the clipboard icon to copy the address to the clipboard.
5. In the terminal type clone and then paste in the repo address. You will get a line:
    
    ```
    :~/SignalK$ clone https://github.com/SignalK/signalk-core-java.git https://github.com/SignalK/signalk-core-java.git
    ```
    
6. Type return. This will provide you with your own local signalk-core-java repo. 
7. In the SignalK directory, in the terminal again, do the same thing for the signalk-server-java repo from github and for the signalk-java repo.

You will now have a directory, SignalK, containing the three local repositories:
    
>SignalK/  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; signalk-core-java  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; signalk-server-java  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; signalk-java  
    
Open a terminal in ~SignalK/signalk-java/signal-static. In github, find the freeboard-sk repo and clone it so that the freeboard-sk repo exists in your SignalK/signalk-java/signalk-static directory.

##Building project in terminal  
  
1. Open Terminal in signalk-core-java and do a mvn install (adjusted for your directory location).  
  
    ```
    :~/Documents/SignalK/signalk-core-java$ mvn install      
    ```  
  
2. Open Terminal in signalk-server-java and do maven install with the indicated options.  
The -Dsignalk.build=dev instructs maven to use the development build and not to download the build from the net.  
The -Dmaven.test.skip=true causes the tests to be skipped (they take a long time).  
    ```
    :~/Documents/SignalK/signalk-server-java$ mvn -Dsignalk.build=dev install -Dmaven.test.skip=true.  
    ```  
3. Open a third terminal in freeboard-sk, and run npm install.  
The first time you run nom install, it will download a large number of javascript packages and the process will take a long time. Since I have run it before, it now does very little.
    
    ```
    :~/Documents/SignalK/signalk-java/signalk-static/freeboard-sk$ npm install  
    ```
    
     Delete bundle.js and then run npm start.  
    

4. Then execute npm start.  
```:~/Documents/SignalK/signalk-java/signalk-static/freeboard-sk$ npm start```  
```> @signalk/freeboard-sk@0.0.4 start /home/rberliner/Documents/SignalK/signalk-java/signalk-static/freeboard-sk```  
```> watchify index.js --exclude mdns --ignore bufferutil --ignore utf-8-validate --outfile bundle.js```  
  
Now any changes in the freeboard-sk source js files will cause  bundle.js to be regenerated. The file bundle.js is the minified code for freeboard-sk including all of its js dependencies. Changes in bundle.js may not be reflected in your browser rendition of freeboard unless you clear the browser cached files (In Chrome it is MoreTools > Clear Browsing Data, select cached images and files.)  
  
npm start runs watchify which looks for changes in the js files and regenerates bundle.js when necessary.  
  
The program can be run by opening a terminal in signalk-java.  
  
```:~/Documents/SignalK/signalk-java$ mvn -Dsignalk.build=dev exec:java```  
  
To run the program from a terminal and have it continue to execute when the terminal is closed:  
  
```rberliner@BigIA:~/Documents/SignalK/signalk-java$ nohup mvn -Dsignalk.build=dev exec:java &```  
  
It may be necessary to delete signalk-java/conf/self.json,  
signalk-java/conf/signalk-config.json and  
signalk-java/conf/resources.json **before starting**  to get a clean start.  

##Debug SignalK with Eclipse  
  
Import projects into workspace. (File > Import)  
  
Select Maven, Existing Maven Project,  
  
Next Select the pom and Add project to working set, Finish.  

##Run and Debug SignalK using NetBeans

