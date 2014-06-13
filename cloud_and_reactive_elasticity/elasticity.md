# Elasticity

In this last section, you will extend the step 3 of level 3. As a reminder, this previous work aimed at deploying a Scaler component which manage the number of Web server replicat inside a node. Replicat is then accessible behind a load balancer which balance the load using a round robin strategy. The current step simply aims at performing a similar process but in addition you need to **isolate** each web server in a **dedicated child node**. Finally for stronger developpers you can extends this cloud scaler manager with a property wich dynamically choose to put several instances on the same nodes.

#### Scaling Web services using child nodes

The easiest initial step is to use the CloudScaler sample project (github kevoree-samples).
Here is the following steps :

* Open in the IDE of your choice the Scaler sample project.
* Extend the reaction of add and remove nodes if necessary with a child node step and an attachement of the new components to this nodes. As a reminder to add a node you should use the following KevScript instruction : `add parent.child : JavaNode` , similarly to attach the  BlogServer to a child node simply use `add child.componentName : BlogServer`.
* Start a runtime and deploy an instance of your scaler inside the root `node0` (or use the kev:run technics for similar behavior).
* Use the editor to change the number of needed instance of Web server
* Test an play with it :-)

#### Dynamic reallocation of WebServers

Indeed isolate each WebServer in a separated virtual machine is costly. Why not being more flexible and allow to add a number of maximum WebServer to run on the same virtual machine ?

* Add a dynamic param to your scaler which will be ne number of maximum WebServer which can be host on the same virtual machine
* In the update method (called when you will update this param), define a code to move WebServer components over the limit in other containers. As a reminder you should use the `move` instruction of KevScript `move child3.web3 child4`.
* Use the same testing strategy than the previous step
* Use the editor to make vary the parameter, you should observe node and components moving.

That's all folks ! We hope that you enjoy developping using Kevoree, now you have every tools to define you own complex dynamic system using Model@Run.time concepts. Don't hesitate to contact the Kevoree team by mail or github if you have any question or issue.
