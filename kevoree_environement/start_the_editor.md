# Start the editor

Launch the `Editor` (if not already done).
You should get the window presented in [Figure 2](#fig-editor) (without content for the moment because your model is empty).
On the *left hand side*, the **library of available component types**. You should have nothing in your editor for the moment, that's ok. We will get some component definitions from existing libraries.
*On top*, several icons open different panels displaying logs, errors or the Kevoree scripting panel.
*On the center*, the model edition space.
Here we go. Let first collect the current model of the runtime we just started. In the editor,
`File / Open From Node`
By default, the `IP:Port` value is set to collect the model from a group running on the localhost, accessible trough the 9000 port. If you changed the values when you started the runtime, then you have to change this value. Otherwise, proceed.
The Editor will then get the current model of the runtime, and display it. Once this operation realized, you should see the synchronization group called *sync* (in green), a node called ’node0’ as specified in the runtime startup window, and a green link that indicates that the node0 is part of the *sync* group.
In the editor, save the model in XMI then in JSON format, and have a look at these files. This is actually what the runtime and the editor are exchanging.
Ok, you’re ready to create your chat application.

[Figure 2: The Kevoree Java Editor](id:fig-runtime)
<img src="https://raw.githubusercontent.com/kevoree/kevoree-tutorials/master/level0/img/editor.png" width="80%"/>
