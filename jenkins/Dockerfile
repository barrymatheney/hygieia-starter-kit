#FROM jenkins/jenkins:lts
FROM jenkins/jenkins:lts-jdk11
USER root
# RUN apt-get update && apt-get install -y maven
#&& cd /usr/local && wget https://download.java.net/openjdk/jdk11/ri/openjdk-11+28_linux-x64_bin.tar.gz && tar -zxvf openjdk-11+28_linux-x64_bin.tar.gz && rm openjdk-11+28_linux-x64_bin.tar.gz

#RUN git clone https://github.com/hygieia/hygieia-publisher-jenkins-plugin \
#&& cd hygieia-publisher-jenkins-plugin \
# &&  mvn test \
# &&  mvn package 


#FROM jenkins/jenkins:lts-jdk11
COPY config.xml /usr/share/jenkins/ref/config.xml
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt
RUN echo 2.0 > /usr/share/jenkins/ref/jenkins.install.UpgradeWizard.state
COPY jobs/ /usr/share/jenkins/ref/jobs
