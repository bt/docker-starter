FROM phusion/baseimage:latest

MAINTAINER "Bertram Truong" <b@bertramtruong.com>

# Set local country
ARG APT_MIRROR_COUNTRY=au
ENV APT_MIRROR_COUNTRY ${APT_MIRROR_COUNTRY}
RUN sed -i -e s/archive/"$APT_MIRROR_COUNTRY"\.archive/g /etc/apt/sources.list

ENV DEBIAN_FRONTEND noninteractive
ENV PATH /usr/local/rvm/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# Install beanstalkd
RUN apt-get update && \
    apt-get install -y beanstalkd && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

VOLUME /var/lib/beanstalkd/data

EXPOSE 11300

CMD ["/usr/bin/beanstalkd"]
