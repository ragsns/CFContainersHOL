#Containers and Cloud Foundry Hands-On Labs

##Exercise 6c: Recoverability of Containers

Verify that the instances are still running (if need be clean up the resources and create a container recovery group with two instances from previous exercise) with the following command.

```
cf ic group instances pcfdemo
```

This should yield the following output.

```
Container Id                         Name                                                  Group                               Image                                         Created                             Updated                             State                               Private IP                          Port
0c3020fd-dc00-4a3f-a85e-04004369b347 pc-jnn5-s7vtwdi5b33l-ld4bf7irjozf-server-h6jj7y62qv24 pcfdemo                             registry.ng.bluemix.net/ragsns/pcfdemo:latest 2016-02-03 23:50:09 -0500 EST       Running                             172.30.1.1                          8080
e041224f-688e-42a3-8598-36142b6dea2b pc-jnn5-2lmwhics33ii-tenmpecphoe3-server-zbiqbllj4dfo pcfdemo                             registry.ng.bluemix.net/ragsns/pcfdemo:latest 2016-02-03 23:50:09 -0500 EST       Running                             172.30.1.0                          8080
```
We will stop one of the containers either using the container Id or by issuing a command as below which will extract the container ID of the last container.

```
cf ic rm --force $(cf ic group instances pcfdemo | tail -1 | awk '{print $1}')
```

Which should yield the following output.

```
e041224f-688e-42a3-8598-36142b6dea2b
```
Again, running the following command

```
cf ic group instances pcfdemo
```
Will yield the following output that shows only one instance running after one of the instances is deleted.

```
Container Id                         Name                                                  Group                               Image                                         Created                             Updated                             State                               Private IP                          Port
0c3020fd-dc00-4a3f-a85e-04004369b347 pc-jnn5-s7vtwdi5b33l-ld4bf7irjozf-server-h6jj7y62qv24 pcfdemo                             registry.ng.bluemix.net/ragsns/pcfdemo:latest 2016-02-03 23:50:09 -0500 EST       Running                             172.30.1.1                          8080
```

Running the following command again

```
curl http://pcfdemo-ragsns.mybluemix.net | grep -i instance
```
Will yield a single instance since the other instance has been killed.

```
Instance hosted at &nbsp;172.30.1.1:8080
```

Eventually the second instance will be restarted. Running the following command.

```
cf ic ps -a
```

Will yield the following output. Notice below that one of the instances was recently restarted (6 minutes ago) automatically.

```
CONTAINER ID        IMAGE                                                           COMMAND             CREATED             STATUS                   PORTS                                                      NAMES
e9129281-5f3        registry.ng.bluemix.net/ragsns/pcfdemo:latest                   ""                  6 minutes ago       Running 6 minutes ago    8080/tcp                                                   pc-jnn5-2lmwhics33ii-tenmpecphoe3-server-7iau5yt5xp3z
0c3020fd-dc0        registry.ng.bluemix.net/ragsns/pcfdemo:latest                   ""                  45 minutes ago      Running 44 minutes ago   8080/tcp                                                   pc-jnn5-s7vtwdi5b33l-ld4bf7irjozf-server-h6jj7y62qv24
```

### Summary

Just like that, with absolutely nothing required to be done by the application developer we see how health monitoring and restart of the container is being handled by the container recovery group.

Next, we will look at how to drain logs.
