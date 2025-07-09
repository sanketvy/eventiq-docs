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

## 2. Messaging Queue - Kafka
For event driven, distributed asynchronous processing, eventIQ uses Kafka, which is wel suited for high throughput high traffic applications. 

### Steps to set up kafka :

1. Run the docker container `docker run -d --name kafka-kraft -e KAFKA_ENABLE_KRAFT=yes -e KAFKA_CFG_NODE_ID=0 -e KAFKA_CFG_PROCESS_ROLES=controller,broker -e KAFKA_CFG_CONTROLLER_LISTENER_NAMES=CONTROLLER -e KAFKA_CFG_LISTENERS=PLAINTEXT://:9092,CONTROLLER://:9093 -e KAFKA_CFG_ADVERTISED_LISTENERS=PLAINTEXT://localhost:9092 -e KAFKA_CFG_LISTENER_SECURITY_PROTOCOL_MAP=CONTROLLER:PLAINTEXT,PLAINTEXT:PLAINTEXT -e KAFKA_CFG_CONTROLLER_QUORUM_VOTERS=0@localhost:9093 -e KAFKA_KRAFT_CLUSTER_ID=abcdefghijklmno1234567 -e ALLOW_PLAINTEXT_LISTENER=yes -p 9092:9092 bitnami/kafka:latest`

## 3. Caching - Redis

1. Run the docker container `docker run -d --name redis -p 6379:6379 redis`