# Compile with Maven

Check your Internet connection is on.
On its first launch, Maven may need to download several plugins and artifacts from the Internet. It looks like it downloads the entire world... that’s true, but don’t worry, this world is finite,... more or less.   

Open a terminal, cd into the unzipped folder, and launch the installation of the artifact on the local repository of the system: `mvn install`.    

On the first launch, it may take up to 3 minutes (according to the load of the network). The mvn install command first executes the Kevoree Annotation Plugin. Basically, this plugin    
1. extracts models of components from their source code
2. generates some classes necessary for the runtime (mostly proxy classes). Then, the code is compiled and packaged in a Jar.

The outcome of this command can be found under the target folder created in the same folder as the pom file.   
In this folder, you can find the generated classes, the model extracted from your components (generated-sources/kevoree/KEV-INF/lib.kev). Both the model and compiled classes has been packaged in the Jar file at the root of the target folder.

Also a copy of this Jar has been placed in your local Maven repository (usually user.home/.m2/repository).

```
cd org.kevoree.library.java.producerconsumer
mvn install
```
