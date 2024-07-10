FROM dunglas/frankenphp

ENV SERVER_NAME="https://www.project.local"

RUN apt update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    git \
    unzip
    #librabbitmq-dev
    #libpq-dev
    #supervisor

# Installe les dépendances nécessaires
RUN install-php-extensions \
    pdo \
    pdo_mysql \
    gd \
    intl \
    zip \
    opcache \
    mbstring \
    dom
    #sockets \
    #redis \
    #amqp

RUN cp $PHP_INI_DIR/php.ini-development $PHP_INI_DIR/php.ini; \
    sed -i 's/variables_order = "GPCS"/variables_order = "EGPCS"/' $PHP_INI_DIR/php.ini;

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

COPY ./Caddyfile /etc/caddy/Caddyfile

WORKDIR /srv
