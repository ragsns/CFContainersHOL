#Containers and Cloud Foundry Hands-On Labs

##Exercise 4: Connect to a service

Ensure that you are in sub-directory `ex4`.

```
cd <path-to-folder>/CFContainersHOL/ex4
```

Services are not part of the Cloud Foundry Elastic Runtime but they are an essential part of application deployment, like connecting to a MySQL database, a NoSQL database like MongoDB or Redis and so on.

In principle, they comprise of the following steps.

- Pick a service via the Marketplace
- Create the service
- Bind the application to the service (or connect to the service by an explicit binding in manifest.yml)
- Restage the application if required

We started the application previously without connecting to a service. We will now connect to a service.

First, let's explore the marketplace with the following command.

```
cf marketplace
```

You should get a listing of the different offerings, plans and so on as below.

```
Getting services from marketplace in org raghsrin@us.ibm.com / space dev as raghsrin@us.ibm.com...
OK

service                        plans                                                                                                                                                                          description   
API Management                 Standard v2*                                                                                                                                                                   Publish, manage, and consume APIs.   
AdvancedMobileAccess           Gold*, Bronze*                                                                                                                                                                 Finely tune mobile apps with operational analytics, and ensure communications with back end systems are secure.   
Analytics for Apache Hadoop    Free                                                                                                                                                                           IBM Analytics for Apache Hadoop is a quick and free option to try Apache Hadoop and BigInsights. For production use or proof of concept at scale, use the IBM BigInsights for Apache Hadoop service.   
AppScan Dynamic Analyzer       standard*                                                                                                                                                                      A robust, practical security vulnerability assessment for your web applications.   
AppScan Mobile Analyzer        standard*                                                                                                                                                                      A robust, practical security vulnerability assessment for your Android applications.   
AppServerOnCloud               WASLibertyCorePlan*, WASBasePlan*, BYOLPlan*, WASBaseDedicatedPlan*, WASNDDedicatedPlan*                                                                                       Allows you to quickly get up and running on a pre-configured WebSphere Liberty Web Profile Server or Full Profile Server in a hosted cloud environment on Bluemix.   
Application Security Manager   asm-service-plan                                                                                                                                                               A practical way to assess the business risk of your web applications.   
Auto-Scaling                   free                                                                                                                                                                           Automatically increase or decrease the number of application instances based on a policy you define.   
BigInsightsonCloud             Enterprise*                                                                                                                                                                    Provision managed bare metal Apache Hadoop clusters for production use or POCs at scale.   
CloudIntegration               cloudintegrationplan*                                                                                                                                                          Bluemix Cloud Integration enables users to integrate cloud services with enterprise systems of record   
Cognitive Commerce™            Beta                                                                                                                                                                           Cognitive Commerce is a service provided by Cognitive Scale.   
Cognitive Graph                Beta                                                                                                                                                                           Cognitive Graph is a service provided by Cognitive Scale.   
Cognitive Insights™            Beta                                                                                                                                                                           Cognitive Insights™ is a service provided by Cognitive Scale.   
DataCache                      starter*, standard*, premium*                                                                                                                                                  Improve the performance and user experience of web applications by retrieving information from fast, managed, in-memory caches, instead of relying entirely on slower disk-based databases.   
DataWorks                      free                                                                                                                                                                           Find, prepare, and deliver data with an intuitive app or with powerful APIs.   
Delivery Pipeline              Standard*                                                                                                                                                                      Use IBM DevOps Services to automate builds and deployments, test execution, configure build scripts, and automate execution of unit tests. Automatically build and deploy your application to IBM's cloud platform, Bluemix.   
Document Generation            Free plan                                                                                                                                                                      Generate documents from any standard data source with the Document Generation for Bluemix service.   
Elasticsearch by Compose       user-provided                                                                                                                                                                  Elasticsearch combines the power of a full text search engine with the indexing strengths of a JSON document database to create a powerful tool for rich data analysis on large volumes of data. With Elasticsearch your searching can be scored for exactness letting you dig through your data set for those close matches and near misses which you could be missing.   
Gamification                   public                                                                                                                                                                         This service provides an easy-to-use platform to gamify your apps   
Geocoding                      user-provided                                                                                                                                                                  Our address geocoding solutions help you to find exact geographical locations by inputting an address and returning a location.   
Geospatial Analytics           Standard*                                                                                                                                                                      Expand the boundaries of your application. Leverage real-time geospatial analytics to track when devices enter or leave defined regions.   
GraphDataStore                 Entry                                                                                                                                                                          A graph store service based on TinkerPop stack.   
IBM Globalization              Experimental                                                                                                                                                                   Use IBM Globalization to translate your Bluemix application UI from English into a selection of target languages.   
Integration Testing            free                                                                                                                                                                           Automated Integration Testing for Bluemix   
Internet of Things Workbench   InternetOfThingsWorkbenchExperimentalPlan                                                                                                                                      An intuitive development environment for rapid design, simulation, & construction of complete Internet of Things solutions and services   
IoT-RealTime-Insight           Free, Bronze*, Silver*                                                                                                                                                         Leverage your IoT Foundation with real-time analytics of your IoT data. Connect your devices and map to your assets, use customizable dashboards, and trigger alerts from your IoT sensor data.   
MAS                            Standard                                                                                                                                                                       Manage application access and implement a basic application security framework for the Mobile Cloud services with IBM Mobile Application Security (MAS) for Bluemix.   
Mobile Analyzer for iOS        free                                                                                                                                                                           A robust, practical security vulnerability assessment for your iOS applications.   
Mobile Quality Assurance       MobileQualityAssurance*, MobileQualityAssurancePremium*                                                                                                                        Capture tester and live user experience to continuously build and deliver high quality mobile apps.   
Mobile Quality Extensions      MQE Free Plan                                                                                                                                                                  This service provides some experimentation services for Mobile Application   
MobileData                     Shared*                                                                                                                                                                        Enhance your mobile apps through simple to use SDKs to save shared data in a scalable, managed database as a service. Powered by Cloudant.   
MongoDB by Compose             user-provided                                                                                                                                                                  MongoDB with its powerful indexing and querying, aggregation and wide driver support, has become the go-to JSON data store for many startups and enterprises. Compose makes MongoDB even better by offering an easy, auto-scaling deployment system which delivers high availability and redundancy, automated and on-demand no-stop backups, monitoring tools, integration into alert systems, performance analysis views and much more all in a clean, simple user interface.   
MonitoringAndAnalytics         Free, diagnostics*                                                                                                                                                             Gain the visibility and control you need over your application. Determine the response time your users see, understand the performance and availability of the application components, leverage analytics to keep your application up and performing well, and get automatically notified if application problems occur.   
Object Storage                 Free                                                                                                                                                                           Provides you access to a fully provisioned Swift Object storage account. Object storage is ideal for cost effective, scale-out storage. Swift provides a fully distributed, API-accessible platform that can be integrated into your applications or used for back up.   
PostgreSQL by Compose          user-provided                                                                                                                                                                  PostgreSQL is a powerful, open-source, highly-customizable, object-relational database. It's a feature-rich enterprise database with JSON support, giving you the best of both the SQL and NoSQL worlds.   
Push                           Standard*                                                                                                                                                                      Send relevant content to the right people at the right place and time with IBM Push for Bluemix.   
Redis by Compose               user-provided                                                                                                                                                                  Redis is an open-source, blazingly fast, key/value low maintenance store. Compose's platform gives you a configuration pre-tuned for high availability and locked down with additional security features.   
Reverse Geocoding              user-provided                                                                                                                                                                  Look up an address for a GPS location. Precision Reverse Geocoding empowers marketers to connect with consumers via location-based mobile marketing.   
Rocket Mainframe Data          User Provided-Beta                                                                                                                                                             Rocket Mainframe Data Service on Bluemix provides an easy way to leverage your mainframe data for new cloud services and mobile apps. Built on our proven data virtualization technology, this new mainframe data provides access to a breadth of data sources--without worrying about the underlying data format. Developers have the flexibility to use either MongoDB or SQL (JDBC) to access data on z Systems. With Rocket Mainframe Data Service on Bluemix, developers working in IBM Bluemix now have an agile method for incorporating system of record data on z Systems into cloud or mobile applications.   
SecureGateway                  securegatewayplan*                                                                                                                                                             IBM Secure Gateway for Bluemix enables users to integrate cloud services with enterprise systems on premises.   
SessionCache                   starter*, standard*, premium*                                                                                                                                                  Improve application resiliency by storing session state information across many HTTP requests. Enable persistent HTTP sessions for your application and seamless session recovery in event of an application failure.   
SingleSignOn                   standard*                                                                                                                                                                      Implement user authentication for your web and mobile apps quickly, using simple policy-based configurations.   
Static Analyzer                free                                                                                                                                                                           Use static analysis to find and fix security vulnerabilities early in the development of your Java applications.   
Track & Plan                   Standard*, Advanced*                                                                                                                                                           Use IBM DevOps Services to create stories, tasks, and defects to describe and track project work, and use agile planning tools for the product backlog, releases, and sprints.   
Travel Boundary Service        user-provided                                                                                                                                                                  Generate isochrone bands around a location based on driving time or distance, essential for site selection analysis, logistics planning, supply chain management and more.   
Twilio                         user-provided                                                                                                                                                                  Build apps that communicate. Integrate voice, messaging and VoIP into your web and mobile apps.   
Validate Address               user-provided                                                                                                                                                                  Standardize and validate addresses, ensuring that your address data adheres to quality standards established by the postal authority improving the deliverability of mail.   
Workflow                       standard*                                                                                                                                                                      Workflow for Bluemix makes it easy for you to create workflows that orchestrate and coordinate the REST-based services that you use in your apps.   
WorkloadScheduler              Standard*                                                                                                                                                                      Automate your tasks to run one time or on recurring schedules. Far beyond Cron, exploit job scheduling within and outside Bluemix.   
XPagesData                     xpages-data-free                                                                                                                                                               Create an IBM Notes .NSF database to store your XPages Domino data.   
activedeploy                   free                                                                                                                                                                           Update your running apps with zero downtime, or quickly revert to your original version.   
alchemy_api                    Free, Standard*                                                                                                                                                                An AlchemyAPI service that analyzes your unstructured text and image content   
apersona-amfa                  free                                                                                                                                                                           Frictionless Adaptive Multi-Factor Authentication   
apiHarmony                     API Harmony free plan                                                                                                                                                          IBM API Harmony for Bluemix supports developers in identifying and selecting APIs.   
blazemeter                     free-tier, basic1kmr*, pro5kmr*, pp10kmr*                                                                                                                                      The JMeter Load Testing Cloud   
box                            user-provided                                                                                                                                                                  Powering Content and data for your application.  Whether you are building a line of business app, content management software or need to display content beautifully on web and mobile, the Box API can help power the content and data layer of your application.   
businessrules                  standard*                                                                                                                                                                      Enables developers to spend less time recoding and testing when the business policy changes. The Business Rules service minimizes your code changes by keeping business logic separate from application logic.   
cleardb                        spark                                                                                                                                                                          Highly available MySQL for your Apps.   
cloudamqp                      lemur, bunny*, panda*, rabbit*, tiger*, ape*, hippo*                                                                                                                           Managed HA RabbitMQ servers in the cloud   
cloudantNoSQLDB                Shared*                                                                                                                                                                        Cloudant NoSQL DB provides access to a fully managed NoSQL JSON data layer that's always on. This service is compatible with CouchDB, and accessible through a simple to use HTTP interface for mobile and web application models   
concept_expansion              concept_expansion_free_plan                                                                                                                                                    Maps euphemisms or colloquial terms to more commonly understood phrases   
concept_insights               standard*                                                                                                                                                                      Explore the concepts behind your input, identifying associations beyond traditional text matching.   
cpy-insights                   free                                                                                                                                                                           End-to-end predictive insights for your Bluemix© app   
dashDB                         Entry*, Enterprise*, Enterprise256.4*, Enterprise256.12*, EnterpriseMPP.4*                                                                                                     Store relational data, including special types such as geospatial data, and analyze it with SQL, R, and built-in predictive and geospatial analytics functions.   
db2oncloud                     db2oncloud_small*, db2oncloud_medium*, db2oncloud_large*, db2oncloud_x-large*, db2oncloud_small_adv*, db2oncloud_medium_adv*, db2oncloud_large_adv*, db2oncloud_x-large_adv*   IBM DB2 on Cloud: Offers customers the rich features of an on-premise DB2 deployment without the cost, complexity, and risk of managing their own infrastructure.   
dialog                         standard*                                                                                                                                                                      Enable your application to use natural language to converse with users   
document_conversion            experimental                                                                                                                                                                   Converts HTML documents into sections that can be used to provide content for other Watson services.   
dreamface                      free, basic*, professional*, enterprise*                                                                                                                                       Web And Mobile Cloud Application Platform   
ecs-checker                    ecs-checker-free                                                                                                                                                               Automate accessibility verification of HTML and EPUB documents   
ecs-dashboard                  ecs-dashboard-free                                                                                                                                                             Integrate automated accessibility auditing and reporting capabilities into your deployment DevOps processes.   
elephantsql                    turtle, panda*, hippo*, elephant*, pigeon*                                                                                                                                     PostgreSQL as a Service   
erservice                      free                                                                                                                                                                           IBM Embeddable Reporting for Bluemix provides a mechanism to connect to relational data sources, create reports/dashboard, and embed this service within your application.   
flowthings                     free, start-up*, pro*, enterprise*                                                                                                                                             agile intelligence for IoT   
imfpush                        Basic*                                                                                                                                                                         Engage Android and iOS  mobile users by sending relevant content including interactive notifications   
iotf-service                   iotf-service-free, iotf-service-bronze*, iotf-service-silver*, iotf-service-gold*                                                                                              This service is the hub of all things IBM IoT, it is where you can set up and manage your connected devices so that your apps can access their live and historical data.   
kinetise                       free                                                                                                                                                                           Mobile applications creator. Multiplatorm. Native.   
language_translation           standard*                                                                                                                                                                      Translate text from one language to another for specific domains.   
loadimpact                     lifree                                                                                                                                                                         Performance and load testing for DevOps   
memcachedcloud                 100mb*, 1gb*, 5gb*, 250mb*, 2-5gb*, 10gb*, 500mb*, 30mb                                                                                                                        Enterprise-Class Memcached for Developers   
mongodb                        100                                                                                                                                                                            MongoDB NoSQL database   
mongolab                       sandbox                                                                                                                                                                        Fully-managed cloud MongoDB   
mqlight                        standard*                                                                                                                                                                      Develop responsive, scalable applications with a fully-managed messaging provider in the cloud. Quickly integrate with application frameworks through easy-to-use APIs.   
mysql                          100                                                                                                                                                                            MySQL database   
namara-catalog                 free                                                                                                                                                                           Open Data. Clean and simple.   
natural_language_classifier    standard*                                                                                                                                                                      Natural Language Classifier performs natural language classification on question texts. A user would be able to train their data and the predict the appropriate class for a input question.   
newrelic                       standard                                                                                                                                                                       Manage and monitor your apps   
objectstorage                  free                                                                                                                                                                           The Object Storage service in Bluemix is based on SoftLayer Object Storage which in turn is based on OpenStack Swift. It has built-in support for provisioning independent object stores and it creates an individual subaccount per object store.   
personality_insights           standard*                                                                                                                                                                      The Watson Personality Insights derives insights from transactional and social media data to identify psychological traits   
pm-20                          Free                                                                                                                                                                           Predictive Analytics   
postgresql                     100                                                                                                                                                                            PostgreSQL database   
presenceInsights               Basic*, Free                                                                                                                                                                   This service performs real-time and historical analytics on mobile device movements in a physical location. These insights can fuel contextually relevant engagement strategies that optimize the user experience and increase in-app conversions.   
probabilistic_match            free                                                                                                                                                                           Index, match, and search data for the 360 view of your customer. You have confidence in your ops and analytics, as you gather records across data sets.   
pubnub-sandbox                 free                                                                                                                                                                           Data Streaming and Realtime Communication   
pushreappt                     reappt:pushtechnology:free, reappt:pushtechnology:pilot*, reappt:pushtechnology:launch*, reappt:pushtechnology:scale*, reappt:pushtechnology:dream*                            Real Time Data Distribution Service   
question_and_answer            question_and_answer_free_plan                                                                                                                                                  Direct responses to users inquiries fueled by primary document sources   
rabbitmq                       100                                                                                                                                                                            RabbitMQ message queue   
redis                          100                                                                                                                                                                            Redis key-value store   
rediscloud                     100mb*, 10gb*, 500mb*, 5gb*, 2-5gb*, 50gb*, 1gb*, 250mb*, 30mb                                                                                                                 Enterprise-Class Redis for Developers   
relationship_extraction        relationship_extraction_free_plan                                                                                                                                              Intelligently finds relationships between sentences components (nouns, verbs, subjects, objects, etc.)   
retrieve_and_rank              standard*                                                                                                                                                                      Add machine learning enhanced search capabilities to your application   
sendgrid                       free, bronze*, silver*, gold*, platinum*                                                                                                                                       Email Delivery. Simplified.   
simplicite                     free, small*                                                                                                                                                                   Versatile Cloud Platform for Enterprise Applications   
spark                          free                                                                                                                                                                           IBM Analytics for Apache Spark for Bluemix.   
speech_to_text                 standard*                                                                                                                                                                      Low-latency, streaming transcription   
sqldb                          sqldb_free, sqldb_premium*                                                                                                                                                     SQL Database adds an on-demand relational database to your application. Powered by DB2, it provides a managed database service to handle web and transactional workloads.   
statica                        starter, spike*, micro*, medium*, large*, enterprise*, premium*                                                                                                                Enterprise Static IP Adresses   
streaming-analytics            Standard*                                                                                                                                                                      Ingest, analyze, monitor, and correlate data as it arrives from real-time data sources. View information and events as they unfold.   
text_to_speech                 standard*                                                                                                                                                                      Synthesizes natural-sounding speech from text.   
timeseriesdatabase             small*                                                                                                                                                                         Time Series Database (powered by Informix) is purpose-built for fast and efficient storage and analysis of time series data.   
tone_analyzer                  experimental                                                                                                                                                                   It helps people detect, understand and revise the language tones of emotions, social propensities and writing styles from their writings.   
tradeoff_analytics             standard*                                                                                                                                                                      Helps make better choices under multiple conflicting goals. Combines smart visualization and recommendations for tradeoff exploration   
twitterinsights                Free, Entry*                                                                                                                                                                   Use IBM Insights for Twitter to incorporate Twitter search results into your Bluemix applications.   
ustream                        basic                                                                                                                                                                          Video streaming, storage and publishing.   
visual_insights                experimental                                                                                                                                                                   Visual Insights enhances the customer view by analyzing photos and video to extract consumer insights related to interests, activities, hobbies, life events, and products.   
visual_recognition             free                                                                                                                                                                           Analyzes the visual content of images and videos to understand their content without requiring a textual description   

* These service plans have an associated cost. Creating a service instance will incur this cost.

TIP:  Use 'cf marketplace -s SERVICE' to view descriptions of individual plans of a given service.
```

We pick the `cloudamqp` service to connect with the application as below.

```
cf create-service cloudamqp lemur myrabbit
```

You should see a response like below.

```
Creating service instance rabbitmq in org raghsrin@us.ibm.com / space dev as raghsrin@us.ibm.com...
OK
```

If you run the command

```
cf services
```
You should see an output that looks something like below. The column "bound apps" that is blank indicates that no application is bound to it (yet).

```
Getting services in org raghsrin@us.ibm.com / space dev as raghsrin@us.ibm.com...
OK

name                               service                                                    plan                                        bound apps     last operation 
myrabbit                           cloudamqp                                                  lemur                                                      create succeeded
```

Next, we bind the service to the application using the following command.

Notice the `manifest.yml` in this directory which looks like below. It has been updated to bind to the service that has just been created. You can bind to more services if you want.

```
---
applications:
- name: pcfdemo
  memory: 512M
  instances: 1
  services: [myrabbit]
  host: pcfdemo-${random-word}
  path: ./target/pcfdemo.war
  env:
   JAVA_OPTS: -Djava.security.egd=file:///dev/urandom
```

Push the application again.

```
cf push
```

Notice in the output below (partially reproduced) the following line which shows that the service was bound.

```
Binding service myrabbit to app pcfdemo in org raghsrin@us.ibm.com / space dev as raghsrin@us.ibm.com...
```

Let's unbind the service as below.

```
cf unbind-service pcfdemo rabbitmq
```

We could have also bound the service manually by following the steps below.

```
cf bind-service pcfdemo rabbitmq
```

You should see an output that looks something like below.

```
Binding service rabbitmq to app pcfdemo in org raghsrin@us.ibm.com / space dev as raghsrin@us.ibm.com...
OK
TIP: Use 'cf restage pcfdemo' to ensure your env variable changes take effect
```

As suggested, issue the following command to restage the app and bind to the service.

```
cf restage pcfdemo
```

If you browse to the URL based on the output above, you should see a message "*Data being streamed from RabbitMQ*" indicating that the rabbitmq service was bound to the application. Now, if you click on the button `Start Data Stream`. You can rerun the `cf services` command to verify this. 

If you click on any state in the browser you will notice that data is indeed being streamed via RabbitMQ.

Run the following command after connecting to a service.

```
cf env pcfdemo
```

This will output the connection credentials to the service via variables in the environment that the application uses to determine if connected to the RabbitMQ service and how to connect to it.

Let's go ahead and delete the app. to free up resources.

```
cf delete pcfdemo --f
```

### Summary

We saw how to connect a service to an application.

Next we will look at how to scale the application.
