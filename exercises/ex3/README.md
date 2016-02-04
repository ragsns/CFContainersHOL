#Containers and Cloud Foundry Hands-On Labs

##Exercise 3: manifest.yml and more CLI commands

Ensure that you are in sub-directory `ex3`.

```
cd <path-to-folder>/CFContainersHOL/ex3
```


Notice the `manifest.yml` in this directory. Its contents looks something like below.

```
---
applications:
- name: pcfdemo
  memory: 512M 
  instances: 1
  host: pcfdemo-${random-word}
  path: ./target/pcfdemo.war
  env:
   JAVA_OPTS: -Djava.security.egd=file:///dev/urandom
```

The `manifest.yml` file is used for deployment if it's available and it's used to set the properties of the deployed application such as

- name of the application
- memory
- number of instances and so on.
- the path of the artifacts to be deployed, in this case it is `target/pcfdemo.war`

Change the instances to 2, and push the application again with the following command.

```
cf push
```
You should see an output (partially reproduced) which shows the instances running as 2.

```
requested state: started
instances: 2/2
usage: 512M x 2 instances
```

Also, notice the differences by running the following command which should show 2 running instances.

```
cf apps
```

Partial output is reproduced below.

```
pcfdemo                       started           2/2         512M     1G     pcfdemo-ineloquent-spookiness.mybluemix.net
```
Try stopping and restarting the applicaton. If you need help with the different commands, you can get help with the following command.

```
cf --help
```

Let's delete the application by issuing the following command.

```
cf delete pcfdemo
```

### Summary

We saw how we can manipulate an application via `manifest.yml` and deploy into Bluemix with relative ease. Its very easy to start and stop the application on demand.

We will connect to a service, next.
