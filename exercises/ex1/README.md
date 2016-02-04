#Cloud Foundry Hands-On Labs

Make sure you've met the prerequisites.

**Prerequisite 1**: Install [Git](http://git-scm.com/downloads) (or "brew install git").


**Prerequisite 2**: Registered for a Bluemix account that is **still current** (trial Bluemix accounts are available at <http://console.ng.bluemix.net>). Contact the instructor for a promotion code for a bump in the quota. Please note down the `username` (or `email`) and `password` which will be used to login via the `cf` CLI.

**Prerequisite 3**: Install the The `cf` CLI from [https://github.com/cloudfoundry/cli#downloads] (https://github.com/cloudfoundry/cli#downloads) - download the latest version that is appropriate for your laptop and follow the instructions in README.txt. 
<p>

**Prerequisite 4**: Install the `ic` plugin for the `cf` CLI based on directions at [https://www.ng.bluemix.net/docs/containers/container_cli_cfic.html](https://www.ng.bluemix.net/docs/containers/container_cli_cfic.html)


##Exercise 1: Target the IBM Bluemix Cloud Foundry instance


Target the Bluemix Cloud Foundry instance by substituting the URL with the one provided and use the following command. 

```
cf api https://api.ng.bluemix.net # to Americas
```
**OR**

```
cf api https://api.eu-gb.bluemix.net # to Europe
```


The output for the `cf` CLI should look something like below.

```
Setting api endpoint to https://api.ng.bluemix.net...
OK

                   
API endpoint:   https://api.ng.bluemix.net (API version: 2.27.0)   
Not logged in. Use 'cf login' to log in.  
```

Login to the instance as directed.

```
cf login
```

Substitute the **non-expired** Bluemix account that was created earlier as below.

```
API endpoint: https://api.ng.bluemix.net

Email> <your Bluemix ID>

Password> 
Authenticating...
OK

Targeted org raghsrin@us.ibm.com

Targeted space dev


                   
API endpoint:   https://api.ng.bluemix.net (API version: 2.27.0)   
User:           raghsrin@us.ibm.com   
Org:            raghsrin@us.ibm.com   
Space:          dev
```


List the spaces with the following command

```
cf spaces
```

The output will look something line below.

```
Getting spaces in org raghsrin@us.ibm.com as raghsrin@us.ibm.com...

name   
dev
```

If there are no space(s) listed, then create a space `dev` with the following command.

```
cf create-space dev
```

The output will look something like below.

```
Creating space dev in org raghsrin@us.ibm.com as raghsrin@us.ibm.com...
OK
Assigning role SpaceManager to user raghsrin@us.ibm.com in org raghsrin@us.ibm.com / space dev as raghsrin@us.ibm.com...
OK
Assigning role SpaceDeveloper to user raghsrin@us.ibm.com in org raghsrin@us.ibm.com / space dev as raghsrin@us.ibm.com...
OK

TIP: Use 'cf target -o raghsrin@us.ibm.com -s dev' to target new space
```

Issue the command as provided in `TIP` above as below to target the newly created space (if required).

```
cf target -o <your IBM ID> -s dev
```

The output will look something like below.

```
API endpoint:   https://api.ng.bluemix.net (API version: 2.27.0)   
User:           raghsrin@us.ibm.com   
Org:            raghsrin@us.ibm.com   
Space:          dev  
```

List the services that are available with the following command (**NOTE: This might take upto a minute or more**)

```
cf marketplace
```

You should see an output that lists the different services and the plans that are available via IBM Bluemix. Partial output is below.

```
Getting services from marketplace in org raghsrin@us.ibm.com / space dev as raghsrin@us.ibm.com...
OK

service                        plans                                                                                                                                                                          description   
API Management                 Standard v2*                                                                                                                                                                   Publish, manage, and consume APIs.   
AdvancedMobileAccess           Gold*, Bronze*
```

List the apps by issuing the following command.

```
cf apps
```

The output will look something like below.

```
Getting apps in org raghsrin@us.ibm.com / space dev as raghsrin@us.ibm.com...
OK

No apps found
```

### Target the IBM Bluemix Containers instance

If you've already set a namespace, you can skip to the next step. Otherwise, set a namespace with the following command.

```
cf ic namespace set <unique name - I use my GitHub and Docker name>
``` 

Login to IBM Containers as below. If you are prompted to setup a namespace, execute the command above.

```
cf ic login
```

You can run most Docker commands by following it with `cf ic`. For example,

```
cf ic ps -a
```

Which will list all the instances.

We will export the namespace into an environment variable that we will subsequently use as below.

```
CONTAINER_NAMESPACE = $(cf is namespace get)
```


#Summary

We targeted the Cloud Foundry instance and IBM Containers running Docker.

We will be using both Cloud Foundry and Docker side by side. We will be pushing an app., containerizing the app. and connecting to a service in the upcoming exercises.

You can also try additional options for the CLI.
