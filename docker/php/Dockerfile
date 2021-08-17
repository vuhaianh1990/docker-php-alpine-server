FROM php:fpm-alpine
# WORKDIR "/WWW"
EXPOSE 9000 22

RUN apk add --no-cache openssh git supervisor nodejs nodejs-npm \
    && sed -i s/#PermitRootLogin.*/PermitRootLogin\ yes/ /etc/ssh/sshd_config \
    && echo "root:root" | chpasswd

RUN docker-php-ext-install mysqli pdo pdo_mysql

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

RUN apk add --no-cache $PHPIZE_DEPS \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug

RUN ssh-keygen -A

RUN mkdir -p /etc/supervisor.d
COPY supervisord.conf /etc/supervisord.conf
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
