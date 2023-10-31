# Jenkins CICD Pipleline

## Installation on EC2 Instance

Install Jenkins, configure Docker as agent, set up cicd, deploy applications to k8s and much more.

## AWS EC2 Instance

Go to AWS Console

Instances(running)

Launch instances
![image](https://github.com/lakshmir2023/CICD/assets/141936877/fad43909-b6ef-4577-9d8a-0e595f838423)

## Install Jenkins.

Pre-Requisites:

Java (JDK) 

## Run the below commands to install Java and Jenkins

Install Java

<br> sudo apt update
<br> sudo apt install openjdk-11-jre

Verify Java is Installed
<br> java -version
![image](https://github.com/lakshmir2023/CICD/assets/141936877/6e11e2e0-f2c6-4c79-8be7-387fc5b05f90)

Now, you can proceed with installing Jenkins

<br> curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
<br> echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
<br> sudo apt-get update
<br> sudo apt-get install jenkins

## **Note: ** By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 8080 in the inbound traffic rules as show below.

EC2 > Instances > Click on

In the bottom tabs -> Click on Security

Security groups

Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed All traffic).
![image](https://github.com/lakshmir2023/CICD/assets/141936877/470e61c5-8a20-4ee7-8b6e-bb3d14c60a76)

## Login to Jenkins using the below URL:
http://:8080 [You can get the ec2-instance-public-ip-address from your AWS EC2 console page]

Note: If you are not interested in allowing All Traffic to your EC2 instance 1. Delete the inbound traffic rule for your instance 2. Edit the inbound traffic rule to only allow custom TCP port 8080

After you login to Jenkins, - Run the command to copy the Jenkins Admin Password - sudo cat /var/lib/jenkins/secrets/initialAdminPassword - Enter the Administrator password
![image](https://github.com/lakshmir2023/CICD/assets/141936877/753f8545-e925-4618-a179-4ba2fc93c252)

## Click on Install suggested plugins
![image](https://github.com/lakshmir2023/CICD/assets/141936877/ae812fb8-be85-419e-ae71-de47b5dbd778)

Wait for the Jenkins to Install suggested plugins
![image](https://github.com/lakshmir2023/CICD/assets/141936877/68a5345c-f4a9-4619-bb59-1fd6b16a5a0b)

Create First Admin User or Skip the step [If you want to use this Jenkins instance for future use-cases as well, better to create admin user]
![image](https://github.com/lakshmir2023/CICD/assets/141936877/17f63718-6eb0-4cd8-b20d-fc0c54bcf83a)

Jenkins Installation is Successful. You can now starting using the Jenkins
![image](https://github.com/lakshmir2023/CICD/assets/141936877/062491db-f4a5-4d10-8f92-01c49a1d9a79)

## Install the Docker Pipeline plugin in Jenkins:
Log in to Jenkins.
Go to Manage Jenkins > Manage Plugins.
In the Available tab, search for "Docker Pipeline".
Select the plugin and click the Install button.
Restart Jenkins after the plugin is installed.
![image](https://github.com/lakshmir2023/CICD/assets/141936877/c8f67e49-1412-4551-b802-9424d43ca513)

Wait for the Jenkins to be restarted.

## Docker Slave Configuration

Run the below command to Install Docker
<br> sudo apt update
<br> sudo apt install docker.io

## Grant Jenkins user and Ubuntu user permission to docker deamon.

sudo su - 
<br> usermod -aG docker jenkins
<br> usermod -aG docker ubuntu
<br> systemctl restart docker

Once you are done with the above steps, it is better to restart Jenkins.

http://<ec2-instance-public-ip>:8080/restart

The docker agent configuration is now successful.
