Make your own Channel
---------------

### Objectives
This practice aims at making you familiar with the Kevoree compilation chain and the Design of new Channel. To this end, you will make use of the Kevoree Maven plugin to compile a sample  channel. We suppose that you already do the [level 0](http://kevoree.org/practices/level0/) and [level 1](http://kevoree.org/practices/level1/).

### Setting up your environment
First of all, you need to have a `JRE 1.7` at least.    
Make sure you have a running installation of [Apache Maven 3](http://maven.apache.org/download.cgi) installed. Check it out by opening a console and typing `mvn -version`. Otherwise follow the Apache instructions.    
For the Java development, we would suggest using [IntelliJ](http://www.jetbrains.com/idea/download/index.html) or [Eclipse](https://eclipse.org), because we provide now plugin for these IDEs.  (See here to install the [eclipse plugin](https://github.com/kevoree/kevoree-eclipse-plugin/))


> [Apache Maven 3 >](http://maven.apache.org/download.cgi)    


Create a new Kevoree project
---------------
From your IDE,  File -> new Kevoree project
Create a new Kevoree Channel,  File -> new Kevoree channel (Choose a Name and a Java Package for your example) for Example MyFirstChannel


Compile with Maven
---------------

Check your Internet connection is on. On its first launch, Maven may need to download several plugins and artifacts from the Internet. It looks like it downloads the entire world... that’s true, but don’t worry, this world is finite,.. more or less.   
Open a terminal, cd into the unzipped folder, and launch the installation of the artifact on the local repository of the system: mvn install.    
On the first launch, it may take up to 3 minutes (according to the load of the network). The mvn install command first executes the Kevoree Annotation Plugin. Basically, this plugin 
extracts models of components/channels/groups from their source code. Then, the code is compiled and packaged in a Jar.
The outcome of this command can be found under the target folder created in the same folder as the pom file.   
In this folder, you can find the generated classes, the model extracted from your components (generated-sources/kevoree/KEV-INF/lib.kev). Both the model and compiled classes has been packaged in the Jar file at the root of the target folder.   
Also a copy of this Jar has been placed in your local Maven repository (usually user.home/.m2/repository).

>In a console   
***************
```
cd yourprojectName
mvn install
```


What did we do?
---------------

Now it is time to go a bit deeper in the code.   

### The channels

Have a look in the `src/main/java` folder. Here is the code of the channel we just compiled. 

```
package org.kevoree;


import org.kevoree.annotation.KevoreeInject;
import org.kevoree.annotation.Library;
import org.kevoree.annotation.ChannelType;
import org.kevoree.api.Callback;
import org.kevoree.api.ChannelContext;
import org.kevoree.api.ChannelDispatch;
import org.kevoree.api.Port;

@ChannelType
@Library(name = "Java")
public class MyFirstChannel implements ChannelDispatch {

    @KevoreeInject
    ChannelContext channelContext;

    @Override
    public void dispatch(final Object payload, final Callback callback) {
        for (Port p : channelContext.getLocalPorts()) {
            p.call(payload, callback);
        }
	}
}    

```

The channel context gives you access to the model. The dispatch method is called automatically when a message is received by one of the channel fragment. You must have in mind that this channel is instantiated for any node on which bound component are deployed. 


### The POM

Open now the pom.xml file. This file is the configuration file for Maven executions.
At top, the Identity section provides information about the group, unique name, display name and version of the artifact.   

This POM declares two dependencies, mainly the Kevoree Annotation API (for component specification) and Kevoree API (for model manipulation).   
The Build section specify which plugins must be executed at which phase of the compilation process. The Kevoree Annotation plugin registers to the *prepare-package* phase of the maven process, and will execute its *generate* goal during this phase. This goal extracts the Kevoree artefact (channel, component groups)’ model and places it into a proper location for it to be embedded within the Jar file.

```
        <dependency>
            <groupId>org.kevoree</groupId>
            <artifactId>org.kevoree.annotation.api</artifactId>
            <version>${kevoree.version}</version>
        </dependency>
        <dependency>
            <groupId>org.kevoree</groupId>
            <artifactId>org.kevoree.api</artifactId>
            <version>${kevoree.version}</version>
        </dependency>
....
	<build>
		<plugins>
		      <plugin>
                <groupId>org.kevoree.tools</groupId>
                <artifactId>org.kevoree.tools.mavenplugin</artifactId>
                <version>${kevoree.version}</version>
                <extensions>true</extensions>
                <executions>
                    <execution>
                        <goals>
                            <goal>generate</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <nodename>node0</nodename>
                    <model>src/main/kevs/main.kevs</model>
                </configuration>
            </plugin>
		<plugin>
			<artifactId>maven-compiler-plugin</artifactId>
			<version>3.0</version>
			<configuration>
				<source>1.5</source>
				<target>1.5</target>
			</configuration>
		</plugin>
		</plugins>
	</build>


```


### Run it !
Launch a runtime, and open an editor.   
Open the model from the runtime you just launched, and add the *Toy* library.   
Import your channel in the editor: `Model / Load Library` and select the Jar file that have been created in the *target* folder or the Sample Project.   
You should now see the your channel. Deploy one instance of each, and connect then together with a channel.   
Push to the node(runtime).


This first channel is synchronized and not distributed.

Do It Yourself  (easy)
---------------


Now, you have in hands all you need to make your own channels.
Try to build a first asynchronous channel. Create a new Channel in your IDE. 


The first idea is to ensure that a call to a channel does not block the caller component behavior. 

We propose to build an Asynchronous channel. Create a new channel. This channel must create a thread when it receives the dispatch call.


```
...
   ExecutorService executor = null;
   @Start
    public void start() {
        executor = Executors.newSingleThreadExecutor();
    }
    public void dispatch(final Object payload,final Callback callback) {
        executor.submit(new Runnable() {
            @Override
            public void run() {
                for (Port p : channelContext.getLocalPorts()) {
                        p.call(payload,callback);
                    }
                }
            }
        });
    }

```

Compile it and try it within the editor. 


Do It Yourself (autonomous)
---------------


Build a third channel which is a simple distributed channel that JSON RPC. 

You can be inspired by https://github.com/kevoree/kevoree-library/blob/master/java/org.kevoree.library.java.hazelcast/src/main/java/org/kevoree/library/java/hazelcast/DistributedBroadcast.java






