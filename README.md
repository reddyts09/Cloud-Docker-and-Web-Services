# Docker and Web Services
Since we have now created a WebService in HW2 and Weather APP in HW3, this Project will have me migrate that WebService into a dockercontainer instance, that makes hosting services much more easier

# Configuration Details:
1. To connect to the aws cloud service:
- ssh -i "red.pem" ubuntu@ec2-3-17-59-123.us-east-2.compute.amazonaws.com

2. After logging in:
- sudo apt-get update 
- sudo apt-get install python3-pip python3-dev python3-setuptools git
- sudo apt-get install language-pack-en
- sudo locale-gen en_GB.UTF-8

3. Install Django and djangorestframework
- pip3 install django
- pip3 install djangorestframework
- pip3 install django-import-export

4. Use git command to clone the project from github to var folder:
- sudo -i
- cd /var
- git clone https://github.com/reddyts09/cloud234G.git

5. Prerequisites for installing Docker:
- First, in order to ensure the downloads are valid, add the GPG key for the official Docker repository to your system:
  ```
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
- Add the Docker repository to APT sources: 
  ```
  sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
- Next, update the package database with the Docker packages from the newly added repo: 
  ```
  sudo apt-get update
- Make sure you are about to install from the Docker repo instead of the default Ubuntu 16.04 repo: 
  ```
  apt-cache policy docker-ce
- Finally, install Docker: 
  ```
  sudo apt-get install -y docker-ce
- Docker should now be installed, the daemon started, and the process enabled to start on boot. Check that it's running: 
  ```
  sudo systemctl status docker

6. Steps for building Docker image:
- To check the existing image:
  ```
  docker ps
- To create a new image: 
  ```
  docker commit  94e814e2efa8  project1:1.0  --> project1:1.0
- create a folder in /var directory:
  ```
  mkdir /var/doc_folder/
- create file "Dockerfile" in /var/doc_folder/ abd paste the following contents:
  ```FROM project1:1.0
     USER root
     ADD cloud234G /var/cloud234
     ADD startme.sh startme.sh
     ENTRYPOINT ["sh", "startme.sh"]
- Copy the Django application cloud234G in /var/doc_folder directory using git clone command:
  ```
  git clone https://github.com/reddyts09/cloud234G.git
- Build the docker image:
  ```
  docker build  -t project1:1.0 .  --> cloud234:1.0
- create startme.sh file in  /var/doc_folder/ and copy the below contents in startme.sh:
  ```#!/bin/bash
     nohup python3 /var/ccpro1/manage.py runserver 0.0.0.0:80
- Save into tgz file:
  ```
  docker save cloud234:1.0 > cloud234.tgz

7. Link to the google dive for cloud234.tgz and follow the steps below:
- https://drive.google.com/drive/folders/1A1egtTAJ78rUd0HJjX7unlSQB6XuHjdB?usp=sharing
- docker load -i cloud234.tgz
- docker run -d -p 8081:80 cloud234:1.0
- http://ec2-3-17-59-123.us-east-2.compute.amazonaws.com:8081/ or http://ec2-3-17-59-123.us-east-2.compute.amazonaws.com/
  
# Built With
- Django,AWS: Web Framework used
- DOCKER for making hosting services much simpler
- Github: repository for code

# Acknowledgements
I Thank Prof.Giridhar for provding me with the opportunity to work on this project that deals with hands on experience with Cloud, AWS, Docker and Django framework.
