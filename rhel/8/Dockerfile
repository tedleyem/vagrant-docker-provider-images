# Manifest Digest
# registry.access.redhat.com/ubi8/ubi@sha256:edc34f89cf9c818c2fb28b8ea1780f384db563ce4293dc0ab8e73ec01791e5af

FROM ubi:8.9-1160
RUN yum -y update; yum clean all && \
    yum -y install openssh-server openssh-clients passwd sudo; yum clean all 

RUN mkdir /var/run/sshd; \
    ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N ''; \
    systemctl enable sshd.service; \
    sed -i '/^session.*pam_loginuid.so/s/^session/# session/' /etc/pam.d/sshd; \
    sed -i 's/Defaults.*requiretty/#Defaults requiretty/g' /etc/sudoers; \
    rm /usr/lib/tmpfiles.d/systemd-nologin.conf;

RUN useradd --create-home -s /bin/bash vagrant; \
    echo -e "vagrant\nvagrant" | (passwd --stdin vagrant); \
    echo 'vagrant ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers.d/vagrant; \
    chmod 440 /etc/sudoers.d/vagrant

RUN mkdir -p /home/vagrant/.ssh; \
    chmod 700 /home/vagrant/.ssh
ADD https://raw.githubusercontent.com/hashicorp/vagrant/master/keys/vagrant.pub /home/vagrant/.ssh/authorized_keys
RUN chmod 600 /home/vagrant/.ssh/authorized_keys; \
    chown -R vagrant:vagrant /home/vagrant/.ssh

VOLUME ["/sys/fs/cgroup", "/tmp", "/run"]
CMD ["/lib/systemd/systemd"]
