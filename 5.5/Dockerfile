FROM openshift/base-centos7

# This image provides an Apache+PHP environment for running PHP
# applications.

MAINTAINER Ben Parees <bparees@redhat.com>

# Image metadata
ENV PHP_VERSION           5.5
ENV IMAGE_DESCRIPTION     PHP 5.5
ENV IMAGE_TAGS            php,php55
ENV IMAGE_EXPOSE_SERVICES 8080:http

# Install Apache httpd and PHP
RUN yum install -y \
    https://www.softwarecollections.org/en/scls/rhscl/httpd24/epel-7-x86_64/download/rhscl-httpd24-epel-7-x86_64.noarch.rpm \
    https://www.softwarecollections.org/en/scls/rhscl/php55/epel-7-x86_64/download/rhscl-php55-epel-7-x86_64.noarch.rpm && \
    yum install -y --setopt=tsflags=nodocs httpd24 php55 php55-php && \
    yum clean all -y

ENV PATH $PATH:/opt/rh/php55/root/usr/bin

USER root

EXPOSE 8080


# These instruction triggers the instructions at a later time, when the image
# is used as the base for another build.
#
# Copy the STI scripts from the specific language image to /usr/local/sti
COPY ./.sti/bin/ /usr/local/sti

# Each language image must have 'contrib' directory with extra files needed to
# run and build the applications.
COPY ./contrib/ /opt/openshift
RUN chown -R default:default /opt/openshift
