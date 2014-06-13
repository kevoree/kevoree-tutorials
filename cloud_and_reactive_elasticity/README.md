# Cloud and reactive elasticity

This last practice level introduces the Cloud aspect of Kevoree framework.
In previous levels, you have edited and played with components, channels, and learnt how to manipulate models and the underlying system using the KevScript DSL.
This practice extends the *Level 3* (which defines elasticity mechanism for WebServers, on a single machine) to allow you to build your own cloud and your own elasticity mechanism inside.

### Objectives

The main goal in this practice is to make you confident in creating and managing virtual machines through Kevoree node encapsulation concept. After a learning phase of how to create and visualize virtual machines, you will have to write a componant aiming at managing a cluster of machine behind a load balancer. In details, the goal of this managament is to constantly adapt the number of running machines to the load.

### Setting up your environment

As in previous pratice levels, this tutorial requires a Kevoree runtime of your choice (i.e. GUI, prompt, standlane, KevScript maven runner...), an editor and a modern browser supporting WebSocket (e.g. Firefox, Chrome, Chromium, Safari).
