FROM php:7.2-apache
COPY php.ini /usr/local/etc/php/
COPY ssl.conf /etc/apache2/sites-available/ssl.conf
RUN apt-get update \
  && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
  && docker-php-ext-install pdo_mysql mysqli mbstring gd iconv

RUN mkdir -p /etc/apache2/ssl_keys

RUN openssl genrsa -out /etc/apache2/ssl_keys/server.key 2048
RUN openssl req -new -key /etc/apache2/ssl_keys/server.key -out /etc/apache2/ssl_keys/server.csr -subj '/C=JP/ST=Tokyo/L=Tokyo/O=Example Ltd./OU=Web/CN=localhost'
RUN openssl x509 -in /etc/apache2/ssl_keys/server.csr -days 3650 -req -signkey /etc/apache2/ssl_keys/server.key -out /etc/apache2/ssl_keys/server.crt

RUN a2enmod ssl
RUN a2ensite ssl

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]