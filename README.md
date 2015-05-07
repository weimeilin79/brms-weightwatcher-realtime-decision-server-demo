JBoss BRMS Weightwatcher Realtime Decision Server Demo
======================================================
This demo project is a demonstration application of a stateless Realtime Decision Server based on JBoss BRMS 
and includes support for complex event processing (CEP) use cases based on a pseudo clock.  

Examples provided include a (REST) client sending a time series of facts in the form of weight observations 
to the deployed Realtime Decision Server. The Realtime Decision Server then reasons over the inputs to derive 
CEP insights such as average weight, least weight and weight change of a rolling time window. These insights 
are returned to the calling client as facts.


Install on local machine
------------------------
1. [Download and unzip.](https://github.com/jbossdemocentral/brms-weightwatcher-realtime-decicion-server-demo/archive/master.zip)

2. Add products to installs directory.

3. Run 'init.sh' or 'init.bat' file. 'init.bat' must be run with Administrative privileges.

4. Start JBoss BRMS Server by running ./target/jboss-eap-6.4/bin/standalone.sh

5. Login to http://localhost:8080/business-central

    ```
    - login for admin and analyst roles (u:erics / p:jbossbrms1!)
    ```

6. Build and deploy version 1.0 of project, verify at 'Authoring -> Artifact repository' to see deployed weightwatchers-1.0.jar artifact.

7. Open rule deployments perspective via menu Deploy -> Rules Deployments

8. Register a new server by filling in pop-up:

  - Endpoint: http://localhost:8080/kie-server/services/rest/server/
  
  - Name: DevServer (...as we are testing this in our dev environment)

  - Username: erics (...who must have role of kie-server)

  - Password: jbossbrms1!

9. Provision starts by creating a Container, click on DevServer '+' on right.

  - Name: container-weightwatchers1.0

  - search button gathers all artifacts available, SELECT weightwatchers-1.0 to auto-fill rest of fields

  - click on OK

10. Container is created, click on icon far right to view details.

11. Select container-weightwatchers1.0 and click START to get it up and running, was orange color next to name, should turn green.

12. See 'Resolved Release Id' section for the container and version that is running and ready for rule queries.

13. Using Firefox + RESTClient you can see which server containers are available by:

   - Add auth credentials in menu Authentication - Basic Authentication:  Username: erics    Password: jbossbrms1!

   - Method: GET

   - URL: http://localhost:8080/kie-server/services/rest/server/containers

   - it will show container = contianer-weightwatchers1.0, meaning our container is available via the provided RestAPI 

14. You can view some more information provided by the RestAPI using GET methods:

   - http://localhost:8080/kie-server/services/rest/server/containers/container-weightwatchers1.0

15. Now to use POST or PUT methods we need to add a header to RESTClient for our requests:

   - in menu Headers -> Custom Header

   - Name: Content-Type

   - Value: application/xml

16. Query the Realtime Decision Server with loan rules by using POST method:

   - http://localhost:8080/kie-server/services/rest/server/containers/container-weightwatchers1.0

   - body of message can be found in support/weightwatchers-query.xml file, copy into Body section of RESTClient.

   - note you can adjust the credit score field in the xml message body to show rows in decision table being used.

17. You can change the decision table as desired, redeploy a new version, use the Server Management Browser to manage the container
		using UPGRADE button to pull the latest version.

   - you need to deploy a new version of the rules, for example version 1.1, then enter 1.1 in version field of
     container-weightwatchers1.0 before hitting UPGRADE button.

18. For creation or deletion of containers in the RestAPI, you need to use PUT methods, see product documentation User Guide for
		details.


Notes
-----
You will need some sort of Rest client, such as the RESTClient Firefox extension which is used in this demo (screenshots and
videos). After installing RESTClient in Firefox, restart and open it under TOOLS menu.


Supporting Articles
-------------------
[Original Authors blog: Really Simple Rules Service](http://blog.emergitect.com/2014/12/08/really-simple-rules-service)


Released versions
-----------------
See the tagged releases for the following versions of the product:

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

