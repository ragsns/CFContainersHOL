#Containers and Cloud Foundry Hands-On Labs

##Prerequisites

Needless to say you'll need a laptop! Any OS is fine, but make sure to install the following software prior to the session:

**Prerequisite 1**: Install [Git](http://git-scm.com/downloads) (or "brew install git").


**Prerequisite 2**: Registered for a Bluemix account that is **still current** (trial Bluemix accounts are available at <http://console.ng.bluemix.net>). Contact the instructor for a promotion code for a bump in the quota. Please note down the `username` (or `email`) and `password` which will be used to login via the `cf` CLI.

**Prerequisite 3**: Install the The `cf` CLI from [https://github.com/cloudfoundry/cli#downloads] (https://github.com/cloudfoundry/cli#downloads) - download the latest version that is appropriate for your laptop and follow the instructions in README.txt. 
<p>

**Prerequisite 4**: Install the `ic` plugin for the `cf` CLI based on directions at [https://www.ng.bluemix.net/docs/containers/container_cli_cfic.html](https://www.ng.bluemix.net/docs/containers/container_cli_cfic.html)

##Samples and General Directions

Each directory is in a separate sub-directory. ***Ensure that you're in the sub-directory when you're working on a particular exercise and you're issuing the CLI commands from the subdirectory pertaining to the exercise.***

We've also provided a choice of samples. The **instructions will refer to the PCF-demo sample application** at [https://github.com/ragsns/PCF-demo](https://github.com/ragsns/PCF-demo) but they can be applied to the NodeJS app. or other Java apps as well.


##Recommended Exercises - User Related

It is recommended that you run through these exercises sequentially since they are progressive with some dependencies. Each exercise should take about 5-10 mins. to complete.

- Exercise 1: [Target the Cloud Foundry Instance](exercises/ex1)
- Exercise 2: [Push your application] (exercises/ex2)
- Exercise 3: [manifest.yml and more CLI commands] (exercises/ex3)
- Exercise 3c: [Containerize the Application] (exercises/ex3c)
- Exercise 4: [Connect to a service] (exercises/ex4)
- Exercise 4c: [Connect a Cloud Foundry Service to a Container] (exercises/ex4c)
- Exercise 5: [Scale your application] (exercises/ex5)
- Exercise 5c: [Scale Containers] (exercises/ex5c)
- Exercise 6: [Health Monitoring] (exercises/ex6)
- Exercise 6c: [Recoverability of Containers] (exercises/ex6c)
- Exercise 7: [Draining logs] (exercises/ex7)
- Exercise 7c: [Container logs] (exercises/ex7c)


##More Resources

Plenty of samples in multiple languages at [https://github.com/cloudfoundry-samples] (https://github.com/cloudfoundry-samples)

IBM Containers documentation at [https://www.ng.bluemix.net/docs/containers/container_index.html] (https://www.ng.bluemix.net/docs/containers/container_index.html)

IBM Containers CLI documentation at [https://www.ng.bluemix.net/docs/containers/container_cli_reference_cfic.html](https://www.ng.bluemix.net/docs/containers/container_cli_reference_cfic.html)

##Contact

Please contact me on Twitter @ragss.
