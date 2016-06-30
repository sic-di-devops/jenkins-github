FROM jenkins

USER root

RUN apt-get update && apt-get -y install apt-transport-https ca-certificates \
    && apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D \
    && echo "deb https://apt.dockerproject.org/repo debian-jessie main" >> /etc/apt/sources.list.d/docker.list \
    && apt-get update && apt-get -y install docker-engine bc patch\
    && curl -L https://github.com/docker/compose/releases/download/1.7.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose \
    && wget https://shunit2.googlecode.com/files/shunit2-2.1.6.tgz -P /usr/local/ \
    && tar zxvf /usr/local/shunit2-2.1.6.tgz -C /usr/local/ \ 
    && wget https://storage.googleapis.com/google-code-attachments/shunit2/issue-16/comment-10/shunit-2.1.6-xml.patch -P /usr/local/  \
    && patch -u -p1 -d /usr/local/shunit2-2.1.6 < /usr/local/shunit-2.1.6-xml.patch

ENV SHUNIT_HOME /usr/local/shunit2-2.1.6

COPY plugins.txt /usr/share/jenkins/ref/
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/ref/plugins.txt
