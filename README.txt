Notation:
# means line as given in the assignment
bare command line is what I entered with variables subbed
-> is output



Users
curl -i -XPOST -H"Content-Type: application/json" localhost:8083/registration -d'{"name": "Pete"}'
-> {"id":1,"name":"Pete","info":"registration info"}
SO USER_ID IS 1

# curl -i localhost:8083/users/${USER_ID}
curl -i localhost:8083/users/1
-> {"id":1,"name":"Pete","info":"user info"}

Accounts
# curl -i localhost:8083/accounts?ownerId=${USER_ID}
curl -i localhost:8083/accounts?ownerId=1
->[{"id":1,"ownerId":1,"name":"Pete's account","info":"account info"}]
SO ACCOUNT_ID IS ALSO 1

Projects
#curl -i -XPOST -H"Content-Type: application/json" localhost:8083/projects -d"{\"name\": \"Basket Weaving\", \"accountId\": ${ACCOUNT_ID}}"
curl -i -XPOST -H"Content-Type: application/json" localhost:8083/projects -d"{\"name\": \"Basket Weaving\", \"accountId\": 1}"
-> {"id":1,"accountId":1,"name":"Basket Weaving","active":true,"info":"project info"}

#curl -i localhost:8083/projects?accountId=${ACCOUNT_ID}
curl -i localhost:8083/projects?accountId=1
-> [{"id":1,"accountId":1,"name":"Basket Weaving","active":true,"info":"project info"}]
SO PROJECT_ID IS ALSO 1

Allocations
#curl -i -XPOST -H"Content-Type: application/json" localhost:8081/allocations -d"{\"projectId\": ${PROJECT_ID}, \"userId\": ${USER_ID}, \"firstDay\": \"2015-05-17\", \"lastDay\": \"2015-05-18\"}"
curl -i -XPOST -H"Content-Type: application/json" localhost:8081/allocations -d"{\"projectId\": 1, \"userId\": 1, \"firstDay\": \"2015-05-17\", \"lastDay\": \"2015-05-18\"}"
-> {"id":1,"projectId":1,"userId":1,"firstDay":"2015-05-17","lastDay":"2015-05-18","info":"allocation info"}

#curl -i localhost:8081/allocations?projectId=${PROJECT_ID}
curl -i localhost:8081/allocations?projectId=1
-> [{"id":1,"projectId":1,"userId":1,"firstDay":"2015-05-17","lastDay":"2015-05-18","info":"allocation info"}]

Stories
#curl -i -XPOST -H"Content-Type: application/json" localhost:8082/stories -d"{\"projectId\": ${PROJECT_ID}, \"name\": \"Find some reeds\"}"
curl -i -XPOST -H"Content-Type: application/json" localhost:8082/stories -d"{\"projectId\": 1, \"name\": \"Find some reeds\"}"
-> {"id":1,"projectId":1,"name":"Find some reeds","info":"story info"}

#curl -i localhost:8082/stories?projectId=${PROJECT_ID}
curl -i localhost:8082/stories?projectId=1
-> [{"id":1,"projectId":1,"name":"Find some reeds","info":"story info"}]

Time Entries
#curl -i -XPOST -H"Content-Type: application/json" localhost:8084/time-entries/ -d"{\"projectId\": ${PROJECT_ID}, \"userId\": ${USER_ID}, \"date\": \"2015-05-17\", \"hours\": 6}"
curl -i -XPOST -H"Content-Type: application/json" localhost:8084/time-entries/ -d"{\"projectId\": 1, \"userId\": 1, \"date\": \"2015-05-17\", \"hours\": 6}"
-> {"id":1,"projectId":1,"userId":1,"date":"2015-05-17","hours":6,"info":"time entry info"}

#curl -i localhost:8084/time-entries?userId=${USER_ID}
curl -i localhost:8084/time-entries?userId=1
-> [{"id":1,"projectId":1,"userId":1,"date":"2015-05-17","hours":6,"info":"time entry info"}]


Handing in:

cd ~/workspace/assignment-submission
./gradlew cloudNativeDeveloperDistributedSystemDeployment \
    -PregistrationServerUrl=https://registration-pal-renzo-sean.apps.pikes.pal.pivotal.io \
    -PbacklogServerUrl=https://backlog-pal-renzo-sean.apps.pikes.pal.pivotal.io \
    -PallocationsServerUrl=https://allocations-pal-renzo-sean.apps.pikes.pal.pivotal.io \
    -PtimesheetsServerUrl=https://timesheets-pal-renzo-sean.apps.pikes.pal.pivotal.io



