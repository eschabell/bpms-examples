Vacation Request Process
===

Tested: JBoss BPM Suite 6.2.2 / JBoss EAP 6.4.7

# Functionality demonstrated:
- REST Service (GET & POST)
- Human Task assignment and escalation
- Business Rule for auto approval

This is a vacation process example which calls out to a REST service to get vacation information based on a particular ID.  Based on the rule for hours requested (10 hours or less), the request is auto approved or is routed to a manager.  If the manager does not claim/complete the task in 30 seconds, it's escalated to another group.  Once approved or not approved, the original requester can see the status.

# Actors:
- alice (id = 1) - requester
- jack (id = 2) - requester
- jane (id = 3) - requester
- john - manager
- joe - executive / escalation
- bpmsAdmin - admin user

password is 'passw0rd!'

# Deploying the demo
- The vacation REST project needs to be compiled
  - `mvn clean package`
  - Copy the `target/vacation.war` to your `<EAP_HOME>/standalone/deployments` directory
- The user / role files
  - Copy both `application-users.properties` & `application-roles.properties` to your `<EAP_HOME>/standalone/configuration` directory
- The BPMS project
  - Copy the `niogit` directory to `<EAP_HOME>/bin` and rename it to `.niogit`

# Starting the demo
- Login as the `bpmsAdmin` user and deploy the project
  - Authoring -> Open Project Editor -> Build -> Build & Deploy
- Once successfully deployed, logout and login as any of the requesters
  - Process Management -> Process Definitions -> Vacation process start
    - Fill in the ID number associated with the user
    - Fill in the number of hours being requested
  - If it's less than 10, it will be auto approved and the user will be assigned the task to see the approval
  - If it's more than 10, it will be routed to the manager
    - If the manager does not claim/complete the task within 30 seconds, it is routed to `joe`
    - Check the box to approve or not approve the vacation request
 
# REST Service API
- Get a list of all users
  - [GET] http://localhost:8080/vacation/rest/
- Get specific user
  - [GET] http://localhost:8080/vacation/rest/1
- Get the hours for a specific user
  - [GET] http://localhost:8080/vacation/rest/hours/1
- Submit a vacation request
  - [POST] http://localhost:8080/vacation/rest/request
  - [DATA] `{"associateId":"1","hours":-300}`


![Process Image](https://raw.githubusercontent.com/kenthua/bpms-examples/master/vacation-request/support/Vacation.VacationRequestProcess.png)

