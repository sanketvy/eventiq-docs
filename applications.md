## 1. Consul : Service Discovery & Dynamic Configurations
EventIQ uses Hashicorp Consul for service discovery and dynamic configuration management among microservices.

To run container - 
`docker run -d --name=consul-dev -p 8500:8500 -p 8600:8600/udp consul:1.15 agent -dev "-client=0.0.0.0"`

The server is available at - http://localhost:8500/

We can create key value with the consul, which dynamically gets reloaded in other services.