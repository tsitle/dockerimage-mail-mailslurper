FROM scratch

ARG CF_DEBIAN_VERSION
ARG CF_CPUARCH_DEB_ROOTFS

ENV DEBIAN_FRONTEND=noninteractive

# add Debian root-fs
ADD cache/debian_stretch/rootfs-debian_stretch_${CF_DEBIAN_VERSION}-${CF_CPUARCH_DEB_ROOTFS}.tar.xz /

RUN \
	apt-get update \
	&& apt-get --assume-yes upgrade \
	&& apt-get --assume-yes dist-upgrade

#

ARG CF_CPUARCH_DEB_DIST

ARG CF_MS_VERSION

# add mailslurper package to image
ADD files/mailslurper-${CF_MS_VERSION}-${CF_CPUARCH_DEB_DIST}.tgz /opt/

#
RUN \
	ln -s /opt/mailslurper-${CF_MS_VERSION}-${CF_CPUARCH_DEB_DIST} /opt/mailslurper \
	#
	&& apt-get --quiet --yes autoclean \
	&& apt-get --quiet --yes autoremove \
	&& apt-get --quiet --yes clean \
	&& rm -rf \
			/usr/share/man \
			/usr/share/doc \
			/usr/share/icons \
			/usr/share/poppler \
			/usr/share/mime \
			/var/lib/apt/lists*

#
ENV DEBIAN_FRONTEND=newt

WORKDIR /opt/mailslurper

ENTRYPOINT ["/opt/mailslurper/mailslurper"]
