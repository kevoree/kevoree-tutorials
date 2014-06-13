# Cloud nodes

First of all, you should be confident in how to create virtual machines in Kevoree framework. This is performed through the creation of child nodes and the attachement of such node to a container. By this encapsulation we can mimic the fonctionnality of a cloud which define a infrastructure level (nodes hosting only nodes) and a platform level (nodes which contains at least one component).

First of all, start the runtime of your choice. Then open a Kevoree Editor an load the current model of the runtime. Find below main steps:

* Load the model from your node : `File / Load model from node`
* Load the Cloud Web library through : `Model / Load Library / Cloud / org.kevoree.library.cloud.web`
* Drag and drop a WebFrontend component in your node
* Deploy the new model on your node : `click on node` then `click button push`

Your model should look like the following picture.

 [Figure 1: The Kevoree Cloud web frontend](id:fig-runtime)
 <img src="https://raw.githubusercontent.com/kevoree/kevoree-tutorials/master/level4/img/cloudFrontend.png" width="100%"/>

You should see a message : `Update sucessfully completed` in your runtime.

>Open a browser, a type the following url
***************
```
http://localhost:8080
```

You are now visualizing a web interface dedicated for Cloud node management. It is simply a strict vizualization of the current model and each time a modification is performed, the modified model is send to the platform to application.

***Add a child node from the web interface***
The *add default* button allows you to quicly add a child node to the current platform hosting the web interface. Because you certainly start your container as a JavaNode (by default), the child node will run in a separated Java virtual machine. As a reminder Kevoree node type (e.g. JavaNode) defines the kind of virtualization strategy to adopt for child node isolation. We offer extactly the same API for concret hypervisor like LXC, Docker, KVM, Amazon EC2,...

After adding a new node you can redo the step `open from node` on editor and observe that the current model reflects the augmented set of nodes.

***Add a child node from KevScript***
Similarly you can now modify the model from the editor, open the KevScript panel and type

```
add node0.newKChild : JavaNode
```

or simply drag and drop a JavaNode inside the node0 and add a HelloJava component for instance.

Then execute and push your model to the platform, you will observe the creation of a node and the start of the hosted component.
