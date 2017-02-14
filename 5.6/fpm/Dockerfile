FROM php:5.6-fpm

# Get repository and install wget and vim
RUN apt-get update && apt-get install --no-install-recommends -y \
        wget \
        vim \
        git \
        unzip

# Add PostgreSQL repository
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main" > /etc/apt/sources.list.d/pgdg.list
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | \
      apt-key add -

# Install Oracle Instantclient
RUN mkdir /opt/oracle \
    && cd /opt/oracle \
    && wget https://s3.amazonaws.com/merofile/instantclient-basic-linux.x64-12.1.0.2.0.zip \
    && wget https://s3.amazonaws.com/merofile/instantclient-sdk-linux.x64-12.1.0.2.0.zip \
    && unzip /opt/oracle/instantclient-basic-linux.x64-12.1.0.2.0.zip -d /opt/oracle \
    && unzip /opt/oracle/instantclient-sdk-linux.x64-12.1.0.2.0.zip -d /opt/oracle \
    && ln -s /opt/oracle/instantclient_12_1/libclntsh.so.12.1 /opt/oracle/instantclient_12_1/libclntsh.so \
    && ln -s /opt/oracle/instantclient_12_1/libclntshcore.so.12.1 /opt/oracle/instantclient_12_1/libclntshcore.so \
    && ln -s /opt/oracle/instantclient_12_1/libocci.so.12.1 /opt/oracle/instantclient_12_1/libocci.so \
    && rm -rf /opt/oracle/*.zip


# Install PHP extensions deps
RUN apt-get update \
    && apt-get install --no-install-recommends -y \
        postgresql-server-dev-9.5 \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        zlib1g-dev \
        libicu-dev \
        g++ \
        unixodbc-dev \
        libxml2-dev \
        libaio-dev \
        libgearman-dev \
        libmemcached-dev \
        freetds-dev \
	libssl-dev \
	openssl

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- \
        --install-dir=/usr/local/bin \
        --filename=composer

# Install PHP extensions
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && echo 'instantclient,/opt/oracle/instantclient_12_1/' | pecl install oci8-2.0.10 \
    && docker-php-ext-configure pdo_oci --with-pdo-oci=instantclient,/opt/oracle/instantclient_12_1,12.1 \
    && docker-php-ext-configure pdo_dblib --with-libdir=/lib/x86_64-linux-gnu \
    && pecl install apcu-4.0.10 \
    && pecl install redis-2.2.8 \
    && pecl install gearman \
    && pecl install memcached-2.2.0 \
    && docker-php-ext-install \
            iconv \
            mbstring \
            intl \
            mcrypt \
            gd \
            pgsql \
            mysqli \
            pdo_pgsql \
            pdo_mysql \
            pdo_oci \
            pdo_dblib \
            soap \
            sockets \
            zip \
            pcntl \
            ftp \
    && docker-php-ext-enable \
            oci8 \
            apcu \
            memcached \
            redis \
            gearman \
            opcache

# Install PHPUnit
RUN wget https://phar.phpunit.de/phpunit.phar -O /usr/local/bin/phpunit \
    && chmod +x /usr/local/bin/phpunit

# Clean repository
RUN apt-get clean \
    && rm -rf /var/lib/apt/lists/*
