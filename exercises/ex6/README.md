#Containers and Cloud Foundry Hands-On Labs

##Exercise 6: Health Monitoring

Health Monitoring happens at multiple levels. In the case of application level health monotring, the platform does a periodic health check and effectively restarts the application if it's down. There is really nothing else that an application developer has to do or to program.

We will scale down the application to a single instance with the following command.

```
cf scale pcfdemo -i=1
```

If you go back to the application URL, you will notice a button "KILL APP" which is used to exit the application.

When you hit this button, the application is terminated. However, the platform that is continually monitoring the health of the application will bring it back to a desired state as soon as it notices that the actual state does not match the desired state.

Note down the Instance details such as below.

```
Instance hosted at  10.254.2.154:61162
```

In the browser, hit the button "KILL APP" and **immediately** and continually refresh the page. Almost immediately or at some point you should see a "Page Not Found" message which indicates the application is not running.

After a while (**it may take a few minutes**) the application will be restarted and this time the Instance details will be different.

```
Instance hosted at  10.254.2.34:61134
```

### Summary

Just like that, with absolutely nothing required to be done by the application developer we see how health monitoring and restart of the application is being handled by the platform.

Next, we will look at how to drain logs.