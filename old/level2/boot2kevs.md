# Boot2Kevs : Launch a Runtime with a specific configuration

KevScript can be used to drive the start of a Kevoree Runtime, so that your Runtime starts in a configuration that suits to you.    
To use this ability, you just need to have the Kevoree Maven plugin in your POM/project, and place the script to execute in    
`src/main/kevs/main.kevs`     
Then, just call the kev:run goal of the Maven plugin.    
As an example, you can see how it is done in the ProducerConsumer sample.

Now I want you to create a project, with only the Kevoree plugin, and put a script to start the chat.
