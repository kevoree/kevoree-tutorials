# Port with Callback

In the previous example, the producer do not require any answer from the consumers. Thus Messge-Oriented communications (one-way Input-Output) is a good solution. However, some components may need to get an answer, a result from other components.    
In this case, you may use the mechanism of Callback. To illustrate this mechanism, checkout the Frame and Popup components.    
Basically, the frame displays a prompt line and a button. On click, what has been entered in the line is sent through the *textEntered* port, and a callback method is created to specify the actions to take when an answer is received.   
On its side, the Popup component will simply display the message received and ask for an answer.    

Deploy and instance of each and checkout their behavior.
