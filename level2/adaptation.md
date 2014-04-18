# First adaptation : How to use KevScript to make runtime system adaptations ?

The principle of runtime adaptations is:    
**Get** the current model    
**Clone** the model to get a modifiable one    
**Update** this model to the new configuration you want    
**Deploy**: Ask the runtime for an adaptation to this new model.    
I would like you to create a component called "TickStarter".   
The idea is to start a runtime with a chat application ready, PLUS one instance of this "TickStarter".    
This "TickStarter" component should display a JFrame, with two JButtons **on** and **off**.
On action on **on** you should execute a KevScript to dynamically add a "Ticker" instance and link it to the consoles.    
As you can guess, an action on **off** would remove this instance and its connections to any channel.   
To help you, here is the code to make an adaptation at runtime.

```java
//Init the variables (from inside a component)
private ModelCloner cloner = new DefaultModelCloner();

@KevoreeInject
private KevScriptService kevScriptService;

@KevoreeInject
private ModelService modelService;

//Get the current Model
UUIDModel model = modelService.getCurrentModel(); 

// Clone the model to make it changeable
ContainerRoot localModel = cloner.clone(model.getModel());

// create the KevScript to execute
String addCompScript = "<PUT_YOUR_SCRIPT_HERE>";

// Apply the script on the current model, to get a new configuration
kevScriptService.execute(addCompScript, localModel); 

//Ask the platform to apply the new model; register an optional callback to know when the adaptation is finised.
modelService.update(localModel, new UpdateCallback() {
	public void run(Boolean aBoolean) {
		//Model update finished. May do something :-), or not
	}
}
```

