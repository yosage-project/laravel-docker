# ベースとするイメージファイル
FROM php:8.2-fpm

# ここから下に必要なセットアップ情報を記載していく

RUN apt update
RUN apt install -y zip unzip libcairo2-dev

RUN docker-php-ext-install pdo_mysql

# composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin


