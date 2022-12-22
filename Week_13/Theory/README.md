# Week 12 - Devops

## Table of contents

- [Infrastructure as code - Terraform](#infrastructure-as-code---terraform)
- [Overview of Jenkins](#overview-of-jenkins)
- [Overview of Ansible](#overview-of-ansible)
- [What is DevOps?](#what-is-devops?)

## Infrastructure as code - Terraform

Infrastructure as code (IaC) tools allow you to manage infrastructure with configuration files rather than through a graphical user interface. IaC allows you to build, change, and manage your infrastructure in a safe, consistent, and repeatable way by defining resource configurations that you can version, reuse, and share.

Terraform is HashiCorp's infrastructure as code tool. It lets you define resources and infrastructure in human-readable, declarative configuration files, and manages your infrastructure's lifecycle. Using Terraform has several advantages over manually managing your infrastructure:

- Terraform can manage infrastructure on multiple cloud platforms.
- The human-readable configuration language helps you write infrastructure code quickly.
- Terraform's state allows you to track resource changes throughout your deployments.
- You can commit your configurations to version control to safely collaborate on infrastructure.

### Manage any infrastructure
Terraform plugins called providers let Terraform interact with cloud platforms and other services via their application programming interfaces (APIs). HashiCorp and the Terraform community have written over 1,000 providers to manage resources on Amazon Web Services (AWS), Azure, Google Cloud Platform (GCP), Kubernetes, Helm, GitHub, Splunk, and DataDog, just to name a few. Find providers for many of the platforms and services you already use in the Terraform Registry. If you don't find the provider you're looking for, you can write your own.

### Standardize your deployment workflow
Providers define individual units of infrastructure, for example compute instances or private networks, as resources. You can compose resources from different providers into reusable Terraform configurations called modules, and manage them with a consistent language and workflow.

Terraform's configuration language is declarative, meaning that it describes the desired end-state for your infrastructure, in contrast to procedural programming languages that require step-by-step instructions to perform tasks. Terraform providers automatically calculate dependencies between resources to create or destroy them in the correct order.

![terraform-deployment-workflow](https://content.hashicorp.com/api/assets?product=tutorials&version=main&asset=public%2Fimg%2Fterraform%2Fterraform-iac.png)

To deploy infrastructure with Terraform:

- Scope - Identify the infrastructure for your project.
- Author - Write the configuration for your infrastructure.
- Initialize - Install the plugins Terraform needs to manage the infrastructure.
- Plan - Preview the changes Terraform will make to match your configuration.
- Apply - Make the planned changes.

### Track your infrastructure
Terraform keeps track of your real infrastructure in a state file, which acts as a source of truth for your environment. Terraform uses the state file to determine the changes to make to your infrastructure so that it will match your configuration.

### Collaborate
Terraform allows you to collaborate on your infrastructure with its remote state backends. When you use Terraform Cloud, you can securely share your state with your teammates, provide a stable environment for Terraform to run in, and prevent race conditions when multiple people make configuration changes at once.

You can also connect Terraform Cloud to version control systems (VCSs) like GitHub, GitLab, and others, allowing it to automatically propose infrastructure changes when you commit configuration changes to VCS. This lets you manage changes to your infrastructure through version control, as you would with application code.

### About the Terraform Language
The main purpose of the Terraform language is declaring resources, which represent infrastructure objects. All other language features exist only to make the definition of resources more flexible and convenient.

A Terraform configuration is a complete document in the Terraform language that tells Terraform how to manage a given collection of infrastructure. A configuration can consist of multiple files and directories.

The syntax of the Terraform language consists of only a few basic elements:
```
resource "aws_vpc" "main" {
  cidr_block = var.base_cidr_block
}

<BLOCK TYPE> "<BLOCK LABEL>" "<BLOCK LABEL>" {
  # Block body
  <IDENTIFIER> = <EXPRESSION> # Argument
}
```

- Blocks are containers for other content and usually represent the configuration of some kind of object, like a resource. Blocks have a block type, can have zero or more labels, and have a body that contains any number of arguments and nested blocks. Most of Terraform's features are controlled by top-level blocks in a configuration file.
- Arguments assign a value to a name. They appear within blocks.
- Expressions represent a value, either literally or by referencing and combining other values. They appear as values for arguments, or within other expressions.

The Terraform language is declarative, describing an intended goal rather than the steps to reach that goal. The ordering of blocks and the files they are organized into are generally not significant; Terraform only considers implicit and explicit relationships between resources when determining an order of operations.

### Example
The following example describes a simple network topology for Amazon Web Services, just to give a sense of the overall structure and syntax of the Terraform language. Similar configurations can be created for other virtual network services, using resource types defined by other providers, and a practical network configuration will often contain additional elements not shown here.

```
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 1.0.4"
    }
  }
}

variable "aws_region" {}

variable "base_cidr_block" {
  description = "A /16 CIDR range definition, such as 10.1.0.0/16, that the VPC will use"
  default = "10.1.0.0/16"
}

variable "availability_zones" {
  description = "A list of availability zones in which to create subnets"
  type = list(string)
}

provider "aws" {
  region = var.aws_region
}

resource "aws_vpc" "main" {
  # Referencing the base_cidr_block variable allows the network address
  # to be changed without modifying the configuration.
  cidr_block = var.base_cidr_block
}

resource "aws_subnet" "az" {
  # Create one subnet for each given availability zone.
  count = length(var.availability_zones)

  # For each subnet, use one of the specified availability zones.
  availability_zone = var.availability_zones[count.index]

  # By referencing the aws_vpc.main object, Terraform knows that the subnet
  # must be created only after the VPC is created.
  vpc_id = aws_vpc.main.id

  # Built-in functions and operators can be used for simple transformations of
  # values, such as computing a subnet address. Here we create a /20 prefix for
  # each subnet, using consecutive addresses for each availability zone,
  # such as 10.1.16.0/20 .
  cidr_block = cidrsubnet(aws_vpc.main.cidr_block, 4, count.index+1)
}
```


## Overview of Jenkins

- Open source automation tool
- Jenkins is used to integrate all DevOps stages with the help of plugins.
- Jenkins has well over 1000 plugins: Git, Ansible, Amazon EC2, Maven 2 project, HTML publisher etc.
- Multi-technology
- Multi-platform
- Extensible
- Pipeline supports building Continuous Delivery (CDel) pipelines through either a Web UI or a scripted Jenkinsfile.

### Jenkins User Interface

![jenkins_ui](https://github.com/WebToLearn/fx-trading-app/blob/devops_open_source/Week_12/Theory/images/jenkins_ui.PNG)

## Overview of Ansible

- Open source automation platform
- Agentless
- Desired end state
- Idempotency
- Human-readable automation

> Playbook -> Play -> Task -> Module

### Orientation to the Classroom Environment

![classroom](https://github.com/WebToLearn/fx-trading-app/blob/devops_open_source/Week_12/Theory/images/classroom.PNG)

### Ansible Inventory

- Static inventory (groups, :children, implicit localhost) 
- Default groups: all (without the default: localhost), ungrouped

### Ansible Configuration Files

- Three locations: /etc/ansible/ansible.cfg, ~/.ansible.cfg, ./ansible.cfg (the recommended location for testing)
- Mostly used sections: [defaults], [privilege_escalation], [ssh_connection]

### Variables in playbooks

- vars:
![vars](https://github.com/WebToLearn/fx-trading-app/blob/devops_open_source/Week_12/Theory/images/vars.png)

- vars_files:
![vars_files](https://github.com/WebToLearn/fx-trading-app/blob/devops_open_source/Week_12/Theory/images/vars_files.png)

### Gathering facts

- Facts = variables that are automatically discovered by Ansible on a managed host.

Example of facts gathered from a managed host: the host name, the IP addresses, the version of the operating system, the available disk space, memory

### Implementing Task Control

- Loops: with_items, with_nested (loops inside of loops), with_fileglob
> Note: with_X deprecated, use loop instead
- Running tasks conditionally: when
- Implementing tags: --tags and --skip-tags

### Handlers

- Tasks that respond to a notification triggered by other tasks (using notify statement)
- Globally-unique name
- Ansible notifies handlers only if the task acquires the CHANGED status
- If no task notifies the handler by name -> it will not run
- If one or more tasks notify the handler -> it will run ONCE, AFTER all the tasks in the play are completed ( unless - meta: flush_handlers) 

### Ansible blocks and Error Handling

Blocks= clauses that logically group tasks

- block : main tasks to run
- rescue: tasks that will be run if the tasks in the block clause fails
- always: tasks that will run independently of the result of the other clauses

![block](https://github.com/WebToLearn/fx-trading-app/blob/devops_open_source/Week_12/Theory/images/block.png)

### Role structure

![role](https://github.com/WebToLearn/fx-trading-app/blob/devops_open_source/Week_12/Theory/images/role.PNG)

### Implementing roles

Create roles:

- Using ansible-galaxy command line tool
  - ansible-galaxy  init //will create the role structure
  - ansible-galaxy install -r //will install role

Use roles in playbooks

- roles/requirements.yml

![requirements](https://github.com/WebToLearn/fx-trading-app/blob/devops_open_source/Week_12/Theory/images/requirements.png)

### Order of execution

- default : the order specified in the playbook
- pre_tasks: executed before any roles are applied
- post_tasks: executed after all roles are applied

## What is DevOps?

Let's watch on Youtube [What is DevOps? - In Simple English](https://www.youtube.com/watch?v=_I94-tJlovg).

