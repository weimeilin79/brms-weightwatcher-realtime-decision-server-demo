JBoss BRMS Weightwatcher Realtime Decision Server Demo
======================================================
This demo project is a demonstration application of a stateless Realtime Decision Server based on JBoss BRMS 
and includes support for complex event processing (CEP) use cases based on a pseudo clock.  

Examples provided include a (REST) client sending a time series of facts in the form of weight observations 
to the deployed Realtime Decision Server. The Realtime Decision Server then reasons over the inputs to derive 
CEP insights such as average weight, least weight and weight change of a rolling time window. These insights 
are returned to the calling client as facts.


Option 1 - Install on local machine
------------------------
1. [Download and unzip.](https://github.com/jbossdemocentral/brms-weightwatcher-realtime-decision-server-demo/archive/master.zip)

2. Add products to installs directory.

3. Run 'init.sh' or 'init.bat' file. 'init.bat' must be run with Administrative privileges.

4. Start JBoss BRMS Server by running ./target/jboss-eap-6.4/bin/standalone.sh

5. Login to http://localhost:8080/business-central

    ```
    - login for admin and analyst roles (u:erics / p:jbossbrms1!)
    ```

6. Build and deploy version 1.0 of project, verify at 'Authoring -> Artifact repository' to see deployed weightwatchers-1.0.jar artifact.

7. Open rule deployments perspective via menu Deploy -> Rules Deployments

8. Add a new Container to the 'local-server-123' template:

  - Name: containerweightwatchers10

  - In the search field, enter *weight* and click the *Search* button to gathers all artifacts available, SELECT com.redhat.demos:weightwatchers:1.0 to auto-fill rest of fields

  - click on *Finish*

9. The container is created. Click the *Start* button in the upper-right of the screen to start the container. The *local-server-123@localhost:8080* instance should now be displayed as on of the KIE-Servers running the template and container.

10. Click on the *local-server-123@localhost:8080* button, this will show the *GroupId*, *ArtifactId* and *Version* of the artifact running in the container, as well as the URL of the REST API.

11. Using Firefox + RESTClient you can see which server containers are available by accessing the following RESTful resource:

   - Add auth credentials in menu Authentication - Basic Authentication:  Username: erics    Password: jbossbrms1!

   - Method: GET

   - URL: http://localhost:8080/kie-server/services/rest/server/containers

   - it will show container = containerweightwatchers10, meaning our container is available via the provided RestAPI 

12. You can view some more information provided by the RestAPI using GET methods:

   - http://localhost:8080/kie-server/services/rest/server/containers/containerweightwatchers10

13. Now to use POST or PUT methods we need to add two headers to RESTClient for our requests:

   - http://localhost:8080/kie-server/services/rest/server/containers/instances/containerweightwatchers10

   - in menu Headers -> Custom Header

   - Name: Content-Type; Value: application/xml
  
   - Name: X-KIE-ContentType; Value: xstream

14. Query the Realtime Decision Server with weightwatcher rules by using POST method:

   - http://localhost:8080/kie-server/services/rest/server/containers/instances/containerweightwatchers10

   - The body of the message can be found in the support/weightwatchers-query.xml file. Copy the content of this file into the Body section of RESTClient.

15. To create or delete of containers via the RestAPI, you need to use the PUT an DELETE methods. See the product documentation's User Guide for details.


Option 2 - Generate containerized install
-----------------------------------------
The following steps can be used to configure and run the demo in a container:

1. [Download and unzip.](https://github.com/jbossdemocentral/brms-weightwatcher-realtime-decision-server-demo/archive/master.zip)

2. Add product installer to installs directory.

3. Copy contents of support/docker directory to the project root.

4. Build demo image.

	```
	docker build -t jbossdemocentral/brms-weightwatcher-realtime-decision-server-demo .
	```
5. Start demo container.

	```
	docker run -it -p 8080:8080 -p 9990:9990 jbossdemocentral/brms-weightwatcher-realtime-decision-server-demo
	```
6. Follow instructions from above starting at step 5 replacing *localhost* with *&lt;RH_CONTAINER_HOST&gt;* when applicable

Additional information can be found in the jbossdemocentral container [developer repository](https://github.com/jbossdemocentral/docker-developer)


Notes
-----
You will need some sort of Rest client, such as the RESTClient Firefox extension which is used in this demo (screenshots and
videos). After installing RESTClient in Firefox, restart and open it under TOOLS menu.


Supporting Articles
-------------------
- [7 Steps to Your First Rules with JBoss BRMS Starter Kit](http://www.schabell.org/2015/08/7-steps-first-rules-jboss-brms-starter-kit.html)

- [JBoss BPM Suite Quick Guide - Weight Watching with a Realtime Decision Server](http://www.schabell.org/2015/05/jboss-bpmsuite-quick-guide-weightwatching-realtime-decision-server.html)

- [Original Authors blog: Really Simple Rules Service](http://blog.emergitect.com/2014/12/08/really-simple-rules-service)


Released versions
-----------------
See the tagged releases for the following versions of the product:

- v1.1 JBoss BRMS 6.2.0, JBoss EAP 6.4.4 and demo rule project to deploy as Realtime Decision Server

- v1.0 JBoss BRMS 6.1 with demo rule project to deploy as Realtime Decision Server

![Loan Project](https://raw.githubusercontent.com/jbossdemocentral/brms-weightwatcher-realtime-decision-server-demo/master/docs/demo-images/weightwatchers-prj-overview.png)

![Artifact Repo](https://raw.githubusercontent.com/jbossdemocentral/brms-weightwatcher-realtime-decision-server-demo/master/docs/demo-images/artifact-repo-weightwatchers.png)

![Deployment View](https://raw.githubusercontent.com/jbossdemocentral/brms-weightwatcher-realtime-decision-server-demo/master/docs/demo-images/clean-rules-deployment-view.png)

![Kie Server Endpoint](https://raw.githubusercontent.com/jbossdemocentral/brms-weightwatcher-realtime-decision-server-demo/master/docs/demo-images/kie-server-endpoint.png)

![Register Server](https://raw.githubusercontent.com/jbossdemocentral/brms-weightwatcher-realtime-decision-server-demo/master/docs/demo-images/register-dev-server.png)

![Dev Server](https://raw.githubusercontent.com/jbossdemocentral/brms-weightwatcher-realtime-decision-server-demo/master/docs/demo-images/dev-server.png)

![Create Container](https://raw.githubusercontent.com/jbossdemocentral/brms-weightwatcher-realtime-decision-server-demo/master/docs/demo-images/create-container.png)

![Container Details](https://raw.githubusercontent.com/jbossdemocentral/brms-weightwatcher-realtime-decision-server-demo/master/docs/demo-images/container-details.png)

![Start Container](https://raw.githubusercontent.com/jbossdemocentral/brms-weightwatcher-realtime-decision-server-demo/master/docs/demo-images/start-container.png)

![Started Container](https://raw.githubusercontent.com/jbossdemocentral/brms-weightwatcher-realtime-decision-server-demo/master/docs/demo-images/started-container.png)

![Restapi Auth](https://raw.githubusercontent.com/jbossdemocentral/brms-weightwatcher-realtime-decision-server-demo/master/docs/demo-images/restapi-basic-authentication.png)

![Restapi Containers](https://raw.githubusercontent.com/jbossdemocentral/brms-weightwatcher-realtime-decision-server-demo/master/docs/demo-images/restapi-containers.png)

![Restapi Loan Container](https://raw.githubusercontent.com/jbossdemocentral/brms-weightwatcher-realtime-decision-server-demo/master/docs/demo-images/restapi-container-weightwatcher1.0.png)

![Restapi Request Header](https://raw.githubusercontent.com/jbossdemocentral/brms-weightwatcher-realtime-decision-server-demo/master/docs/demo-images/restapi-request-header.png)

![Restapi Loan Request](https://raw.githubusercontent.com/jbossdemocentral/brms-weightwatcher-realtime-decision-server-demo/master/docs/demo-images/restapi-weightwatchers-request.png)

![Restapi Loan Request Response](https://raw.githubusercontent.com/jbossdemocentral/brms-weightwatcher-realtime-decision-server-demo/master/docs/demo-images/restapi-weightwatchers-request-response.png)

