# Create a VM in Google Cloud

The most basic component in GCP, but most other cloud ecosystems as well, is the Virtual Machine. This replicates a physical server (with CPU, memory, disk, networking, etc) inside the internal network, corresponding to your GCP project.

Let's start with creating a new on so we can deploy one of the applications in fx-trading project.

Using the left hand side menu (three horizontal lines), select the following:
```
Compute Engine -> VM Instances
Create an instance -> New VM instance
```
Use the following details, leaving all else at default:
```
Name: fx-trading-host
Region: europe-west3 (Frankfurt)
Zone: europe-west3-c
Machine family: GENERAL-PURPOSE
Series: E2
Machine-type: e2-medium (2vCPU, 4 GB memory)
Do not select 'Enable display device'

Boot disk
Type: New balanced persistent disk
Size: 10 GB
Image: Debian GNU/Linux 11 (bullseye)

Enable both:
    Allow HTTP traffic
    Allow HTTPS traffic
```

Leave all other values as default and Click `CREATE`

Wait for the VM to boot up and when it is ready click on the SSH button right next to it.

<br/>

# Deploy the quotes-service application

First we need to install some prerequisites to build the Spring Boot application.

- Update the local apt package sources
```
sudo apt update
```

- Install openjdk, with a version matching what is defined in the pom.xml
```
sudo apt install -y openjdk-11-jdk
```

- Install git, required to fetch the application sources from github
```
sudo apt install -y git
```

- Fetch the github project to a local workspace
```
mkdir github && cd github
git clone https://github.com/WebToLearn/fx-trading-app.git
```

- Build the application and package it as jar file
```
cd fx-trading-app/App/quote-service/
chmod 755 mvnw
./mvnw package -Pprod -DskipTests
```

- Start the quote-service application
```
java -jar target/quote-service-0.0.1-SNAPSHOT.jar
```

- Open a second SSH window to the same host and try to see if the application reponds to http requests
```
curl http://localhost:8220/currencies
```


## Optional

Change the spring boot default port to 80, rebuild the application and restart it. Now you should be able to access it from your local PC, using the VMs `external ip`

