FROM jenkins/jenkins:lts-centos
USER root
RUN dnf update -y && dnf install -y 'dnf-command(config-manager)' && \
dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo && \
dnf list docker-ce && \
dnf update && \
dnf install docker-ce --nobest -y && \
dnf clean all
RUN usermod -a -G docker jenkins
USER jenkins
ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"
ENV JENKINS_USER admin
ENV JENKINS_PASS admin
COPY plugins.txt /usr/share/jenkins/ref/

# COPY security.groovy /usr/share/jenkins/ref/init.groovy.d/
COPY default-user.groovy /usr/share/jenkins/ref/init.groovy.d/
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt
