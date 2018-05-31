FROM golang
MAINTAINER sheltonliu "sheltonliu@tencent.com"

RUN apt-get update && apt-get install -y --no-install-recommends openssh-server 
    && mkdir /var/run/sshd \
    #&& useradd -m developer && echo 'developer:aiot' |chpasswd \
    && echo 'root:aiot' |chpasswd \
    #&& echo 'chown developer /go' > /etc/profile.d/init.sh \
    #&& echo 'export PATH=$PATH:/user/local/go/bin' >> /etc/profile.d/init.sh \
    && rm -rf /var/lib/apt/lists/*

#RUN sed -ri 's/export PATH/export PATH=\/user\/local\/go\/bin:$PATH/' /etc/profile
RUN sed -ri 's/^#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]