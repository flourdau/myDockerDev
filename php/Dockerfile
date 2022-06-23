FROM php:8.1.7-apache

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf
RUN a2enmod rewrite && service apache2 restart

ADD .upDate /var/.upDate
RUN sh /var/.upDate

RUN apt-get install -y --no-install-recommends \
    locales apt-utils git libicu-dev g++ libpng-dev libxml2-dev libzip-dev libonig-dev libxslt-dev unzip libpq-dev nodejs npm wget \
    apt-transport-https lsb-release ca-certificates

RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen  \
    &&  echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen \
    &&  locale-gen

RUN pecl install xdebug-3.1.3 \
    && pecl install apcu \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-enable apcu \
    && echo "xdebug.mode=debug" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.client_host=host.docker.internal" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN curl -sS https://getcomposer.org/installer | php -- \
    &&  mv composer.phar /usr/local/bin/composer

RUN curl -sS https://get.symfony.com/cli/installer | bash \
    &&  mv /root/.symfony/bin/symfony /usr/local/bin


RUN npm install --global yarn

RUN git config --global user.email "lourdaux.florian.pro.com" \
    &&  git config --global user.name "Florian LOURDAUX"

CMD echo YOUPI && tail -f /dev/null

WORKDIR /var/www/
