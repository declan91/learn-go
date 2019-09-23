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

switch to root user 
sudo su - 

When docker is first installed, a user named postgres will be created. We need to setup the DB password on this user. 
As root user run the command passwd postgres
You will be prompted to type the new password twice. 

Switch to the postgres user by typing su - postgres



Installing postgres if required:
To see if the postgres is installed correctly run the command postgres help.
If you see a help menu it is installed. 








# New Features!

 



### Tech



### Installation

### Plugins


### Development


### Docker
