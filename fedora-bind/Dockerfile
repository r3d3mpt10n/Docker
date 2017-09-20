# Based on the Fedora image
FROM fedora

# File Author / Maintainer
MAINTAINER Shep

RUN rm -f /etc/yum.repos.d/*.repo
ADD fedora.repo /etc/yum.repos.d/
ADD fedora-updates.repo /etc/yum.repos.d/
ADD resolv.conf /etc/resolv.conf
RUN cat /etc/yum.repos.d/*.repo

# Install BIND
RUN dnf -y update && dnf clean all
RUN dnf -y install bind && dnf clean all
RUN dnf -y install bind-utils && dnf clean all
RUN mkdir /var/named/zones

#Gen BIND keys
RUN rndc-confgen -a -c /etc/rndc.key
RUN chown named:named /etc/rndc.key

# if you would like to use authentication
ADD named.conf /etc/named.conf
ADD zones.conf /etc/named/zones.conf
ADD bne-home.net /var/named/zones/bne-home.net
RUN chown named:named /etc/named/zones.conf
RUN chown -R named:named /var/named
RUN chown named:named /etc/named.conf
# Expose ports
EXPOSE 53

# Set the default command to execute
# when creating a new container
CMD /usr/sbin/named -u named -f
