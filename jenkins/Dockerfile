FROM jenkins

USER root

RUN apt-get update -y &&\
    apt-get install -y sudo &&\
    apt-get install -y lxc &&\
    rm -rf /var/lib/apt/lists/*
	
RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers

RUN curl -O https://bootstrap.pypa.io/get-pip.py
RUN sudo python get-pip.py
RUN sudo pip install awscli
RUN sudo pip install docker-compose

USER jenkins

ENV INSTALL_DIR=/install

# Entrypoint to setup volume mounts
COPY jenkins_entrypoint.sh ${INSTALL_DIR}/jenkins_entrypoint.sh
RUN sudo chown -R jenkins:jenkins  ${INSTALL_DIR}
RUN sudo chmod -R 700 ${INSTALL_DIR}

# For later, if we want to install plugins
# USER jenkins
# COPY plugins.txt /usr/share/jenkins/plugins.txt
# RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt


ENTRYPOINT ${INSTALL_DIR}/jenkins_entrypoint.sh