#Containers and Cloud Foundry Hands-On Labs

##Exercise 3c: Containerize the Application

Ensure that you are in sub-directory `ex3b`.

```
cd <path-to-folder>/CFContainersHOL/ex3b
```

Also make sure you're logged into IBM Containers and you have the environment variable `CONTAINER_NAMESPACE` instantiated.

```
echo $CONTAINER_NAMESPACE
```

If the output is blank, you need to export the environment variable `CONTAINER_NAMESPACE` as indicated in [exercise 1](../ex1).

Notice the `Dockerfile` in this directory. Its contents looks something like below.

```
FROM tomcat:7-jre7
MAINTAINER Rags

RUN ["rm", "-fr", "/usr/local/tomcat/webapps/ROOT"]
COPY /./target/pcfdemo.war /usr/local/tomcat/webapps/ROOT.war

CMD ["catalina.sh", "run"]
```

We start with a base tomcat image, deploy the application, instantiate the container and start it. Pretty straightforward!

Let's build the container with the following command.

```
cf ic build -t $CONTAINER_NAMESPACE/pcfdemo .
```

Which should yield an output like below.

```
Sending build context to Docker daemon 29.04 MB
Step 0 : FROM tomcat:7-jre7
 ---> 6e2693da42e8
Step 1 : MAINTAINER Rags
 ---> Running in b1dfef98487a
 ---> 3e3a4e566d8e
Removing intermediate container b1dfef98487a
Step 2 : RUN rm -fr /usr/local/tomcat/webapps/ROOT
 ---> Running in 375a8bb48db9
 ---> 7c19a4ca7f61
Removing intermediate container 375a8bb48db9
Step 3 : COPY /./target/pcfdemo.war /usr/local/tomcat/webapps/ROOT.war
 ---> e0ada6f3c26c
Removing intermediate container 1e45d34bce78
Step 4 : CMD catalina.sh run
 ---> Running in b671ce58bd59
 ---> 21ddb28f803d
Removing intermediate container b671ce58bd59
Successfully built 21ddb28f803d
The push refers to a repository [registry.ng.bluemix.net/ragsns/pcfdemo] (len: 1)
21ddb28f803d: Image already exists 
e0ada6f3c26c: Image successfully pushed 
7c19a4ca7f61: Image successfully pushed 
3e3a4e566d8e: Image successfully pushed 
6e2693da42e8: Image already exists 
043f8f17af36: Image already exists 
091147d0bd34: Image already exists 
b8572eeff90c: Image already exists 
2acf7d169343: Image already exists 
e8bff98d45c5: Image already exists 
a9012f9af271: Image already exists 
07a8a1a251f8: Image already exists 
38dde79b1a30: Image already exists 
507e827e87f2: Image already exists 
f9926aa78231: Image already exists 
b31b28b7a135: Image already exists 
742b29fb7583: Image already exists 
acc6e8c99435: Image already exists 
72df1363530d: Image already exists 
4f5ac798ba8f: Image already exists 
120cc37a76e0: Image already exists 
4abeef0c20e4: Image already exists 
706c9f1cbd8c: Image successfully pushed 
d4b2ba78e3b4: Image already exists 
cb6fb082434e: Image already exists 
Digest: sha256:e81e4327b4c6f2d9d02ccc9725cc83d085ea7dbaa5bf41c654475e78b29d12ca
```

Running the command

```
cf ic images
```

Should yield the following output (partially reproduced). Notice that the image was just created. Notice that the image was created just moments ago.

```
REPOSITORY                                               TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
registry.ng.bluemix.net/ragsns/pcfdemo                   latest              21ddb28f803d        4 minutes ago       359.3 MB
```

Let's create an instance of the container as below. We strictly don't need to create a container group, but we do so anyway because it provides us with a route than to have do it explicitly.

```
cf ic group create  -p 8080 --name pcfdemo --hostname pcfdemo-$CONTAINER_NAMESPACE --domain mybluemix.net --memory 512 --max 1 --desired 1 registry.ng.bluemix.net/$CONTAINER_NAMESPACE/pcfdemo
```

This should yield an output as below.


```
Create group in progress
Created group pcfdemo (id: 85538824-3ba9-461a-bc92-6a7a54a2430a)
Minimum container instances: 0
Maximum container instances: 1
Desired container instances: 1
```

Issue the following command to get the status of the container group. Eventually, the status of the group will change to `CREATE_COMPLETE` as shown below.

```
{
    "Cmd": [], 
    "Creation_time": "2016-02-03T22:43:52Z", 
    "Env": [
        "sgroup_name=pcfdemo", 
        "group_id=85538824-3ba9-461a-bc92-6a7a54a2430a", 
        "logging_password=", 
        "tagseparator=_", 
        "tenant_id=49911e9c-cf3e-4913-9e20-ff52ed6d34e3", 
        "space_id=49911e9c-cf3e-4913-9e20-ff52ed6d34e3", 
        "logstash_target=logmet.opvis.bluemix.net:9091", 
        "Image_name=registry.ng.bluemix.net/ragsns/pcfdemo:latest", 
        "Image_digest=registry.ng.bluemix.net/ragsns/pcfdemo@sha256:e81e4327b4c6f2d9d02ccc9725cc83d085ea7dbaa5bf41c654475e78b29d12ca", 
        "sgroup_id=85538824-3ba9-461a-bc92-6a7a54a2430a", 
        "tagformat=tenant_id group_id uuid", 
        "metrics_target=logmet.opvis.bluemix.net:9095", 
        "metadata_hidden_hostname=instance-001271d3"
    ], 
    "Id": "85538824-3ba9-461a-bc92-6a7a54a2430a", 
    "Image": "21ddb28f803dfb5c75f60035e53b475731754830cfbb22d0b3899d3e7ebaa9de", 
    "Memory": 512, 
    "Name": "pcfdemo", 
    "NumberInstances": {
        "CurrentSize": 1, 
        "Desired": 1, 
        "Max": 1, 
        "Min": 0
    }, 
    "Port": 8080, 
    "Route_Status": {
        "in_progress": false, 
        "message": "registered route successfully", 
        "successful": true
    }, 
    "Routes": [
        "pcfdemo-ragsns.mybluemix.net"
    ], 
    "Status": "CREATE_COMPLETE", 
    "Updated_time": null
}
```

Now browse the URL as shown above which should be `pcdemo-$CONTAINER_NAMESPACE.mybluemix.net` with the `CONTAINER_NAMESPACE` substituted and you should see the application deployed in a container.

Notice the message `No RabbitMQ service bound - streaming is not active`. We will do that later.

We will clean up by issuing the following command.

```
cf ic group rm -f pcfdemo
```
Let's delete the route explicitly as well.

```
cf delete-route mybluemix.net -f -n pcfdemo-$CONTAINER_NAMESPACE
```

# Summary

We saw how we can containerize an application and deploy into Bluemix containers with relative ease.

We will connect to a service, next.
