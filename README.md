 ---------------------------------

# | Mes Tâches : pour le 15/07/2025 |

----------------------------------

## _OBJECTIFS:_

    - Install Jenkins,
    - configure Docker as agent,
    - set up cicd, 
    - deploy applications to k8s and much more.

# ----------*************-------------------------

# ----------*************-------------------------

### 1- création serveur Ubuntu

AWS EC2 Instance
    Go to AWS Console
    Instances(running)
    Launch instances

### 2- installation de java 11

 sudo apt update
      sudo apt install openjdk-17-jre

### 3- installation de Jenkins

 Pre-Requisites:
          Java (JDK)
Apres installation de java on peut de suite installer les Jenkins

   curl -fsSL <https://pkg.jenkins.io/debian/jenkins.io-2023.key> | sudo tee \
   /usr/share/keyrings/jenkins-keyring.asc > /dev/null
 echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
   <https://pkg.jenkins.io/debian> binary/ | sudo tee \
   /etc/apt/sources.list.d/jenkins.list > /dev/null
    sudo apt-get update
    sudo apt-get install Jenkins

**Note:** By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS.
Open port 8080 in the inbound traffic rules as show below.

   **EC2 > Instances > Click on
    In the bottom tabs -> Click on Security
    Security groups
    Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed All traffic).**

### 4- création de premier pipeline

- Install the Docker Pipeline plugin (voir 6)
- Click the New Item menu within Jenkins
- Provide a name for your new item (e.g. My-Pipeline) and select Multibranch Pipeline

### 5- création d'un job + Jenkins file

### 6- Jenkins agents vs agent docker Jenkins

 Install the Docker Pipeline plugin in Jenkins:
 ***
    Log in to Jenkins.
    Go to Manage Jenkins > Manage Plugins.
    In the Available tab, search for "Docker Pipeline".
    Select the plugin and click the Install button.
    Restart Jenkins after the plugin is installed.
    ***

Docker Slave Configuration
 sudo apt update
 sudo apt install docker.io
Grant Jenkins user and Ubuntu user permission to docker deamon.
 sudo su -
 usermod -aG docker jenkins
 usermod -aG docker ubuntu
 systemctl restart docker
Once you are done with the above steps, it is better to restart Jenkins.
http://<ec2-instance-public-ip>:8080/restart
The docker agent configuration is now successful.

### 7- projets à réaliser : définition d'un pipeline de a-z + commentaire sur le projet (video)
