Jenkins webapp for container 
We took https://github.com/jenkinsci/docker as base image for the installation of Jenkins and modified with our requirements .

Ssh configuration

Base image doesn’t have the ssh installed so modified the docker file to install the ssh service and configured login to our Azure webapp for contianer.

RUN apt-get install openssh-server -y

RUN echo "root:Docker!" | chpasswd \

&& echo "cd /home" >> /etc/bash.bashrc

COPY sshd_config /etc/ssh/ 

After build and deployment of image completed jenkins will ask for adminstarator passowrd which is stored in jenkins contianer by accesing ssh we will copy that password 
and login into jenkinsUI

In below location we will get jenkins admin passowrd , after instalaltion we can create a seperate user from jenkinsUI

/home/Jenkins/XX 

** base image used Jenkins user for logging and in our docker file we used root as user to login to the container.
Volume Persistent
To make our azure file persistent added a symbolic link to Jenkins root folder to /home/jenikins_home –Azure container volume

ln -s /var/jenkins_home /home/jenkins_home

After installation we need to install initial plugins.

Issues 
 Encountered some issues like 403 No valid crumb was included in the request, ssh failure ,backup plugin issue

followed https://stackoverflow.com/questions/44711696/spinnaker-403-no-valid-crumb-was-included-in-the-request -  To resolve issue.

Ssh issue

Ssh login failed sometimes because of the outdated plugin. we updated ssh plugin from jenkinsUI -To resolve issue



