KevScript and Runtime Adaptations
---------------

### Objectives
In this practice, you will learn how to use Kevoree Script (a.k.a. KevScript) to edit your models at both design time and run time.     
You will also see how to launch a Kevoree runtime with a specific configuration (bootstrap) and how KevScript can be used to program self-adaptations in software systems.


### Setting up your environment
For this practice, you only need to have the ProducerConsumer Sample project. All other components used will be collected from the *Toy* library.    
Obviously, you'll need a Kevoree Runtime, a Kevoree Editor, an IDE and Maven installed.

> [ProducerConsumer Sample >](https://github.com/kevoree/kevoree-samples/releases)     
> 
> [Kevoree Downloads >](http://kevoree.org/download.html)


Edit a model with KevScript
---------------
First of all, here is a pointer to the [documentation of KevScript](http://kevoree.org/doc/#kevoree-script-aka-kevscript). It describes the commands, how to use them and gives examples.

> [KevScript Doc >](http://kevoree.org/doc/#kevoree-script-aka-kevscript)   

First let see what a complete KevScript looks like.    
Open a Kevoree Editor and do again the Chat application (see [Level 0](http://kevoree.org/practices/level0/)).    
Once your model is ready (no need to push to the platform), click on the **KevScript** icon of the editor. It should open a panel at the bottom of the frame. Here, click on    
`Load Current Model`    
You should see, in the bottom panel, the KevScript to execute in order to create the model you see. As a proof, clear the model (`Model / Clear`), and click on *Execute* in the bottom panel. You should see you model disapear and apear again.

Now, from this model I want you to add a *Ticker* component and connect it to the existing channels.   
Copy/paste the script in a text editor to keep it safe.    
Clear the script (not the model).   
Create the script to add an instance of *Ticker* and connect it to a channel.    
Test your script by executing.    
Sould you fail, clear the model, copy/paste the previous script and execute it to get back the base model.

Launch a Runtime with a specific configuration
---------------

KevScript can be used to drive the start of a Kevoree Runtime, so that your Runtime starts in a configuration that suits to you.    
To use this ability, you just need to have the Kevoree Maven plugin in your POM/project, and place the script to execute in    
`src/main/kevs/main.kevs`     
Then, just call the kev:run goal of the Maven plugin.    
As an example, you can see how it is done in the ProducerConsumer sample.

Now I want you to create a project, with only the Kevoree plugin, and put a script to start the chat.



How to use KevScript to make runtime system adaptations ?
---------------

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

```
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

