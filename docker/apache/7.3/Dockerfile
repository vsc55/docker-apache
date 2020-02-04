FROM php:7.3-apache

LABEL version="1.0" maintainer="vsc55@cerebelum.net" description="Docker Apache + PHP 7.3"

RUN a2enmod headers; \
    a2enmod proxy_http; \
    a2enmod rewrite; \
    a2enmod vhost_alias; \
    a2enmod remoteip; \
    a2enmod ssl; \
    a2enmod ldap; \
    a2enmod dav; \
    a2enmod dav_fs; \
    docker-php-ext-install mysqli; \
	docker-php-ext-install imagick;

RUN chmod 777 -R /var/www; \
    chown -R www-data:www-data /var/www; \
    usermod -u 1000 www-data; \
    chsh -s /bin/bash www-data;

RUN ln -sf /dev/stdout /var/log/apache2/access.log; \
    ln -sf /dev/stderr /var/log/apache2/error.log;
