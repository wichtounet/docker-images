FROM scratch

MAINTAINER Baptiste Wicht

# Download a stage3 tarball
ADD http://distfiles.gentoo.org/releases/amd64/autobuilds/current-stage3-amd64-hardened+nomultilib/stage3-amd64-hardened-20150604.tar.bz2 /
#ADD stage3-amd64-hardened.tar.xz /

# Set the runlevel
RUN echo "default" > /run/openrc/softlevel

# Setup the rc_sys
RUN sed -e 's/#rc_sys=""/rc_sys="lxc"/g' -i /etc/rc.conf

# Make sure the network is statted
RUN ln -s /etc/init.d/net.lo /run/openrc/started/net.lo
RUN ln -s /etc/init.d/net.lo /etc/init.d/net.eth0
RUN ln -s /etc/init.d/net.eth0 /run/openrc/started/net.eth0

# By default, UTC system
RUN echo 'Europe/Zurich' > /etc/timezone

# Setup the portage directory and permissions
ONBUILD RUN mkdir -p /usr/portage/{distfiles,metadata,packages}
ONBUILD RUN chown -R portage:portage /usr/portage
ONBUILD RUN echo "masters = gentoo" > /usr/portage/metadata/layout.conf

# Sync portage
ONBUILD RUN emerge-webrsync -q

# Update the environment
ONBUILD RUN env-update
