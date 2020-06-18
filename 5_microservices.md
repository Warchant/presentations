##### Microservices

<img src="./microservices.png" style="width=550px;" />

+++

- **separately deployable units** (services)
- each unit may be written in different language
- distributed architecture
- without a dedicated devops team - this pattern is forbidden

+++

Problems:
- configuration
- service discovery
- logging
- request tracing
- orchestration
- secret management
- circuit breakers
- availability - `99.9% * 99.9% * 99.9% = 97.03%`
- ...

+++

![](./netflix_ms.jpg)

+++

![](./micronaut-microservices-architecture.png)

+++

Problems - Solutions:
- configuration - Consul
- service discovery - Consul
- logging - ELK
- request tracing - Zipkin
- orchestration - Docker + k8s/swarm
- secret management - Vault
- circuit breakers - ... ?
- availability - ... ?
- ...

+++

<img src="./PatternsRelatedToMicroservices.jpg" width=1000px />

+++

## Examples?
