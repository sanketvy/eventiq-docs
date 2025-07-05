# EventIQ - Technology Stack

## 1. Authorization Server
For Authentication, eventIQ uses Keycloak Authorization server for centralized authentication along with social logins like gmail and github.

### Steps to set up keycloak :

1. Run the docker container `docker run -p 127.0.0.1:8001:8080 -d -e KC_BOOTSTRAP_ADMIN_USERNAME=admin -e KC_BOOTSTRAP_ADMIN_PASSWORD=admin quay.io/keycloak/keycloak:26.3.0 start-dev`, where 8080 is the port where keycloak runs. 
2. Create a new realm in the keycloak. 
3. Create a new client in the realm.
   a. Keep client Authentication OFF
4. To setup google identity provider, enter client id and client secret.
5. Create app with name and for authorized redirect URL use -http://localhost:8001/realms/eventiq/broker/google/endpoint 