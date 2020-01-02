ARG CF_DEBIAN_RELEASE
ARG CF_DEBIAN_VERSION
ARG CF_CPUARCH_DEB_DIST

FROM tsle/os-debian-${CF_DEBIAN_RELEASE}-${CF_CPUARCH_DEB_DIST}:${CF_DEBIAN_VERSION}

ENV DEBIAN_FRONTEND=noninteractive

RUN \
	apt-get update \
	&& apt-get upgrade -y \
	&& apt-get dist-upgrade -y

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
ENV DEBIAN_FRONTEND=dialog

WORKDIR /opt/mailslurper

ENTRYPOINT ["/opt/mailslurper/mailslurper"]
