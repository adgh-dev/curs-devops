# Week 12 - Devops Part 1

## Table of contents

- [What is DevOps?](#devops)
- [DevOps - when Development meets Operations](#devops1)
- [Benefits of DevOps](#benefits)
- [DevOps Practices]
- [Linux commands in DevOps]
- [Overview of Virtual Machine](#overview-of-virtual-machine)
- [Overview of Container](#overview-of-a-container)
- [Container Orchestration](#container-orchestration)
- [Cloud Computing](#cloud-computing)

## What is DevOps? <a name="devops"></a>

DevOps is an approach to culture, automation, and platform design intended to deliver increased business value and responsiveness through rapid, high-quality service delivery.

The word "DevOps" is a mashup of "development’ and "operations" but it represents a set of ideas and practices much larger than those two terms alone, or together. DevOps describes approaches to speed up the processes by which an idea (like a new software feature, a request for enhancement, or a bug fix) goes from development to deployment in a production environment where it can provide value to the user. These approaches require that development teams and operations teams communicate frequently and approach their work with empathy for their teammates. 

## DevOps - when Development meets Operations <a name="devops1"></a>

 - Development: the infrastructure needed to unify development, from distributing resources to writing code and algorithms for enterprise applications, which can benefit from advanced capabilities such as AI/machine learning, containers, and serverless features. In addition, testing, archiving, tracking coding errors, and other important tasks are performed during the development phase, all on the way to release. Some frequently used tools for development: Git for code input, Github or the evolutionary Bitbucket for managing code repositories.

 - Operations - after an application is deployed, the operations side takes over, focusing on ensuring that cloud platforms are running smoothly. This function includes addressing issues such as user security, database management, scalability of production workflows, and patching. Some commonly used tools for operations: Terraform, Ansible, Puppet, and Chef for infrastructure and configuration management.

The result is an efficient model that maximizes resources and works at the ever-faster pace of the software development process, something that has become increasingly difficult to achieve with the traditional development model. In conclusion, a strong DevOps model enables companies to fix problems, grow users, and serve customers better by developing and iterating software products faster.

## Benefits od DevOps <a name="benefits"></a>

1. Speed 

![image](https://user-images.githubusercontent.com/24647488/208228552-717fe828-42ea-4358-8d2a-0971e6771156.png) 

With a flexible DevOps model, technology is optimized according to current lifecycle needs. In many cases, DevOps uses the latest machine learning and artificial intelligence technologies to achieve speed. 

DevOps also emphasizes automation and continuous integration/delivery, freeing staff from a number of manual activities to focus on innovation. On the development side, engineers can reach their coding goals faster or collaborate more effectively. On the operations side, system administrators can use automation frameworks to easily provision and upgrade new applications and infrastructure.


## Overview of Virtual Machine

### What is a Virtual Machine?

  Virtual machines are software computers that provide the same functionality as physical computers. Like physical computers, they run applications and an operating system. However, virtual machines are computer files that run on a physical computer and behave like a physical computer. 
  In other words, virtual machines behave as separate computer systems.

### Usage of Virtual Machine
  
  Virtual machines are created to perform specific tasks that are risky to perform in a host environment, such as accessing virus-infected data and testing operating systems. Since the virtual machine is sandboxed from the rest of the system, the software inside the virtual machine cannot tamper with the host computer. Virtual machines can also be used for other purposes such as server virtualization.

### Advantages of Virtual Machines:

- Provides disaster recovery and application provisioning options
- Virtual machines are simply managed, maintained, and are widely available
- Multiple operating system environments can be run on a single physical computer

### Disadvantages of Virtual Machines:

- Running multiple virtual machines on one physical machine can cause unstable performance
- Virtual machines are less efficient and run slower than a physical computer

## Overview of a Container

### What is a Container

A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another.

### Usage of a Container

Containers are an abstraction at the app layer that packages code and dependencies together. Multiple containers can run on the same machine and share the OS kernel with other containers, each running as isolated processes in user space. Containers take up less space than VMs (container images are typically tens of MBs in size), can handle more applications and require fewer VMs and Operating systems.

### Advantages of a Container

- Enables more efficient use of system resources
- Enables faster software delivery cycles
- Enables application portability
- Shines for microservices architecture

### Disadvantages of Container:

- Containers don't run at bare-metal speeds
- The container ecosystem is fractured. Its based on companies developments. Example: Openshift RedHat's container-as-a-service platform works only with Kubernetes container orchestrator.
- Persistent data storage is complicated
- Graphical applications don't work well
- Not all applications benefit from containers

![vm-container](https://rafay.co/wp-content/uploads/2022/06/Container-Evolution-.png)

## Container orchestration 

Container orchestration is the process of managing containers using automation. It allows organizations to automatically deploy, manage, scale and network containers and hosts, freeing engineers from having to complete these processes manually.

### How does container orchestration work?
Container orchestration is fundamentally about managing the container life cycle and the containerization of your environment. In general, the container life cycle follows the build-deploy-run phases of traditional software development, though the specific steps may vary slightly depending on the container orchestration tool being used. A typical life cycle might look like this:

- Build: In this first step, developers decide how to take the capabilities they’ve selected and build the application.
- Acquire: In this next step, containerized applications are usually acquired from public or private container image repositories. Developers start with a base image from one application and extend its functionality by placing a layer from another application over it. While using existing code from multiple sources in this way is more efficient and productive than creating everything from scratch, it also introduces the challenge of tracking the interdependencies among the various images.
- Deploy: This includes the process of placing and integrating the tested application into production.
- Maintain: In this step, developers continuously monitor the application to ensure it performs correctly. If it deviates from its desired state or fails, they try to understand the problem and fix it.

### What is container orchestration used for?
Container orchestration is used to automate and manage tasks across the container life cycle. This includes:
- Configuration and scheduling
- Provisioning and deployment
- Health monitoring
- Resource allocation
- Redundancy and availability
- Updates and upgrades
- Scaling or removing containers to balance workloads across the infrastructure
- Moving containers between hosts
- Load balancing and traffic routing
- Securing container interactions

One big advantage of container orchestration is that you may implement it in any environment where you can run containers, from on-premises servers to public, private, or multi-cloud running AWS, Microsoft Azure or Google Cloud Platform.

![kubernetes-cluster](https://preview.redd.it/lmewib0evdv41.png?width=926&format=png&auto=webp&s=f8bad3c01ef9e2e05b4b0fff703a8fa3f7d705fd)
![kubernetes-node](https://preview.redd.it/kjaq7ahfvdv41.png?width=562&format=png&auto=webp&s=06420f0355f3191c9efbbd4af90293f878fc4f92)

<br/>

## Cloud Computing

Cloud computing is a general term for anything that involves delivering hosted services over the internet. These services are divided into three main categories or types of cloud computing: infrastructure as a service (IaaS), platform as a service (PaaS) and software as a service (SaaS).

A cloud can be private or public. A public cloud sells services to anyone on the internet. A private cloud is a proprietary network or a data center that supplies hosted services to a limited number of people, with certain access and permissions settings. Private or public, the goal of cloud computing is to provide easy, scalable access to computing resources and IT services.

Cloud infrastructure involves the hardware and software components required for proper implementation of a cloud computing model. Cloud computing can also be thought of as utility computing or on-demand computing.

![cloud-services](https://www.mtechsystems.co.uk/wp-content/uploads/2022/06/Understanding-the-Different-Types-of-Cloud-Computing-Services-1024x414.jpg)

For what we are concerned, as devops engineers, we will look at IaaS offerings from cloud providers. Major players on the market at the time of this writing are:
- Amazon Web Services (AWS)
- Microsoft Azure
- Google Cloud Platform (GCP)

Throughout the exercises we will be using GCP, as it offers an extensive trial program of 3 months, with 99% of the services available (mostly services that require external licensing are unavailable - for example Windows Server VMs)

|     |                                            | Google Cloud Platform products span the following categories:                                                                                                                                                                                                                   |
| --- | ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.  | Artificial intelligence & Machine Learning | AI Hub (beta), Cloud AutoML (beta), Cloud TPU, Cloud Machine Learning Engine, Diagflow Enterprise Edition, Cloud Natural Language, Cloud Speech-to-Text, Cloud Text-to-Speech, Cloud Translation, Cloud Vision, Cloud Video Intelligence, Cloud Inference API (alpha), and more |
| 2.  | API management                             | API Analytics, API Monetization, Cloud Endpoints, Developer Portal, Cloud Healthcare API                                                                                                                                                                                        |
| 3.  | Compute                                    | Compute Engine, Shielded VMs, Container Security, App Engine, Cloud Functions, GPU, and more                                                                                                                                                                                    |
| 4.  | Data Analytics                             | BigQuery, Cloud Dataflow, Cloud Dataproc, Cloud Datalab, Cloud Dataprep, Cloud Composer, and more                                                                                                                                                                               |
| 5.  | Databases                                  | Cloud SQL, Cloud Bigtable, Cloud Spanner, Cloud Datastore, Cloud Memorystore                                                                                                                                                                                                    |
| 6.  | Developer Tools                            | Cloud SDK, Container Registry, Cloud Build, Cloud Source Repositories, Cloud Tasks, and more, as well as Cloud Tools for IntelliJ, PowerShell, Visual Studio, and Eclipse                                                                                                       |
| 7.  | Internet of Things (IoT)                   | Cloud IoT Core, Edge TPU (beta)                                                                                                                                                                                                                                                 |
| 8.  | Hybrid and multi-cloud                     | Google Kubernetes Engine, GKE On-Prem, Istio on GKE (beta), Anthos Config Management, Serverless, Stackdriver, and more                                                                                                                                                         |
| 9.  | Management Tools                           | Stackdriver, Monitoring, Trace, Logging, Debugger, Cloud Console, and more                                                                                                                                                                                                      |
| 10. | Media                                      | Anvato, Zync Render                                                                                                                                                                                                                                                             |
| 11. | Migration                                  | Cloud Data Transfer, Transfer Appliance, BigQuery Data Transfer Service, Velostrata, VM Migration, and more                                                                                                                                                                     |
| 12. | Networking                                 | Virtual Private Cloud (VPC), Cloud Load Balancing, Cloud Armor, Cloud CDN, Cloud NAT, Cloud Interconnect, Cloud VPN, Cloud DNS, Network Service Tiers, Network Telemetry                                                                                                        |
| 13. | Security                                   | Access Transparency, Cloud Identity, Cloud Data Loss Prevention, Cloud Key Management Service, Cloud Security Scanner, and more                                                                                                                                                 |
| 14. | Storage                                    | Cloud Storage, Persistent Disk, Cloud Filestore, and more                                                                                                                                                                                                                       |
