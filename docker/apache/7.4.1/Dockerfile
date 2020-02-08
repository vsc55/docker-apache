FROM php:7.4.1-apache

LABEL version="1.0" maintainer="vsc55@cerebelum.net" description="Docker Apache + PHP 7.4.1 + Client MySQL + Imagick"

RUN a2enmod headers; \
    a2enmod proxy_http; \
    a2enmod rewrite; \
    a2enmod vhost_alias; \
    a2enmod remoteip; \
    a2enmod ssl; \
    a2enmod ldap; \
    a2enmod dav; \
    a2enmod dav_fs;

RUN docker-php-ext-install mysqli;

RUN apt-get update; \
    apt-get install -y libmagickwand-dev --no-install-recommends; \
    rm -rf /var/lib/apt/lists/*; \
    pecl install imagick; \
    docker-php-ext-enable imagick;

RUN apt-get update; \
    apt-get install -y msmtp --no-install-recommends; \
    rm -rf /var/lib/apt/lists/*; \
    echo 'sendmail_path = "/usr/bin/msmtp -t"' > /usr/local/etc/php/conf.d/msmtp.ini;
    
RUN chmod 777 -R /var/www; \
    chown -R www-data:www-data /var/www; \
	chown -R www-data:www-data /var/log/apache2; \
    usermod -u 1000 www-data; \
    chsh -s /bin/bash www-data; \
    ln -sf /dev/stdout /var/log/apache2/access.log; \
    ln -sf /dev/stderr /var/log/apache2/error.log;
