# Week 12 - Devops Part 1

## Table of contents

- [What is DevOps?]
- [DevOps - when Development meets Operations]
- [Benefits of DevOps]
- [DevOps Practices]
- [Linux commands in DevOps]
- [Overview of Virtual Machine](#overview-of-virtual-machine)
- [Overview of Container](#overview-of-a-container)
- [Differences between Virtual Machines and Containers](#differences-between-virtual-machines-and-containers)

## What is DevOps?

DevOps is an approach to culture, automation, and platform design intended to deliver increased business value and responsiveness through rapid, high-quality service delivery.

The word "DevOps" is a mashup of "development’ and "operations" but it represents a set of ideas and practices much larger than those two terms alone, or together. DevOps describes approaches to speed up the processes by which an idea (like a new software feature, a request for enhancement, or a bug fix) goes from development to deployment in a production environment where it can provide value to the user. These approaches require that development teams and operations teams communicate frequently and approach their work with empathy for their teammates. 

## DevOps - when Development meets Operations

 - Development: the infrastructure needed to unify development, from distributing resources to writing code and algorithms for enterprise applications, which can benefit from advanced capabilities such as AI/machine learning, containers, and serverless features. In addition, testing, archiving, tracking coding errors, and other important tasks are performed during the development phase, all on the way to release. Some frequently used tools for development: Git for code input, Github or the evolutionary Bitbucket for managing code repositories.

 - Operations - after an application is deployed, the operations side takes over, focusing on ensuring that cloud platforms are running smoothly. This function includes addressing issues such as user security, database management, scalability of production workflows, and patching. Some commonly used tools for operations: Terraform, Ansible, Puppet, and Chef for infrastructure and configuration management.

The result is an efficient model that maximizes resources and works at the ever-faster pace of the software development process, something that has become increasingly difficult to achieve with the traditional development model. In conclusion, a strong DevOps model enables companies to fix problems, grow users, and serve customers better by developing and iterating software products faster.

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
