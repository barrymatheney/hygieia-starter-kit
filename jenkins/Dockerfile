#FROM jenkins/jenkins:lts
FROM jenkins/jenkins:lts-jdk11
ARG JENKINS_HOME='/var/jenkins_home'
USER root
RUN apt-get update && apt-get install -y  wget git nano inetutils-ping \
&& cd /usr/local && wget https://download.java.net/openjdk/jdk11/ri/openjdk-11+28_linux-x64_bin.tar.gz && tar -zxvf openjdk-11+28_linux-x64_bin.tar.gz && rm openjdk-11+28_linux-x64_bin.tar.gz \
&& cd /usr/local && wget https://dlcdn.apache.org/maven/maven-3/3.8.3/binaries/apache-maven-3.8.3-bin.tar.gz && tar -zxvf apache-maven-3.8.3-bin.tar.gz && rm apache-maven-3.8.3-bin.tar.gz

ARG MAVEN_HOME='/usr/local/apache-maven-3.8.3'
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

COPY conf/. /root/.m2/
COPY id_rsa/. /root/.ssh/
COPY --chown=jenkins:jenkins conf/. "${JENKINS_HOME}/.m2/"
COPY --chown=jenkins:jenkins id_rsa/. "${JENKINS_HOME}/.ssh/"

RUN  git config --global user.email "nobody@nowhere.com"  && \
  git config --global user.name "Dummy Name"  && \
  chmod 644 /root/.ssh/id_rsa.pub && chmod 600 /root/.ssh/id_rsa  && \
  chmod 644 ${JENKINS_HOME}/.ssh/id_rsa.pub && chmod 600 ${JENKINS_HOME}/.ssh/id_rsa 

ENV PATH "${MAVEN_HOME}/bin:${PATH}"
RUN printenv | sort  