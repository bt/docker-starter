FROM phusion/baseimage:latest

MAINTAINER "Bertram Truong" <b@bertramtruong.com>

# Set local country
ARG APT_MIRROR_COUNTRY=au
ENV APT_MIRROR_COUNTRY ${APT_MIRROR_COUNTRY}
RUN sed -i -e s/archive/"$APT_MIRROR_COUNTRY"\.archive/g /etc/apt/sources.list

# Initialize APT package manager
RUN apt-get update -y && \
    apt-get install -y curl software-properties-common

# HHVM repository
RUN curl -o - http://dl.hhvm.com/conf/hhvm.gpg.key | apt-key add - && \
    echo deb http://dl.hhvm.com/ubuntu xenial main | tee /etc/apt/sources.list.d/hhvm.list

# Install HHVM
RUN apt-get update -y \
    && apt-get install -y hhvm \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /var/www/public
RUN usermod -u 1000 www-data

COPY server.ini /etc/hhvm/server.ini

WORKDIR /var/www/

CMD ["/usr/bin/hhvm", "-m", "server", "-c", "/etc/hhvm/server.ini"]

EXPOSE 9000
