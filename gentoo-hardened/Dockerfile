FROM scratch

MAINTAINER Baptiste Wicht

# Unpack stage3
ADD stage3-amd64-hardened.tar.bz2 /

# Set the runlevel
RUN echo "default" > /run/openrc/softlevel

# Setup the rc_sys
RUN sed -e 's/#rc_sys=""/rc_sys="lxc"/g' -i /etc/rc.conf

# Make sure the network is statted
RUN ln -s /etc/init.d/net.lo /run/openrc/started/net.lo
RUN ln -s /etc/init.d/net.lo /etc/init.d/net.eth0
RUN ln -s /etc/init.d/net.eth0 /run/openrc/started/net.eth0

# Set the timezone
RUN echo 'Europe/Zurich' > /etc/timezone

# Setup the portage directory and permissions
RUN mkdir -p /usr/portage/{distfiles,metadata,packages}
RUN chown -R portage:portage /usr/portage
RUN echo "masters = gentoo" > /usr/portage/metadata/layout.conf

# Sync portage
RUN emerge-webrsync -q

# Update the environment
RUN env-update

# Sync portage again on build
ONBUILD RUN emerge-webrsync -q

# Update the environment again on build
ONBUILD RUN env-update
