
# Setting up Dockerr on new VM
Installing docker on the new VM
Firstly update ubuntu
apt-get upgrade
Click 'y' to perform the upgrade.

You will be logged in as an admin user. Example miu-admin
run the following command to install. sudo apt-get install docker-ce docker-ce-cli containerd.io


Verify installation was successful by running the following hello-world image 
sudo docker run hello-world

Configure docker to start on boot
sudo systemctl enable docker

Configure docker to run without sudo 
sudo groupadd docker
sudo usermod -aG docker $USER



# New Features!

 



### Tech



### Installation

### Plugins


### Development


### Docker
