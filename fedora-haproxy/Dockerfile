# Based on the Fedora image
FROM fedora

# File Author / Maintainer
MAINTAINER http://fedoraproject.org/wiki/Cloud

# Install Squid
RUN dnf -y update && dnf clean all
RUN dnf -y install haproxy && dnf clean all

# Change the first occurrence squid.conf to auth_squid.conf
# if you would like to use authentication
ADD haproxy.cfg /etc/haproxy/haproxy.cfg
ADD resolv.conf /etc/resolv.conf
RUN chown -R haproxy.haproxy /etc/haproxy


# Expose ports
EXPOSE 3128 

# Set the default command to execute
# when creating a new container
CMD /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg -p /run/haproxy.pid
