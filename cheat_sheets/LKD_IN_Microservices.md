


## Major Challenges
most critical challenge in microservices architecture is the call chains.
### logging
this can be easy but this must be planned early in the development process (unified logging mechanism) from day 1 otherwise the cost of recuperation is exponential
- support day to day 
- troubleshooting
- maintanance
- investigations
- general task

logging is much noisier in microservice architecture
- larger volume of artifacts
- agile nature
- different teams building up different logging strategies

log aggregator are then critical to use in this context. as it brings unification and consolidation of logging

Usage of tracing: a unique token is created from initial request and then transfered to all service calls mades.
the traceid is then used in all log and communication
structure of log + tracing is a no brainer to support long term operation

### continuous delivery
because ot he many moving parts, to improve the chances of success a strong continuous delivery is mandatory
[img]("lgall_gh\cheat_sheets\img\2021-05-07 12_26_34-Continuous delivery as a requirement.png")
continous delivery produces and compiles object whis are then moved to "non production environement".

value of microservice is agility, hence CI/CD is a must ... otherwise this is wasted effort

### Hybrid architecture
- hierarchical (althoug many are opposed to it)
  - prevent circular dependencie
  - models an n-tier architecture
a good intermediate step for braaking out the monolith
[img src="lgall_gh\cheat_sheets\img\2021-05-07 12_31_44-Hybrid architectures_ Hierarchy and service-based.png"]

- service based architecture
  similar to SOA
  - single underlying db
  - leverage service to handle decomposition
beware of the risk of "monolith of monolith" when not paying a proper attention to domain boundaries

## Making architecture choices
### design consideration
- continuous integration and delivery are the first aspects of the design
  - model simple pipeline
  - have it documented and automated
- design logging and tracing (see above the reasoning)
  - use log aggregator for log message structured appropriately
- consider DDD as a must "think"
- Service design to evaluate and control latency
- - no blocking point
  - standardize on the stack when possible (but always push for it)
- design the system "asynchronous first" (and move to synchronous when the point is made that synchronous is a must)

### Tradeoff
- paying the distribution tax
  - more distributable
  - well defined service boundaries (limiting the risks for monolith monoliths emergence)
  - scalability is eased
  - event driven asynchronous model allows to reduce this tax
- Issue of complexity
  - deployment complexity is the most critical issue
    - always a problem... but increases in microservices with the amount of moving parts
- Polyclkog development practices
  - microservice is heterogeneous..
  - but risk in team organisation and resources allocation
  - hence consider standardization
  
### Edge Services
API layer should be used as as proxy layer... pay attention not to bloat it though.
do not add logic in this layer
2 types of edges service
- outbound edge service
  - exposes client specific needs to outside world
    - not all client consuming our services are requiring the same workload
    - could be managed with API gateway
    - manage the edge service for the client and proxy them
      - managen code transformation simular to other codes in system
      - continue to provide a consistent interface evne though the underlying logic changes..
- indbound translation edge service
  - abstract from 3rd party dependency (hence quite critical)
    - protects from vendor changes on their API
    - limits the consequences of breaking changes
    - secures the risk brought by vendor changes
  - identify those services where it makes sense

### DevOps
Never underestimate culture...
devops culture is key... brings operation and development in the same sphere of discussion
distribution tax must be monitored to ensure lag doesn't have significatn impact
continuous monitoring allows for an automatic response to systems event (provisionning, scale up/down)
automation of testing and deployment increases the team efficiency and hence its throughput


## Conclusion
based foundation for micro service
    - history of service development
    - risk and benefits
    - cloud native
    - core concepts of microservices
      - communication pattern
    - advanced conception
      - logging
      - CI/CD as requ
      - asynchronous communication (event based)
