JBoss BPM Suite Vacation Request Demo
=====================================
This is a simple vacation request process project for employees to request PTO / Vacation days. It demonstrates the following
functionality:

- Rest service (GET & POST)

- Human Task assignment and escalation

- Business Rule for auto approval

This is a vacation process example which calls out to a REST service to get vacation information based on a particular ID.  Based on the rule for hours requested (10 hours or less), the request is auto approved or is routed to a manager.  If the manager does not claim/complete the task in 30 seconds, it's escalated to another group.  Once approved or not approved, the original requester can see the status.


Option 1 - Install on your machine
----------------------------------
1. [Download and unzip.](https://github.com/eschabell/bpms-vacation-request-demo/archive/master.zip)

2. Add products to installs directory. For example download and add BPMS installer jar into the installs directory.

3. Run 'init.sh' or 'init.bat' file. 'init.bat' must be run with Administrative privileges.

4. Start JBoss BPMS Server by running 'standalone.sh' or 'standalone.bat' in the <path-to-project>/target/jboss-eap-6.4/bin
	 directory.

5. Login to [http://localhost:8080/business-central](http://localhost:8080/business-central)

    ```
     - login for admin and other roles (u:erics / p:bpmsuite1!)
    ```

Submitting a Vacation Request
-----------------------------
1. Fill in the ID number associated with the user

2. Fill in the number of hours being requested

3. If it's less than 10, it will be auto approved and the user will be assigned the task to see the approval

4. If it's more than 10, it will be routed to the manager

5. If the manager does not claim/complete the task within 30 seconds, it is routed to `joe`

6. Check the box to approve or not approve the vacation request

The REST Service API can be queried to show:

- Get a list of all users -> [GET] http://localhost:8080/vacation/rest/

- Get specific user -> [GET] http://localhost:8080/vacation/rest/1

- Get the hours for a specific user -> [GET] http://localhost:8080/vacation/rest/hours/1

- Submit a vacation request --> [POST] http://localhost:8080/vacation/rest/request   [DATA] `{"associateId":"1","hours":-300}`


Supporting Articles
-------------------
coming soon...


Released versions
-----------------
See the tagged releases for the following versions of the product:

- v1.0 - JBoss BPM Suite 6.2.0-BZ-1299002 on JBoss EAP 6.4.4 with vacation request process project installed.

![Process Image](https://raw.githubusercontent.com/eschabell/bpms-vacation-request-demo/master/docs/demo-images/Vacation.VacationRequestProcess.png)

