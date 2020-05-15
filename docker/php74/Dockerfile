# image
FROM php:7.4-apache

# Install pdo_mysql
RUN docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli

RUN apt-get install -y apache2

# authorize apache to write in the virtualhost
RUN a2enmod rewrite

# restart apache for the new configuration
RUN service apache2 restart

# Some needed library
RUN apt-get update \
    && apt-get install -y --no-install-recommends locales apt-utils git;

#Comment this line if you don't use Reactjs or just yarn packages
RUN apt install -y nodejs npm

#Comment this line if you don't use Reactjs or just yarn packages
RUN npm install -y -g yarn

# get locals
# if you aren't French you can change the second line with your local language
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen && \
    locale-gen

# copy php.ini
COPY ./docker/php74/php.ini /usr/local/etc/php/php.ini

# dl & move composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
   && apt-get update && apt-get install -y git libzip-dev unzip\
   && docker-php-ext-install zip \
   && a2enmod rewrite headers

COPY . /var/www

# root directory (on the right in the docker-compose, MUST BE THE SAME !) 
WORKDIR /var/www

#Adding apache .htaccesss
RUN composer require symfony/apache-pack

#Uncomment for WINDOWS; create & add user here the docker-machine
#RUN addgroup --system default --gid 1000 && adduser --system default --uid 1000 --ingroup default

RUN composer install

#Comment this line if you don't use Reactjs or just yarn packages
RUN yarn install 