FROM php:5.6-apache

LABEL version="1.0" maintainer="vsc55@cerebelum.net" description="Docker Apache + PHP 5.6 + Client MySQL + Imagick + zip + exif + gd + ldap"

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

RUN apt-get update --fix-missing; \
    apt-get install -y libmagickwand-dev --no-install-recommends; \
    rm -rf /var/lib/apt/lists/*; \
    pecl install imagick; \
    docker-php-ext-enable imagick; \
	apt-get purge -y --auto-remove libmagickwand-dev;

RUN apt-get update --fix-missing; \
    apt-get install -y libzip-dev zip --no-install-recommends; \
    rm -rf /var/lib/apt/lists/*; \
    docker-php-ext-install zip; \
	apt-get purge -y --auto-remove libzip-dev;

RUN apt-get update --fix-missing; \
    apt-get install -y exiftool --no-install-recommends; \
    rm -rf /var/lib/apt/lists/*; \
    docker-php-ext-install exif;

RUN apt-get update --fix-missing; \
	apt-get install -y libgd-dev libfreetype6-dev libjpeg62-turbo-dev libpng-dev --no-install-recommends; \
	rm -rf /var/lib/apt/lists/*; \
	docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/; \
	docker-php-ext-install gd; \
	apt-get purge -y --auto-remove libgd-dev libfreetype6-dev libjpeg62-turbo-dev libpng-dev;

RUN apt-get update --fix-missing; \
	apt-get install -y libldap2-dev --no-install-recommends; \
	rm -rf /var/lib/apt/lists/*; \
	docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/; \
	docker-php-ext-install ldap; \
	apt-get purge -y --auto-remove libldap2-dev;

RUN apt-get update --fix-missing; \
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
