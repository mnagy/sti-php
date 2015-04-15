FROM openshift/httpd-24-centos7

# This image provides an Apache+PHP environment for running PHP
# applications.

MAINTAINER Ben Parees <bparees@redhat.com>

# Image metadata
ENV PHP_VERSION           5.5
ENV IMAGE_DESCRIPTION     PHP 5.5
ENV IMAGE_TAGS            php,php55
ENV IMAGE_EXPOSE_SERVICES 8080:http

# Install PHP
USER root
RUN yum install -y \
    https://www.softwarecollections.org/en/scls/rhscl/php55/epel-7-x86_64/download/rhscl-php55-epel-7-x86_64.noarch.rpm && \
    yum install -y --setopt=tsflags=nodocs php55 php55-php && \
    yum clean all -y && \
    mkdir -p /opt/openshift/www/php && chown -R default.default /opt/openshift/www && \
    chown -R root.default /opt/rh/php55/root/var/lib/php/*

# Copy the STI scripts from the specific language image to /usr/local/sti
COPY ./.sti/bin/ /usr/local/sti

# Each language image must have 'contrib' directory with extra files needed to
# run and build the applications.
COPY ./contrib/ /opt/openshift
RUN chown -R default:default /opt/openshift

# Set the default CMD to print the usage of the language image
CMD ["usage"]

USER default
