FROM ubuntu:latest

MAINTAINER Cesar L

ARG DEBIAN_FRONTEND=noninteractive

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get update && apt-get install -y locales \
    && locale-gen en_US.UTF-8 \
    && dpkg-reconfigure locales

RUN apt-get update && apt-get install -y gnupg tzdata \
    && echo "UTC" > /etc/timezone \
    && dpkg-reconfigure -f noninteractive tzdata

RUN apt-get update \
    && apt-get install -y curl zip unzip git supervisor software-properties-common \
    && apt-get install -y php-fpm php-cli php-json php-common \
       php-mysql php-zip php-gd php-mbstring \
       php-curl php-xml php-pear php-bcmath \
       php-memcached php-imap php-soap \
       php-xdebug \
       php-msgpack php-igbinary \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && mkdir /run/php \
    && apt-get remove -y --purge software-properties-common \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY xdebug.ini /etc/php/7.4/mods-available/xdebug.ini

COPY start-container /usr/local/bin/start-container
RUN chmod +x /usr/local/bin/start-container

EXPOSE 80
CMD ["start-container"]

