FROM alpine:3.13

RUN apk add --no-cache \
    tini curl php8-cli php8-fpm \
    php8-ctype php8-curl php8-dom php8-ffi php8-iconv php8-intl php8-mbstring php8-opcache php8-pcntl php8-phar php8-posix php8-session php8-simplexml php8-tokenizer php8-xml \
    php8-pdo php8-pdo_mysql php8-pdo_sqlite
RUN ln -s /usr/bin/php8 /usr/local/bin/php

RUN curl -L -o /usr/local/bin/symfony https://github.com/symfony/cli/releases/download/v4.23.5/symfony_linux_amd64 \
    && chmod +x /usr/local/bin/symfony

RUN curl -L -o /usr/local/bin/composer https://getcomposer.org/composer-stable.phar \
    && chmod +x /usr/local/bin/composer

COPY --chown=root:root ./etc/php8/php-fpm.conf /etc/php8/php-fpm.conf
COPY --chown=root:root ./etc/php8/php-fpm.d/www.conf /etc/php8/php-fpm.d/www.conf

EXPOSE 9000
WORKDIR /srv
ENTRYPOINT ["/sbin/tini", "--"]
CMD ["/usr/sbin/php-fpm8", "--fpm-config", "/etc/php8/php-fpm.conf"]
