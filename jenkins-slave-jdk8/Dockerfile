FROM jenkins/jnlp-slave
MAINTAINER Larry Tin <dev@goodow.com>

USER root

RUN apt-get update && apt-get install -y --no-install-recommends \
    apt-transport-https \
    maven \
    && rm -rf /var/lib/apt/lists/*

# Install docker
RUN curl -sSL https://get.docker.com/ | sh && \
    apt-get purge -y docker-engine && \
    apt-get install docker-ce

RUN curl -L https://github.com/docker/compose/releases/download/1.21.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose && \
	chmod +x /usr/local/bin/docker-compose

RUN usermod -aG docker jenkins

# Install kubectl
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
RUN chmod +x ./kubectl
RUN mv ./kubectl /usr/local/bin/kubectl

COPY maven-settings.xml .m2/settings.xml
RUN chown -R jenkins .m2

USER jenkins

