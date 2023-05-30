FROM php:7.4-apache

RUN apt-get update -y

RUN pecl install mongodb && docker-php-ext-enable mongodb

RUN apt-get update && apt-get install -y git zip unzip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www/html

COPY /mongodb-crud-php-record /var/www/html

RUN echo "<DIRECTORY /var/www/html>\n Options Indexes FollowSymlinks\n AllowOverride All\n Require all granted\n </DIRECTORY>" | tee -a >> /etc/apache2/apache2.conf

RUN composer install --no-dev

RUN composer update

RUN chown -R www-data:www-data /var/www/html

RUN chmod -R 755 /var/www/html

EXPOSE 80

RUN a2enmod rewrite

CMD ["apache2ctl", "-DFOREGROUND"]

