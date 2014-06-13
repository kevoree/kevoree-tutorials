# WebServer Scaler

#### Understand the mapping WebServer <=> Component

For sake of simplicity, this practice uses a simple mapping:     
*a component instance == a web server instance*.    
This means, each web server (i.e.: component instance) uses its own http port.    
A webserver component can serve static content, or dynamic content using data received on `inputPort`.

### Play with the toys

As a first step you can play with the Web toy library included in kevoree.

* Start a runtime and an editor (load from node)
* Load web library (for instance type `include mvn:org.kevoree.library.java:org.kevoree.library.java.web:RELEASE` in the KevScript panel of editor)
* Drag and drop a NanoBlogServer component
* Configure the http_port property for `8080`
* Push your model to a runtime
* Open a browser to `http://localhost:8080`
* You should see a `hello world` page.

As a second step you can try the dynamic content update

* Drag an drop an instance of BufferPage
* Configure its http_port property for `8081`
* Load toys library (for instance type `include mvn:org.kevoree.library.java:org.kevoree.library.java.toys:RELEASE` in the KevScript panel of editor)
* Load channels library (for instance type `include mvn:org.kevoree.library.java:org.kevoree.library.java.channels:RELEASE` in the KevScript panel of editor)
* Create a `SyncBroadcast` channel
* Create a ticker component (set property random to `true` by clicking on the component in editor)
* Bind the ticker port and input port of both new component to channel, your model should look like the figure 1.

> [Figure 1: Kevoree Web servers first toys](id:fig-webtoys)
> <img src="https://raw.githubusercontent.com/kevoree/kevoree-tutorials/master/level3/img/webtoys.png" width="100%"/>

* Push your model
* Open a browser an naviguate `http://localhost:8081` , you normally observe a web page displaying the content of the data pushed by the ticker. This illustrates how we use Kevoree to display data from sensors for instance.

### Web elastic manager

In order to reply to an increasing load, web instratructures commonly use load balancers as front end and several web servers in back-ends. Due to the variation of the load, the number of backend required at a time to ensure a satisfactory quality of service vary.    
In this last step, we build a component which aims at autonomously scale the back-end servers (add and remove back-ends) according to the load.    

<span class="warning-bloc"><span class="fa fa-exclamation-triangle fa-lg orange"></span> The load balancer component works on Unix and OSX operating systems only.   

For Windows users, please comment the corresponding line in   
`src/main/kevs/main.kevs` : `add node0.lb : HAProxy`
You will not have the load balancer page, but still you can execute the scaler component and observe result in the console</span>

Hands on !

* Open the **Scaler** sample project in your IDE.
* You'll find a `src/main/kevs/main.kevs` which corresponds to the initial model
* The `Scaler.java` has to be completed. Localize the two `TODO` and replace by a call of the kevScript engine with a `add hostName.replaceByComponentName : NanoBlogServer` and `remove hostName.replaceByComponentName`.
* Compile the code with `mvn clean install`
* Run the sample (`mvn kev:run`)
* Open a browser to `http://localhost:8070` (login/mdp : kev/kev). Now you can access to the load balancer web admin page. Notice the list of backends corresponds exactly to the number of BlogServer components deployed.
* Open a browser an naviguate `http://localhost:8080` , you normally observe that the load balancer dispatches you to one or another BlogServer.
* Open the model from the node `File / Open from node`
* Modify the parameter of the scaler
* Refresh the page of the Load balancer