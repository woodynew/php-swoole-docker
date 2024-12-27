FROM phpswoole/swoole:php8.3-alpine

# Composer - https://getcomposer.org/download/
ARG COMPOSER_VERSION="2.8.4"
ARG COMPOSER_SUM="c4c4e2e1beab0ea04e0bd042a5dbba9feda1fbf5eda0d36203958edd343c0a8a"

ADD --chmod=0755 https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

# Install dependencies
RUN set -eux \
    && apk add --no-cache \
    tzdata 

# 在此处添加其他扩展：
RUN install-php-extensions \
    opcache \
    lz4 \
    ssh2 \
    uuid \
    vips \
    bcmath \
    bz2 \
    calendar \
    Core \
    ctype \
    curl \
    date \
    dba \
    dom \
    exif \
    FFI \
    fileinfo \
    filter \
    ftp \
    gd \
    gettext \
    gmp \
    hash \
    iconv \
    igbinary \
    imagick \
    imap \
    intl \
    json \
    ldap \
    libxml \
    mbstring \
    mongodb \
    mysqli \
    mysqlnd \
    openssl \
    pcntl \
    pcre \
    PDO \
    pdo_mysql \
    pdo_pgsql \
    pdo_sqlite \
    pgsql \
    Phar \
    posix \
    random \
    readline \
    redis \
    Reflection \
    session \
    shmop \
    SimpleXML \
    soap \
    sockets \
    sodium \
    SPL \
    sqlite3 \
    standard \
    sysvmsg \
    sysvsem \
    sysvshm \
    tokenizer \
    xml \
    xmlreader \
    xmlwriter \
    xsl \
    zip \
    zlib \
    zstd \
    xlswriter \
    grpc


RUN set -eux \
    # Fix php.ini settings for enabled extensions
    && chmod +x "$(php -r 'echo ini_get("extension_dir");')"/* \
    # Shrink binaries
    && (find /usr/local/bin -type f -print0 | xargs -n1 -0 strip --strip-all -p 2>/dev/null || true) \
    && (find /usr/local/lib -type f -print0 | xargs -n1 -0 strip --strip-all -p 2>/dev/null || true) \
    && (find /usr/local/sbin -type f -print0 | xargs -n1 -0 strip --strip-all -p 2>/dev/null || true) \
    && true

# Install Composer
RUN set -eux \
    && curl -LO "https://getcomposer.org/download/${COMPOSER_VERSION}/composer.phar" \
    && echo "${COMPOSER_SUM}  composer.phar" | sha256sum -c - \
    && chmod +x composer.phar \
    && mv composer.phar /usr/local/bin/composer \
    && composer --version \
    && true

RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
