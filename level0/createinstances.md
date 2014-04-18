# Create instances

Drag&Drop a component called ”ToyConsole”, two times, from the library to the `node0`. Doing that, you will create two instances of the ToyConsole component type in the model we previously got from the runtime. The actual creation of ToyConsole instances is made by the runtime, in order to fit the new model it receives. Click on the node, and hit the `Push` button at the bottom of the node property windows that shows-up.   
This action pushes the modifier model to the runtime, and you should see the two instances of the ToyConsole component created.    
Now you should have a new window with two tabs. Each tab is an instance of the ToyConsole component. They have been automatically grouped in a single window.    
These consoles are functional (you can type in text), but connected to nothing, so the communication between the two ToyConsole instances is not working. Also, the consoles have generated names, so we may change them.   
Come back in the Editor, and change the names of the consoles’ instances in their properties window (click on the instance).    

[Figure 3: Adding two consoles](id:fig-consoles)
<img src="https://raw.githubusercontent.com/kevoree/kevoree-tutorials/master/level0/img/consoles.png" width="80%"/>