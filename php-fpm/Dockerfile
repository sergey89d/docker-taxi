ARG PHP_VERSION=8.2

FROM php:${PHP_VERSION}-fpm-alpine

ARG GROUP_ID
ARG GROUP_NAME
ARG USER_ID
ARG USER_NAME

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN chmod +x /usr/local/bin/install-php-extensions && install-php-extensions intl http ctype pdo pdo_mysql zip calendar dom mbstring xml xsl iconv dom fileinfo gd json

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Create system user to run Composer and Artisan Commands
#RUN chown -R $USER_NAME:$USER_NAME /var/www/html/
RUN chown -R www-data:www-data /var/www/html

RUN if [ "$GROUP_ID" != "0" ] ; then addgroup -g $GROUP_ID $GROUP_NAME ; fi
RUN if [ "$GROUP_ID" != "0" ] ; then adduser --uid $USER_ID -G $GROUP_NAME -D $USER_NAME ; fi

USER $USER_NAME

WORKDIR /var/www/html/
