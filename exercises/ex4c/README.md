#Containers and Cloud Foundry Hands-On Labs

##Exercise 4c: Connect a Cloud Foundry Service to a Container

Ensure that you are in sub-directory `ex4c`.

```
cd <path-to-folder>/CFContainersHOL/ex4c
```

Ensure that the `myrabbit` service has been created by running the following command.

```
cf services
````

You should see an output that shows the service `myrabbit`. 

```
Getting services in org raghsrin@us.ibm.com / space dev as raghsrin@us.ibm.com...
OK

name                               service                                                    plan                                        bound apps     last operation 
myrabbit                           cloudamqp                                                  lemur                                                      create succeeded
```
If the service is not created (based on output above), create it using the following command.

```
cf create-service cloudamqp lemur myrabbit
```

We pick this `cloudamqp` service and we provide the appropriate environment variables as below.

```
cf ic group create  -p 8080 -e "CCS_BIND_SRV=myrabbit" --name pcfdemo --hostname pcfdemo-$CONTAINER_NAMESPACE --domain mybluemix.net --memory 512 --max 1 --desired 1 --auto --env "VCAP_APPLICATION={}" registry.ng.bluemix.net/$CONTAINER_NAMESPACE/pcfdemo
```

You should an output like below.
```
Create group in progress
Created group pcfdemo (id: 948b070a-e309-4c3b-a868-1189c9b5667b)
Minimum container instances: 0
Maximum container instances: 1
Desired container instances: 1
```

Let's inspect the container recovery group using the command below.

```
cf ic group inspect pcfdemo
```

This will yield an output like below. The output includes the connection credentials to the service via variables in the environment that the application uses to determine if connected to the RabbitMQ service and how to connect to it.

```
{
    "Autorecovery": "true", 
    "BluemixServices": [
        "myrabbi"
    ], 
    "Cmd": [], 
    "Creation_time": "2016-02-04T03:41:26Z", 
    "Env": [
        "VCAP_SERVICES_CLOUDAMQP_0_METADATA_URL=https://api.ng.bluemix.net/v2/service_keys/ed64d44f-b135-44e5-81e1-cf8f1deee25a", 
        "Image_digest=registry.ng.bluemix.net/ragsns/pcfdemo@sha256:996e77c59c57acd1b02bdb0ca59cb71fdfc639df077c831d00c95e45ec525e1e", 
        "VCAP_SERVICES_CLOUDAMQP_0_LABEL=cloudamqp", 
        "VCAP_SERVICES_CLOUDAMQP_0_ENTITY_SERVICE_INSTANCE_URL=https://api.ng.bluemix.net/v2/service_instances/e5d03e81-21c2-445b-90ea-cd6617806576", 
        "tagformat=tenant_id group_id uuid", 
        "VCAP_SERVICES_CLOUDAMQP_0_CREDENTIALS_HTTP_API_URI=https://ynerosxl:12frf8LC53CS6ycbHLnXd5ZR7hpyWFhp@white-swan.rmq.cloudamqp.com/api/", 
        "VCAP_APPLICATION={}", 
        "VCAP_SERVICES_CLOUDAMQP_0_NAME=myrabbi", 
        "metadata_hidden_hostname=instance-0012782d", 
        "VCAP_SERVICES_CLOUDAMQP_0_CREDENTIALS_URI=amqp://ynerosxl:12frf8LC53CS6ycbHLnXd5ZR7hpyWFhp@white-swan.rmq.cloudamqp.com/ynerosxl", 
        "tagseparator=_", 
        "VCAP_SERVICES=<snip>{\"cloudamqp\": [{\"name\": \"myrabbi\", \"entity\": {\"service_instance_url\": \"https://api.ng.bluemix.net/v2/service_instances/e5d03e81-21c2-445b-90ea-cd6617806576\"}, \"plan\": \"lemur\", \"credentials\": {\"http_api_uri\": \"https://ynerosxl:12frf8LC53CS6ycb</snip>", 
        "logstash_target=logmet.opvis.bluemix.net:9091", 
        "VCAP_SERVICES_CLOUDAMQP_0_PLAN=lemur", 
        "metrics_target=logmet.opvis.bluemix.net:9095", 
        "sgroup_name=pcfdemo", 
        "logging_password=", 
        "tenant_id=49911e9c-cf3e-4913-9e20-ff52ed6d34e3", 
        "space_id=49911e9c-cf3e-4913-9e20-ff52ed6d34e3", 
        "CCS_BIND_SRV=myrabbi", 
        "Image_name=registry.ng.bluemix.net/ragsns/pcfdemo:latest", 
        "sgroup_id=e76a0029-6a0f-42a5-bfdb-1e9aac65b5b3", 
        "group_id=e76a0029-6a0f-42a5-bfdb-1e9aac65b5b3"
    ], 
    "Id": "e76a0029-6a0f-42a5-bfdb-1e9aac65b5b3", 
    "Image": "8a2de6991aaa4a9c37490f6f61f20ab742b9368488d74461ce11c45d381f7ee1", 
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

Notice the message `Data being streamed from RabbitMQ` indicating that the container is connected to the cloud foundry service. Clicking on a state, will display the heat map data.

Let's go ahead and delete the group to free up resources.

```
cf ic group rm -f pcfdemo 
```

### Summary

We saw how to connect a cloud foundry service to a container and how to inject the credentials of the service into the environment.

Next we will look at scaling and recoverability of the container.
