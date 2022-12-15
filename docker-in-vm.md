Docker prereqs for vanilla [Debian 11] VM

https://docs.docker.com/engine/install/debian/

sudo apt-get remove docker docker-engine docker.io containerd runc

sudo apt-get update

sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# yes, we need to run this again to update local docker apt repository
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

#### TEST ####
sudo docker run hello-world



[tested the above and works correctly on GCP VM]


Install git:
sudo apt-get install git

Clone app repository:
git clone https://github.com/WebToLearn/fx-trading-app.git

Build docker image (adding an appropriate tag):
cd fx-trading-app/App/quote-service/
sudo docker build . --tag quote-service:0.0.1

Check new image is available locally:
sudo docker images

Example output:
REPOSITORY      TAG                 IMAGE ID       CREATED              SIZE
quote-service   0.0.1               6b3bdd98ddee   About a minute ago   284MB
<none>          <none>              c691a1fc1ad1   About a minute ago   482MB
hello-world     latest              feb5d9fea6a5   14 months ago        13.3kB
maven           3.6.2-jdk-11-slim   f90eccee82af   3 years ago          418MB
openjdk         11.0.4-jre          fa6d3c4702db   3 years ago          267MB

Start container, mapping the Spring boot defaul port to host VM:
sudo docker run -p 8220:8220 quote-service:0.0.1


