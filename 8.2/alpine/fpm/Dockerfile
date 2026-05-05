FROM docker.io/library/php:8.2-fpm-alpine

# 1. Set working directory
WORKDIR /var/www/html

# 2. Add composer
COPY --from=docker.io/library/composer:latest /usr/bin/composer /usr/local/bin/composer

# 3. Group installations and clean up build dependencies to drastically reduce image size
RUN apk add --no-cache --virtual .build-deps \
        $PHPIZE_DEPS \
        postgresql-dev \
    && apk add --no-cache \
        zip \
        libzip-dev \
        libjpeg-turbo-dev \
        libpng-dev \
        libwebp-dev \
        freetype-dev \
        git \
        curl \
        oniguruma-dev \
        libpq \
    && docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp \
    && docker-php-ext-install -j$(nproc) \
        gd \
        pdo \
        pdo_mysql \
        pdo_pgsql \
        zip \
        mbstring \
        exif \
        pcntl \
        bcmath \
        calendar \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && apk del .build-deps \
    && rm -rf /tmp/pear \
    && rm -rf /var/cache/apk/*

CMD ["php-fpm", "-y", "/usr/local/etc/php-fpm.conf", "-R"]
