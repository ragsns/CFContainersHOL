#Containers and Cloud Foundry Hands-On Labs

##Exercise 5: Scale the Application

Scaling an application is relatively straightforward. However, it's really upto the application to exploit *scale out* by effectively using the multiple instances. A Queueing application for instance can *scale out* by adding more workers.

Let's redeploy the application as we did in exercise 4 and not delete it (yet).

Next, let's scale down the application to 1 instance (if there are multiple instances) by using the following command.

```
cf scale -i=1 pcfdemo
```

Let's *scale out* the application to 2 instances by using the following command.

```
cf scale -i=2 pcfdemo
```

You should see an output that looks something like below.

```
Scaling app pcfdemo in org raghsrin@us.ibm.com / space dev as raghsrin@us.ibm.com...
OK
```

The command

```
cf apps
```

Should yield the following output showing that there are 2 instances of the application running.
```
Getting apps in org raghsrin@us.ibm.com / space dev as raghsrin@us.ibm.com...
OK

name                          requested state   instances   memory   disk   urls     
pcfdemo                       started           2/2         512M     1G     pcfdemo-clustery-cicatrix.mybluemix.net      
```

If you browse to the URL and hit the refresh button a few times you'll notice the hosted instance cycling through 2 different values, such as

```
Instance hosted at  10.254.2.130:61157
Instance hosted at  10.254.1.218:61067
```

The instance index also cycles between 0..1.

This indicates the load on the application is balanced amongst the 2 instances thereby achieving scale out.

Let's scale back down to 1 instance.

```
cf scale -i=1 pcfdemo
```

Can you try to scale up and down the application instead of scaling it out (hint: you have to manipulate the memory size)?

###Summary

We saw how scaling an application can be achieved relatively easily.

Next we'll stop this application. We notice that the platform which is monitoring the health of the application automatically restarts it.
