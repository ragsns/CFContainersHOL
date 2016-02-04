#Containers and Cloud Foundry Hands-On Labs

##Exercise 2: Push your application

Ensure that you are in sub-directory `ex2`.

```
cd <path-to-folder>/CFContainersHOL/ex2
```

We will use the Pivotal Cloud Foundry field engineering [demo.](https://github.com/Pivotal-Field-Engineering/PCF-demo) that is also [locally available](../samples/PCF-demo). For your convenience, symbolic links are provided. However, you can use the [samples directory](../samples/PCF-demo) to do the same.

Push the application with the following command.

```
cf push
```

You should see at output something like below.

```
Using manifest file /Users/raghavansrinivas/work/HOLs/javaone-cloudfoundry-hol/ex2/manifest.yml

Creating app pcfdemo in org raghsrin@us.ibm.com / space dev as raghsrin@us.ibm.com...
OK

Creating route pcfdemo-premarital-prolongment.mybluemix.net...
OK

Binding pcfdemo-premarital-prolongment.mybluemix.net to pcfdemo...
OK

Uploading pcfdemo...
Uploading app files from: /Users/raghavansrinivas/work/HOLs/javaone-cloudfoundry-hol/ex2/target/pcfdemo.war
Uploading 613.1K, 65 files
Done uploading               
OK

Starting app pcfdemo in org raghsrin@us.ibm.com / space dev as raghsrin@us.ibm.com...
-----> Downloaded app package (8.4M)
-----> Liberty Buildpack Version: v2.0-20150914-1535
-----> Avoid Trouble: Specify a minimum of 512M as the Memory Limit for your apps when using IBM JDK.
-----> Retrieving IBM 1.8.0_20150711 JRE (ibm-java-jre-8.0-1.10-pxa6480sr1fp10-20150711_01-cloud.tgz) ... (0.0s)
         Expanding JRE to .java ... (1.0s)
-----> Retrieving App Management 1.7.0_20150729-1104 (app-mgmt_v1.7-20150729-1104.zip) ... (0.0s)
         Expanding App Management to .app-management (1.1s)
-----> Downloading Auto Reconfiguration 1.10.0_RELEASE from https://download.run.pivotal.io/auto-reconfiguration/auto-reconfiguration-1.10.0_RELEASE.jar (1.8s)
       Modifying /WEB-INF/web.xml for Auto Reconfiguration
-----> Retrieving com.ibm.ws.liberty-2015.8.0.0-201509141535.tar.gz ... (0.0s)
         Installing archive ... (1.0s)
-----> Warning: Liberty feature set is not specified. Using the default feature set: ["beanValidation-1.1", "cdi-1.2", "ejbLite-3.2", "el-3.0", "jaxrs-2.0", "jdbc-4.1", "jndi-1.0", "jpa-2.1", "jsf-2.2", "jsonp-1.0", "jsp-2.3", "managedBeans-1.0", "servlet-3.1", "websocket-1.1"]. For the best results, explicitly set the features via the JBP_CONFIG_LIBERTY environment variable or deploy the application as a server directory or packaged server with a custom server.xml file.
-----> Liberty buildpack is done creating the droplet

-----> Uploading droplet (147M)

0 of 1 instances running, 1 starting
0 of 1 instances running, 1 starting
0 of 1 instances running, 1 starting
1 of 1 instances running

App started


OK

App pcfdemo was started using this command `.liberty/initial_startup.rb`

Showing health and status for app pcfdemo in org raghsrin@us.ibm.com / space dev as raghsrin@us.ibm.com...
OK

requested state: started
instances: 1/1
usage: 300M x 1 instances
urls: pcfdemo-premarital-prolongment.mybluemix.net
last uploaded: Tue Oct 13 01:51:46 UTC 2015
stack: cflinuxfs2
buildpack: Liberty for Java(TM) (WAR, liberty-2015.8.0_0, ibmjdk-1.8.0_20150711, env, java-opts, spring-auto-reconfiguration-1.10.0_RELEASE)

     state     since                    cpu    memory           disk           details   
#0   running   2015-10-12 09:53:03 PM   0.0%   176.5M of 300M   257.9M of 1G 
```

Your application has now been deployed. You can verify that by running the following command.

```
cf apps
```

Which should produce an output that looks something like below.

```
cf apps
Getting apps in org raghsrin@us.ibm.com / space dev as raghsrin@us.ibm.com...
OK

name                          requested state   instances   memory   disk   urls     
pcfdemo                       started           1/1         300M     1G     pcfdemo-premarital-prolongment.mybluemix.net
```

If you browse the URL from the output above you should be able to see a heat map that is not yet active since we've not connected a service. You will also notice a message "*No RabbitMQ service bound - streaming is not active*" indicating that the RabbitMQ service is not hooked up the application, yet.

You can get the application logs with the following command. We will subsequently connect to a log provider such as papertrail or splunk.

```
cf logs pcfdemo
```

You can delete the application with the following command, which will not prompt you and also delete all associated routes.

```
cf delete --f --r pcfdemo
```

and verify that it is deleted as below.

```
cf apps
```

```
No apps found
```

# Summary

We pushed a Cloud Foundry app with a `cf push` command. The Cloud Foundry platform used the appropriate buildpack and the application was made available.

We will look at the manifest file and how to connect to a service, subsequently.

