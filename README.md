# Central Repository for software delevopment exam 2022
### Group members: 

**Name** Josef Marc Pedersen **Github** [@josefmarcc ](https://github.com/josefmarcc) **Email** cph-jp325@cphbusiness.dk  
**Name** Frederik Dinsen **Github**[@fdinsen](https://github.com/fdinsen) **Email** cph-fd77@cphbusiness.dk  
**Name** Sebastian Bentley **Github** [@sebastianbentley ](https://github.com/SebastianBentley) **Email** cph-sb287@cphbusiness.dk  
**Name** Frederik Dahl **Github** [@dahlfrederik ](https://github.com/dahlfrederik) **Email** cph-fd76@cphbusiness.dk  

## All repositories:
We have made a GitHub orginization for all repositories: [https://github.com/f2js](https://github.com/f2js)


The repositories for our services, can also be found here:
- [https://github.com/f2js/CPHMTOGO_API](https://github.com/f2js/CPHMTOGO_API)
- [https://github.com/f2js/cphmtogo_frontend](https://github.com/f2js/cphmtogo_frontend)
- [https://github.com/f2js/paymentsystem](https://github.com/f2js/paymentsystem)
- [https://github.com/f2js/cust-order-service](https://github.com/f2js/cust-order-service)
- [https://github.com/f2js/gateway](https://github.com/f2js/gateway)
- [https://github.com/f2js/cour-delivery-service](https://github.com/f2js/cour-delivery-service)
- [https://github.com/f2js/rest-management-service](https://github.com/f2js/rest-management-service)
- [https://github.com/f2js/rest-order-items-service](https://github.com/f2js/rest-order-items-service)
- [https://github.com/f2js/RatingProducer](https://github.com/f2js/RatingProducer)
- [https://github.com/f2js/cour-order-service](https://github.com/f2js/cour-order-service)
- [https://github.com/f2js/resource-provisioning](https://github.com/f2js/resource-provisioning)
- [https://github.com/f2js/KafkaSetup](https://github.com/f2js/KafkaSetup)

## Domain diagram 
![Domain model](domain.png)
The entire system has been designed using **domain driven design** - which is why the structure of our system appears to be very close to the domain diagram exploring the business domain. 

**Domain-driven design (DDD)** is a software design approach that aims to create a common language between business stakeholders and technical team members by using a shared understanding of the business domain to inform the design of the software. 

## System diagram 
![System diagram](system.png)
Our system uses a microservice architecture with a GraphQL API gateway that combines data from multiple microservices in response to user requests. The API gateway also handles authorization and issues unique JSON web tokens for each user. 

The legacy system is monolithic and handles tasks such as user creation, authentication, payment verification via an gRPC-service, and order tracking, which will eventually be separated into separate microservices. 

Each user role has its own OrderService that connects to the same cluster of HBase Order databases, allowing for flexibility in scaling up specific services as needed.

## Development process 
This system can be seen as an further development / scaling process to our monolithic application (CPHMTOGO). 
The starting point of our program is the *legacy monolithic application* in which we have further developed and divided responsibilities between various services to achieve a micro-service-oriented architecture. 

The system has an integrated CI/CD-pipeline using CircleCI that makes automatic deployments to Kubernetes utilising docker containers via dockerHub and terraform. 

### Business scenario 
CPHMTOGO is a food delivery company that allows customers to order food remotely through their website, mobile app, or telephone service. Customers have accounts with CPHMTOGO and can view the menu online, which is provided by partnering restaurants or CPHMTOGO's own food businesses. Restaurants pay a fee to use CPHMTOGO's service and a share of the order value, which is added as a processing fee to all orders. Customers do not pay a delivery charge and menu prices include free delivery. CPHMTOGO employs local couriers to collect and deliver food, and customers receive updates on their order through SMS, email, or the app. All payments are made on order and restaurants can reject orders if they cannot fulfill them. After delivery, customers receive a feedback request and management can view a dashboard of order status. CPHMTOGO's legacy application needs to be updated to handle the expected growth in customers and orders over the next 5 years.

## Event-driven design 
The system uses an event-driven design with Kafka for communication between microservices. This decouples the services and makes communication asynchronous. Kafka groups are used to ensure that only one replica of a service consumes each message.

### Kubernetes 
Kubernetes is a system for managing containerized applications that offers features such as automatic rollouts, rollbacks, self-healing, automatic scaling, and more. It consists of a master node or control plane, which includes an API server, controller, scheduler, and etcd key-value store, and worker nodes that include kubelets, pods, and kube-proxies. Pods are shared execution environments that can contain multiple containers, but it is recommended to use a single container per pod to maintain low coupling. When configuring a cluster, the desired number of replicasets can be specified, and Kubernetes will automatically set up new identical pods if necessary to maintain the desired state, a process known as self-healing. The kube-proxy and Kubernetes API service provide stable names and IPs and load balance the pods. Kubernetes also offers features such as persistent volumes and secrets for storing data, and ingress and egress rules for controlling access to the cluster.

### Terraform 
Terraform is an Infrastructure as Code (IaC) tool that provisions infrastructure in the cloud through declarative code. It automates the process of setting up infrastructure and keeps track of changes through a state file, allowing for easy expansion to multiple regions or even different providers. In our project, Terraform was used to provision a Kubernetes cluster on DigitalOcean and store the state file on terraform.io, allowing us to update our resources through our CI/CD pipeline

## Quality Assurance 
We used several quality techniques, including circle-ci, unit tests, integration tests, and acceptance tests, to ensure the quality of our software. Circle-ci is a continuous integration platform, unit tests verify individual code units, integration tests verify the integration of different code units and components, and acceptance tests verify that the software meets the specified requirements. We also employed the test-driven development model, writing tests before code to ensure proper function. These techniques improve the reliability, speed, and efficiency of our software development process.








