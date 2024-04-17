FROM debian:bullseye
ENV DEBIAN_FRONTEND noninteractive
# Install packages needed for SSH and interactive OS
RUN apt-get update && \
    apt-get -y install \
        openssh-server \
        passwd \
        sudo \
        man-db \
        curl \
        wget \
        vim-tiny && \
    apt-get -qq clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* 

# Enable ssh for vagrant
RUN systemctl enable ssh.service; 
EXPOSE 22

# Create the vagrant user
RUN useradd -m -G sudo -s /bin/bash vagrant && \
    echo "vagrant:vagrant" | chpasswd && \
    echo 'vagrant ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers.d/vagrant && \
    chmod 440 /etc/sudoers.d/vagrant

# Establish ssh keys for vagrant
RUN mkdir -p /home/vagrant/.ssh; \
    chmod 700 /home/vagrant/.ssh
ADD https://raw.githubusercontent.com/hashicorp/vagrant/master/keys/vagrant.pub /home/vagrant/.ssh/authorized_keys
RUN chmod 600 /home/vagrant/.ssh/authorized_keys; \
    chown -R vagrant:vagrant /home/vagrant/.ssh

VOLUME ["/sys/fs/cgroup", "/tmp", "/run"]
CMD ["/lib/systemd/systemd"]
