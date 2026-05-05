# Use a PHP image with FPM and Alpine for small size
FROM php:8.2-fpm-alpine

# Install system dependencies and required PHP extensions for Symfony
RUN apk add --no-cache \
    git \
    curl \
    libzip-dev \
    icu-dev \
    postgresql-dev \
    supervisor \
    # Install common extensions
    && docker-php-ext-install pdo pdo_pgsql opcache intl zip

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Set working directory
WORKDIR /var/www/html

# Copy custom php.ini settings
COPY php.ini /usr/local/etc/php/conf.d/custom.ini

# Copy Symfoni CLI
COPY --link \
    --from=ghcr.io/symfony-cli/symfony-cli:latest \
    /usr/local/bin/symfony /usr/local/bin/symfony

# Expose port for PHP-FPM
EXPOSE 9000

# Default command to run PHP-FPM
CMD ["php-fpm"]