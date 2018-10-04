FROM jenkins/jenkins:lts
USER root

# SSH instalaltion and configartion related to Azure Web App SSH Login##

RUN apt-get update -y
RUN apt-get install openssh-server -y
RUN echo "root:Docker!" | chpasswd \
    && echo "cd /home" >> /etc/bash.bashrc

COPY sshd_config /etc/ssh/
#####SSH Installation and configration Completed##

### Define Jenkins root direcotry as Environment varible, we can choose any location Jenkins will work with having root directory location dependency ##
ENV JENKINS_HOME /var/jenkins_home

# making sym-link to prestent jenkins data### 
RUN ln -s /var/jenkins_home /home/jenkins_home

# for JenkinsUI web interface Port:
EXPOSE 8080

EXPOSE 2222

# for jenkins slave agents Port:
EXPOSE 50000

COPY jenkins.sh /usr/local/bin/jenkins.sh

ENTRYPOINT ["/usr/local/bin/jenkins.sh"]