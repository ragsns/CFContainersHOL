#Containers and Cloud Foundry Hands-On Labs

##Exercise 5c: Scale Containers

Let's start a container recovery group of two instances.

```
cf ic group create  -p 8080 --name pcfdemo --hostname pcfdemo-$CONTAINER_NAMESPACE --domain mybluemix.net --memory 512 --max 2 --desired 2 --auto registry.ng.bluemix.net/$CONTAINER_NAMESPACE/pcfdemo
```

You should an output like below.

```
Create group in progress
Created group pcfdemo (id: c9195b5f-e77e-4141-a71c-686358801164)
Minimum container instances: 0
Maximum container instances: 2
Desired container instances: 2
```

Running the following command repeatedly should show that the load is balanced automatically by a load balancer that front ends the instances created. In this case, it will cycle between the two instances.

```
curl http://pcfdemo-ragsns.mybluemix.net | grep -i instance
```

You should see an output that looks something like below.

```
Instance hosted at &nbsp;172.30.1.0:8080
```

Running the previous command again should yield an output that shows the load being handled by the other instance as below.

```
Instance hosted at &nbsp;172.30.1.1:8080
```

###Summary

We saw how scaling with containers can be achieved relatively easily by including it in a container recovery group.

Next we'll stop the instance within the container. We notice that the container recovery group which is monitoring the health of the container instances automatically restarts it.
