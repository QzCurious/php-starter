FROM php:7.4-fpm-alpine

# Install composer
#RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install extensions
#RUN docker-php-ext-install bcmath

# Update
RUN apk update && apk upgrade
RUN apk add bash neovim
#RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

# Add user for laravel application
RUN addgroup --gid 1000 www
RUN adduser --uid 1000 --shell /bin/bash --ingroup www --disabled-password www

# Copy existing application directory contents
#COPY --chown=www:www . /var/www/html
WORKDIR /var/www/html/public

# Change current user to www
USER www

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]
