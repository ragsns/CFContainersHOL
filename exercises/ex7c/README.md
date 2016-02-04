#Containers and Cloud Foundry Hands-On Labs

##Exercise 7c: Container logs

Rudimentary logging is available by running the following command 

```
cf ic logs <Container ID>
```
or by accessing the UI at [http://console.ng.bluemix.net](http://console.ng.bluemix.net).

To be able to drain logs based on the syslog format further configuration of the container instance will be required depending on the program you're using.

### Summary

Rudimentary logging is straightforward but draining via syslog is a bit more involved whereas it's relatively easier with Cloud Foundry.
