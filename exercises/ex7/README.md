#Containers and Cloud Foundry Hands-On Labs

##Exercise 7: Drain Logs

Applications log to stdout in syslog format that can be redirected to a log provider. We will look at [papertrail] (https://papertrailapp.com/) for this but the instructions work for most syslog providers.

We will follow the instructions at [http://docs.cloudfoundry.org/devguide/services/log-management-thirdparty-svc.html#papertrail] (http://docs.cloudfoundry.org/devguide/services/log-management-thirdparty-svc.html#papertrail) to obtain an account. After opening an account, pick B. Cloud Foundry as an option. Then, we substitute the appropriate value of the URL and the PORT-NUMBER from the account details.

```
cf cups my-logs -l syslog://syslog://logs3.papertrailapp.com:PORT-NUMBER
```

Bind the service to the app with the following command.

```
cf bind-service pcfdemo my-logs
```

As suggested restage the app.

```
cf restage pcfdemo
```

If you wander over to paper trail on your browser and click on Dashboard you should be able to see the logs. 

### Summary

We aw how to consolidating logs using the syslog format.