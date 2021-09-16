# Learning Kubernetes
By **Karthik Gaekwad**

## Reference
CNCF
architecht

## Prerequesites
- General IT concepts
- Devops Docker
- Shell Experience

## Containerization
containers have existed since long. (1972)
Docker evolves the definition to 
is a runtime instance containing:
1) a docker image
2) an execution environment
3) a standard set of instructions

The docker ecosystem
- the docker engine
  - runtime and packaging tools
  - must be installed on the host that run Docker
- the docker store (aka docker hub)
  - online cloud service where the users can store and share its docker image

containers looks like VM... but is not.
containers has application and its dependencies
runs isolated process on host
containers are portable ans packaged in a standard way
testing/packaging can be fully automated
elleviate platform dependencies issues
deployment is repeatable and efficient
scaling is simpler

Perfect for microservices architecture pattern
allows for CI/CD and agile dev

## Kubernetes
container orchestration
about 10 containers are runing on a single host
container orchestrator allows for
- provisioning host
- starting container on the host
- restarting failing containtes
- exposing containers as service outside the cluster
- scaling the cluster up or down

K8S: open sources 
issued from google (borg)
it runs on bare metal,, VM private or public cloud

one can use other container platform than docker (although the majority of users do)

K8s by Joe Beda (search for quote on the web)
- multi host containte scheduling
  - done by the kube scheduler
  - assigns podes to node at runtime
  - checks resources, quality of service, policies and user specification before scheduling
- scalability ad availability
  - K8s master can be deployed in a highly available configuration
  - multi region deployments are available
- Scalability (v 1.17)
  - supports  5000 nodes cluster
  - up to 150.000 total pods
  - max of 100 podes per node
  - pods are scaled horizontally via API
- Flexibility and Modularization
  - plug and play architecture
  - extend architecture when needed
  - has add ons: network drivers, service discovery, container runtime, vizualization and commands
- Registration and discovery allows for scale
- Persistent storage
- logging and monitoring (healthcheck, failure monitoring)
- loggin framework built in and can be replaced
- secrets managment is first class citizen

### Other Implementation 
don't build your own orchestrator today, you'll on ly regret and end up moving to something else...
- kuberneters
- doxcker swarm
- rancher
  - installe and manage K8s easily
  - early docker player
  - great UI and API
  - small to large team
  - 
- mesos
  - C++ api python and C++
  - apis in javea
  - older orchestrator
  - big data job
  - driven by devs
  - 
- amazone EC2
- google anthos

Chosing orchestrator
Two axis: 
    - size of the team
      - from small to large: nomad --> rancher --> docker Swarm --> mesos --> Kubernetes
    - number of host
      - from few to many: nomad --> Rancher --> Docker Swarm --> Mesos or K8s

companies to move to serverless infrastructure

## Terminology

- master node
  - api server
  - scheduler
  - controller manager
- etcd
  - manages db of running cervices
- kubectl
  - has a config file: kubeconfig
  - CLI for master node
- Worker Nodes
  - where the application operates
  - communicates throught the kubelet
  - has an container instance in it
  - kube proxy
    - load balancer for the service
    - manages network protocol for communication
    - zllows for exposition to the outside internet
    - 
  - pod: smallest unit
    - group of containerss running together for the app

### basic building blocks
Node serves as worker machine (can be VM of physical one)
has 
    kubelet
    surpervisord
    kupeproxy
Minikude allows for running K8s locally

### Pods
simplest unit to interact with
1 running process on the cluster
has:
- docker application container
- storage resources
- unique network IP
- options governing how the container should run
one can have multiple container running on a pod, and a pod represents a single unit of deployment. they are tightly coupled application sharing resources.
 
 Pods are
 ephemeral and disposable
 doesn't self heal
 doest not restart
 always use higher level constructs

 Pod states
 - pending
 - running
 - succeeded (will not be restarted; all container have executed normally)
 - faile (will not be restarted; at least one has exited abnormally)
 - crashloopback off
  
  Deployments, Replicate Sets and Services
  controllers allows for solving pb of application reliability
  scaling
  load balancing (having multiple isntance to balance load)

### ReplicaSet
- 1 job has as specified number of replica for  a pod running at the same time
### Depployment
- provides declarative (yaml) description of replica set
- suport controls of pods (start, pause, resume)
- used with large chnage set
- get status on deployment
### REplication controller
- early implementation of replicaset
### DameonSets
- all nodes runs a copy of a specific pod
### JObs
- supervisor process for pods carrying out batch jobs
- run individual process that runs once and complete successfully
### Service
allwo for communication between one set of dep
- has an IP
- internal service: only from inside the cluster
- external: external endpoint through node ip: port
- load balancer: expose the servcei to the internet

### Labels
- key/value pair attached to objects( pods, serivces...)
### Selectors
- equality based: == and !=
- set based: exist, in, not in a set
- are used with kubctl
### Namespaces
- allows to have multiple cluster hosted on the same infra
- creat for large enterprise
- allws to access resources with accountability
- divide cluyster between users
- provides scope into which names are unique


### KUBELET
K8S node agent running on every node
uses a posdspec (yaml) describing what's init

### kube proxy 
is a network proxy for what's inside the node
- user space mode
- iptables mode
- ipvs model

## Install Kubernetes
need to have docker and hyperversor installerd
get and install docker
hypervisor: virtualbox
instal kubectl
then get minikube from the k8s website and have it installed

for windows: get docker desktop, install...
there is a complex list of task to execute to get it running on windows. See LiL https://www.linkedin.com/learning/learning-kubernetes/getting-up-and-running-windows-install-2?u=98011314 (section "getting up and running on windows")

Next to Minikube, there are alternatives to run kubernetes:
1) minikube
   - Pro: large communities
   - original tooling to run K8S local
   - UX meant for new users
2) docker desktop
   - easy creation of cluster from GUI
   - good alternative for
   - lags on latest K8S version
3) kubernetes in docker (kind)
   - meant for testing K8s locally
   - good second level: not for beginners
4) managed kubernetes services in a cloud (e.g. Amazone Elastic Kubernetes Service - EKS)
   - available on all cloud provide
   - not a good 1st step for begining




 

