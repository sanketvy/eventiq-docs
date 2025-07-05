# EventIQ - Component and Modules Design

This document contains high level design and implementation details of the components of the architecture design.

## Ingestion Service
### Role
The primary purpose of the ingestion service is to listen to all the incoming events from various public SDKs used by customers. 
### Responsibilities
1. Accepts HTTP requests at `/api/v1/public/event` API. This is a public API exposed to all SDK Clients.
2. The application processed the requests, adds necessary metadata to the incoming event and further pushes to messaging queue for processing.
### Technology
1. Spring Reactive
2. Spring Cloud
3. Docker

---
## Authorization Service
### Role
The purpose is to provide the enterprise grade authentication to the client application.
### Responsibilities
1. Allow user to signup with the application using email and password.
2. Allow user to use the platform using OAuth Google login for a quicker and simpler process.
### Technology
1. KeyCloak Authorization Server

---
## Identity Service
### Role
The service has primary roles related to maintaining user identity and related information.
### Responsibilities
1. Maintaining user database in sync with keycloak, automatically. Also, maintain user data like email, firstname, lastname, company etc.
2. Creating eventIQ projects, with public API keys for client access.

### Technology

---
## Analytics Service
### Role
### Responsibilities
### Technology

---
## Analytics Processor Workers
### Role
### Responsibilities
### Technology

---
## Events Processor Workers
### Role
### Responsibilities
### Technology

---
## API Gateway
### Role
### Responsibilities
### Technology

---
## Landing Client
### Role
### Responsibilities
### Technology

---
## Application Client
### Role
### Responsibilities
### Technology