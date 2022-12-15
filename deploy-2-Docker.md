# Install and configure docker on a Debian 11 host 

Official documentation used: https://docs.docker.com/engine/install/debian/

Connect to the VM running in Google Cloud using the 'SSH' button. This will open a new broser window to it's console. Run the following commands:

- Make sure to remove any existing previous docker installation)
```
sudo apt-get remove docker docker-engine docker.io containerd runc
```

- Update the local apt repository (default debian one)
```
sudo apt-get update
```

- Install prerequisites for adding official docker certificates and apt repo
```
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

- Add docker gpg key
```
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

- Add the official docker apt repository on local machine
```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

- Update the package sources list and install docker
```
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

- Run the sample container to make sure all works fine

```
sudo docker run hello-world
```
Sample output:
  `Hello from Docker!`
  `This message shows that your installation appears to be working correctly.`

<br/>

# Build and deploy the application in a docker container

- First install git:
```
sudo apt-get install git
```

- Clone application repository:
```
git clone https://github.com/WebToLearn/fx-trading-app.git
```

- Build docker image (adding an appropriate tag):
```
cd fx-trading-app/App/quote-service/
sudo docker build . --tag quote-service:0.0.1
```

- Check new image is available locally:
```
sudo docker images
```

Example output:
```
REPOSITORY      TAG                 IMAGE ID       CREATED              SIZE
quote-service   0.0.1               6b3bdd98ddee   About a minute ago   284MB
<none>          <none>              c691a1fc1ad1   About a minute ago   482MB
hello-world     latest              feb5d9fea6a5   14 months ago        13.3kB
maven           3.6.2-jdk-11-slim   f90eccee82af   3 years ago          418MB
openjdk         11.0.4-jre          fa6d3c4702db   3 years ago          267MB
```

- Start container, mapping the Spring boot defaul port to host VM:
```
sudo docker run -p 8220:8220 quote-service:0.0.1
```

- From a separate SSH session to the same VM, test that the application works correcty:
```
curl http://localhost:8220/currencies
```
Application should provide a json response, similar to `["EUR","USD","GBP","RON"]`

<br/>

### Optional

You can map the container port onto a different port on the host. This would allow using default http/https ports and also match some firewall rules in the cloud, allowing external connections - for example from you local PC, via curl and even browser.

```
sudo docker run -p 80:8220 quote-service:0.0.1
```

To test the connection, copy the VMs `external IP` and use that from a network outside your GCP project. 
