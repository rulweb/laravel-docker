FROM php:7.4.3-fpm

# Установка редис
RUN pecl install -o -f redis && rm -rf /tmp/pear

# Текущая дериктория
WORKDIR /var/www

# Установка зависимостей
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y git zip unzip curl libzip-dev libpq-dev \
    libonig-dev libxslt-dev libfreetype6-dev libjpeg-dev cron supervisor

# Очистка кеша
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Установка нужных PHP расширений
RUN docker-php-ext-install gd pdo pdo_pgsql xsl mbstring zip opcache pcntl intl

# Конфигурирование PHP расширений
RUN docker-php-ext-configure gd
RUN docker-php-ext-configure zip
RUN docker-php-ext-configure intl
RUN docker-php-ext-enable redis

# Устанавливаем композер
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN mkdir -p /var/log/supervisor

COPY crontab /etc/cron.d/cron_web
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY php.ini /usr/local/etc/php/conf.d/php.ini

EXPOSE 9000

CMD ["/usr/bin/supervisord"]
