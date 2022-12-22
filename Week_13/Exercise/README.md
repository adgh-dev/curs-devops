Get project id:
gcloud config list --format 'value(core.project)'

# Week 13 - Continous deployment exercises

## Table of contents

- [Exercise 1 - Create a VM in Google Cloud](#exercise-1---create-a-vm-in-google-cloud)
- [Exercise 2 - Deploy the quote-service application in VM](#exercise-2---deploy-the-quote-service-application-in-vm)
- [Exercise 3 - Install and configure Docker on a Debian 11 host](#exercise-3---install-and-configure-docker-on-a-debian-11-host)
- [Exercise 4 - Build and deploy the application in a Docker container](#exercise-4---build-and-deploy-the-application-in-a-docker-container)
- [Exercise 5 - Deploy quote-service as a serverless application](#exercise-5---deploy-quote-service-as-a-serverless-application)

<br/>

## Exercise 1 - Infrastrucutre as code with Terraform - Introduction

### Overview
In this lab, you will use Terraform to create, update, and destroy Google Cloud resources. You will start by defining Google Cloud as the provider.
You will then create a VM instance without mentioning the network to see how terraform parses the configuration code. You will then edit the code to add network and create a VM instance on Google Cloud.
You will explore how to update the VM instance. You will edit the existing configuration to add tags and then edit the machine type. You will then execute terraform commands to destroy the resources created.

### Objectives
In this lab you will learn how to perform the following tasks:
- Verify Terraform installation
- Define Google Cloud as the provider
- Create, change, and destroy Google Cloud resources by using Terraform

### Check Terraform Installation
1.	On the Google Cloud menu, click Activate Cloud Shell. If a dialog box appears, click Continue.
2.	If prompted, click Continue.
3.	Confirm that Terraform is installed by running the following command:
```
terraform --version
```

Note: The available downloads for the latest version of Terraform can be found on the Terraform website. Terraform is distributed as a binary package for all supported platforms and architectures and Cloud Shell uses Linux 64-bit.
The output should look like this (do not copy; this is example output):
```
Terraform v1.2.2
Terraform comes pre-installed in Cloud Shell. With Terraform already installed, you can directly create some infrastructure.
```

### Add Google Cloud provider
1.	Create a directory called compute:
```
mkdir compute
```
2.	Create the main.tf file:
```
touch main.tf
```
3.	Click Open Editor on the toolbar of Cloud Shell. Click Open in a new window to leave the Editor open in a separate tab.
4.	Copy the following code in the main.tf file.
```
terraform {
  required_providers {
    google = {
      source = "hashicorp/google"
    }
  }
}
provider "google" {
  region  = "us-central1"
  zone    = "us-central1-c"
}
```
5.	Click File > Save.
6.	Switch to the Cloud Shell and run the terraform init command.
```
terraform init
```
The output should look like this (do not copy; this is example output):
```
Initializing the backend...
Initializing provider plugins...
- Finding hashicorp/google versions matching "4.15.0"...
- Installing hashicorp/google v4.15.0...
- Installed hashicorp/google v4.15.0 (signed by HashiCorp)
Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.
Terraform has been successfully initialized!
```

### Build the infrastructure
Let us try creating a compute instance without specifying the network parameter and see how terraform processes such configuration.
1.	Switch to the editor window. Within the main.tf file, enter the following code block.
```
resource "google_compute_instance" "terraform" {
  name         = "terraform"
  machine_type = "n1-standard-2"
  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-11"
    }
  }
}
```
2.	Save the main.tf file by clicking File > Save.
3.	Now run the following command to preview if the compute engine will be created.
```
terraform plan
```
4.	The configuration fails with the following error. This is because you cannot configure a compute engine without a network.
```
│ Error: Insufficient network_interface blocks
│
│ on main.tf line 15, in resource "google_compute_instance" "terraform":
│ 15: resource "google_compute_instance" "terraform" {
│
│ At least 1 "network_interface" blocks are required.
5.	Now add the network by including the following code segment to the google_compute_instance block.
network_interface {
    network = "default"
    access_config {
    }
}
```
The final code in main.tf file will look like this:
```
terraform {
  required_providers {
    google = {
      source = "hashicorp/google"
    }
  }
}
provider "google" {
  region  = "us-central1"
  zone    = "us-central1-c"
}
resource "google_compute_instance" "terraform" {
  name         = "terraform"
  machine_type = "n1-standard-2"
  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-11"
    }
  }
  network_interface {
    network = "default"
    access_config {
    }
  }
}
```
6.	Save the main.tf file by clicking File > Save.
7.	Now run the terraform plan command to preview if the compute engine will be created.
```
terraform plan
```
Click Authorize when prompted.
The output should look like this (do not copy; this is example output):
```
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create
Terraform will perform the following actions:
  # google_compute_instance.terraform will be created
  + resource "google_compute_instance" "terraform" {
      + can_ip_forward       = false
      + cpu_platform         = (known after apply)
      + current_status       = (known after apply)
      + deletion_protection  = false
      ...
Plan: 1 to add, 0 to change, 0 to destroy.
```
8.	Apply the desired changes by running the following command.
```
terraform apply
```
9.	Confirm the planned actions by typing yes.
The output should look like this (do not copy; this is example output):
```
...
Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
Note: If you get an error, revisit the previous steps to ensure that you have the correct code entered in the main.tf file.
```

### Verify on Cloud Console
In the Cloud Console, verify that the resources were created.
1.	In the Cloud Console, on the Navigation menu, click Compute Engine > VM instances.
2.	View the terraform instance created. 

### Change the infrastructure
In this task, we will be performing 2 types of changes to the infrastructure:
- Adding network tags
- Editing the machine-type
Adding tags to the compute resource
In addition to creating resources, Terraform can also make changes to those resources.
1.	Add a tags argument to the instance we just created so that it looks like this:
```
resource "google_compute_instance" "terraform" {
  name         = "terraform"
  machine_type = "n1-standard-2"
  tags         = ["web", "dev"]
  # ...
}
```
2.	Run terraform plan
```
terraform plan
```
3.	Run terraform apply to update the instance.
```
terraform apply
```
The output should look like this (do not copy; this is example output):
```
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  ~ update in-place
Terraform will perform the following actions:
  # google_compute_instance.terraform will be updated in-place
  ~ resource "google_compute_instance" "terraform" {
        id                   = "projects/qwiklabs-gcp-00-da04aeabe9ab/zones/us-central1-c/instances/terraform"
        name                 = "terraform"
      ~ tags                 = [
          + "dev",
          + "web",
        ]
        # (17 unchanged attributes hidden)
        # (4 unchanged blocks hidden)
    }
Plan: 0 to add, 1 to change, 0 to destroy.
```
The prefix ~ means that Terraform will update the resource in-place.

4.	Respond yes when promoted, and Terraform will add the tags to your instance.

### Editing the machine type without stopping the VM
Machine type of a VM cannot be changed on a running VM. Let us see how terraform processes the change in machine type for a running VM.
1.	Navigate to main.tf and edit the machine_type argument of terraform instance from n1-standard-2 to n1-standard-1 so that it looks like this:
```
resource "google_compute_instance" "terraform" {
  name         = "terraform"
  machine_type = "n1-standard-1"
  tags         = ["web", "dev"]
  # ...
}
```
2.	Run terraform plan
```
terraform plan
```
3.	Run terraform apply again to update the instance.
```
terraform apply
```
The terraform apply fails with a warning as shown below. (do not copy; this is example output)
```
╷
│ Error: Changing the machine_type, min_cpu_platform, service_account, enable_display, shielded_instance_config, scheduling.node_affinities or network_interface.[#d].(network/subnetwork/subnetwork_project) or advanced_machine_features on a started instance requires stopping it. To acknowledge this, please set allow_stopping_for_update = true in your config. You can also stop it by setting desired_status = "TERMINATED", but the instance will not be restarted after the update.
│
│   with google_compute_instance.terraform,
│   on main.tf line 31, in resource "google_compute_instance" "terraform":
│   31: resource "google_compute_instance" "terraform" {
```
4.	The machine-type cannot be changed on a running VM. To ensure the VM stops before updating the machine_type, set allow_stopping_for_update argument to true so that the code looks like this:
```
resource "google_compute_instance" "terraform" {
  name         = "terraform"
  machine_type = "n1-standard-1"
  tags         = ["web", "dev"]
  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-11"
    }
  }
  network_interface {
    network = "default"
    access_config {
    }
  }
  allow_stopping_for_update = true
}
```
5.	Run terraform plan
```
terraform plan
```
6.	Run terraform apply again to update the instance.
```
terraform apply
```
7.	Respond yes when promoted.
8.	Verify the change in machine-type and the tags added by navigating to the VM Instances on the Cloud Console and clicking the terraform instance created. 

### Destroy the infrastructure
You have now seen how to build and change infrastructure. Before moving on to creating multiple resources and showing resource dependencies, you will see how to completely destroy your Terraform-managed infrastructure.
1.	Execute the following command. Answer yes to execute this plan and destroy the infrastructure:
```
terraform destroy
```
2.	Verify that the instance terraform no longer exists by navigating to the VM Instances on the Cloud Console.

