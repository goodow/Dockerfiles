FROM node
MAINTAINER larrytin "dev@goodow.com"

RUN npm install -g typescript

RUN apt-get update && apt-get install -y --no-install-recommends \
    openssh-server \
    && mkdir /var/run/sshd && echo 'root:root' |chpasswd \
    && rm -rf /var/lib/apt/lists/*

RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]

WORKDIR /root/dev