FROM php:5.6-apache
MAINTAINER Potato Powered Software <support@potatopowered.net>

# update apt-get 
RUN apt-get update

# install the required components 
RUN apt-get install -y libmcrypt-dev g++ libicu-dev libmcrypt4 libicu52 zlib1g-dev git

# install the PHP extensions we need 
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install mcrypt
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install intl
RUN docker-php-ext-install zip

#####ADD ADDITIONAL INSTALLS OR MODULES BELOW######### 
#####ADD ADDITIONAL INSTALLS OR MODULES ABOVE######### 

# cleanup after the installations 
RUN apt-get purge --auto-remove -y libmcrypt-dev g++ libicu-dev zlib1g-dev
# delete the lists for apt-get as the take up space we do not need. 
RUN rm -rf /var/lib/apt/lists/*

# install composer globally so that you can call composer directly 
RUN curl -sSL https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

# install xdebug for remote debug 
RUN curl -L -o /tmp/xdebug-2.3.3.tgz http://xdebug.org/files/xdebug-2.3.3.tgz \
    && tar xfz /tmp/xdebug-2.3.3.tgz \
    && rm -r /tmp/xdebug-2.3.3.tgz \
    && mv xdebug-2.3.3 /usr/src/php/ext/xdebug \
    && docker-php-ext-install xdebug

# enable apache rewrite 
RUN a2enmod rewrite

# set www permissions 
RUN usermod -u 1000 www-data
