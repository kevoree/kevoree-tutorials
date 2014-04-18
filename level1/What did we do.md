# What did we do?

Now it is time to go a bit deeper in the code.   
Open IntelliJ :-). Then File / OpenProject and select the POM file in the sample project folder.

## The components

Have a look in the `src/main/java` folder. Here is the code of the components we just compiled. As you can imagine, these components implement a Producer/Consumer example.   
The HelloProducerThread is a utility class that produces HelloWorld messages regularly. The two components (in Kevoree terms) are those called *Component*.   
Open the consumer. This rather simple component just displays on the console what it receives on the ”consumeHello” port (see the *consumeHello* method).   
Open the producer. This slightly more complex component creates a HelloProducer thread on start, and registers a listener (Observer pattern) (see *helloProduced* method). Each time a message is produced by the thread, the listener is called, and the message is sent through the ”helloProducedPort” outputPort. Also, notice the delay between two messages, set by a property of the component.

## The POM

Open now the pom.xml file. This file is the configuration file for Maven executions.
At top, the Identity section provides information about the group, unique name, display name and version of the artifact.   
In our sample, we inherit some of these information (groupId, version) from a *parent* artefact.    
This POM declares no specific *dependencies*, because all the libraries necessary for this project are inherited from the parent, mainly the Kevoree Annotation API (for component description) and probably a Logger.   
The Build section specify which plugins must be executed at which phase of the compilation process. The Kevoree Annotation plugin registers to the *prepare-package* phase of the maven process, and will execute its *generate* goal during this phase. This goal extracts the Kevoree components’ model and places it into a proper location for it to be embedded within the Jar file.


## Run it !
Launch a runtime, and open an editor.   
Open the model from the runtime you just launched, and add the *Channels* library.   
Import your components in the editor: `Model / Load Library` and select the Jar file that have been created in the *target* folder or the Sample Project.   
You should now see the Producer and Consumer components. Deploy one instance of each, and connect then together with a channel.   
Push to the node(runtime) and check out the console of the runtime.   
If you wanna play, you can change the delay of 'hello generation' on the producer.