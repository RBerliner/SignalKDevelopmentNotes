##Debug SignalK with Eclipse  
  
Import projects into workspace. (File > Import)  
  
Select Maven, Existing Maven Project,  
  
Next Select the pom and Add project to working set, Finish.  
  
  
##Building project in terminal  
  
Open Terminal in signalk-core-java and do a mvn install (adjusted for your directory location).  
  
```
rberliner\@BigIA:rberliner@BigIA:~/Documents/SignalK/signalk-core-java$ mvn install      
[INFO] Scanning for projects...      
[INFO]                                                                           
[INFO] ------------------------------------------------------------------------  
[INFO] Building signalk-core-java 0.0.1-SNAPSHOT    
[INFO] ------------------------------------------------------------------------  
[INFO]  
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ signalk-core-java ---    
[INFO] Using 'UTF-8' encoding to copy filtered resources.    
[INFO] Copying 2 resources    
[INFO]    
[INFO] --- maven-compiler-plugin:3.0:compile (default-compile) @ signalk-core-java ---    
[INFO] Nothing to compile - all classes are up to date    
[INFO]    
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ signalk-core-java ---  
[INFO] Using 'UTF-8' encoding to copy filtered resources.  
[INFO] Copying 9 resources  
.  
.  
. .......Many lines deleted  
.  
.  
Tests run: 123, Failures: 0, Errors: 0, Skipped: 3  
  
[INFO]  
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ signalk-core-java ---  
[INFO] Building jar: /home/rberliner/Documents/SignalK/signalk-core-java/target/signalk-core-java-0.0.1-SNAPSHOT.jar  
[INFO]  
[INFO] --- maven-install-plugin:2.5.2:install (default-install) @ signalk-core-java ---    
[INFO] Installing   /home/rberliner/Documents/SignalK/signalk-core-java/target/signalk-core-java-0.0.1-SNAPSHOT.jar to   /home/rberliner/.m2/repository/nz/co/fortytwo/signalk/core/signalk-core-java/0.0.1-SNAPSHOT/signalk-core-java-0.0.1-SNAPSHOT.jar    
[INFO] Installing /home/rberliner/Documents/SignalK/signalk-core-java/pom.xml to /home/rberliner/.m2/repository/nz/co/fortytwo/signalk/core/signalk-core-java/0.0.1-SNAPSHOT/signalk-core-java-0.0.1-SNAPSHOT.pom    
[INFO] ------------------------------------------------------------------------    
[INFO] BUILD SUCCESS    
[INFO] ------------------------------------------------------------------------    
[INFO] Total time: 8.782 s    
[INFO] Finished at: 2018-07-02T20:41:27-04:00    
[INFO] Final Memory: 11M/92M    
```  
  
Open Terminal in signalk-server-java and do maven install with the indicated options.  
The -Dsignalk.build=dev instructs maven to use the development build and not to download the build from the net.  
The -Dmaven.test.skip=true causes the tests to be skipped (they take a long time).  
```
rberliner@BigIA:~/Documents/SignalK/signalk-server-java$ mvn -Dsignalk.build=dev install -Dmaven.test.skip=true.  
[INFO] Scanning for projects...  
  
[INFO]                                                                           
[INFO] ------------------------------------------------------------------------  
[INFO] Building signalk-server-java 0.0.1-SNAPSHOT  
[INFO] ------------------------------------------------------------------------  
[INFO]  
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ signalk-server-java ---  
[INFO] Using 'UTF-8' encoding to copy filtered resources.  
[INFO] Copying 4 resources  
.  
.  
. ... Many lines skipped  
.  
.  
[INFO]  
[INFO] --- maven-install-plugin:2.5.2:install (default-install) @ signalk-server-java ---  
[INFO] Installing /home/rberliner/Documents/SignalK/signalk-server-java/target/signalk-server-java-0.0.1-SNAPSHOT.jar to /home/rberliner/.m2/repository/nz/co/fortytwo/signalk/server/signalk-server-java/0.0.1-SNAPSHOT/signalk-server-java-0.0.1-SNAPSHOT.jar  
[INFO] Installing /home/rberliner/Documents/SignalK/signalk-server-java/pom.xml to /home/rberliner/.m2/repository/nz/co/fortytwo/signalk/server/signalk-server-java/0.0.1-SNAPSHOT/signalk-server-java-0.0.1-SNAPSHOT.pom  
[INFO] Installing /home/rberliner/Documents/SignalK/signalk-server-java/target/signalk-server-java-0.0.1-SNAPSHOT-jar-with-dependencies.jar to /home/rberliner/.m2/repository/nz/co/fortytwo/signalk/server/signalk-server-java/0.0.1-SNAPSHOT/signalk-server-java-0.0.1-SNAPSHOT-jar-with-dependencies.jar  
[INFO] ------------------------------------------------------------------------  
[INFO] BUILD SUCCESS  
[INFO] ------------------------------------------------------------------------  
[INFO] Total time: 24.448 s  
[INFO] Finished at: 2018-07-02T20:49:36-04:00  
[INFO] Final Memory: 56M/719M  
[INFO] ------------------------------------------------------------------------  
```
Open a third terminal in freeboard-sk, and run npm install.  
The first time you run nom install, it will download a large number of javascript packages and the process will take a long time. Since I have run it before, it now does very little.  
  
rberliner@BigIA:~/Documents/SignalK/signalk-java/signalk-static/freeboard-sk$ npm install  
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@^1.0.0 (node_modules/chokidar/node_modules/fsevents):  
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.4: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})  
npm WARN @signalk/freeboard-sk@0.0.4 No repository field.  
npm WARN @signalk/freeboard-sk@0.0.4 license should be a valid SPDX license expression  
  
Delete bundle.js and then run npm start.  
```rberliner@BigIA:~/Documents/SignalK/signalk-java/signalk-static/freeboard-sk$ npm start```    
```> @signalk/freeboard-sk@0.0.4 start /home/rberliner/Documents/SignalK/signalk-java/signalk-static/freeboard-sk```  
```> watchify index.js --exclude mdns --ignore bufferutil --ignore utf-8-validate --outfile bundle.js  
```   
  
Now any changes in the freeboard-sk source js files will cause  bundle.js to be regenerated. The file bundle.js is the minified code for freeboard-sk including all of its js dependencies. Changes in bundle.js may not be reflected in your browser rendition of freeboard unless you clear the browser cached files (In Chrome it is MoreTools > Clear Browsing Data, select cached images and files.)  
  
Npm start watches for changes in the js files and regenerates bundle.js when necessary.  
  
The program can be run by opening a terminal in signalk-java.  
  
```rberliner@BigIA:~/Documents/SignalK/signalk-java$ mvn -Dsignalk.build=dev exec:java```  
  
To run the program from a terminal and have it continue to execute when the terminal is closed:  
  
```rberliner@BigIA:~/Documents/SignalK/signalk-java$ nohup mvn -Dsignalk.build=dev exec:java &```  
  
It may be necessary to delete signalk-java/conf/self.json,  
signalk-java/conf/signalk-config.json and  
signalk-java/conf/resources.json **before starting**  to get a clean start.  
