Docker: PHP and extensions
==========================

Official [PHP docker image](https://hub.docker.com/_/php/) with additional extensions.

Supported tags
--------------

- [`7.1-cli`, `7-cli`, `cli`, `7.1`, `7`, `latest`](7.1/Dockerfile)
- [`7.1-fpm`, `7-fpm`, `fpm`](7.1/fpm/Dockerfile)
- [`7.1-apache`, `7-apache`, `apache`](7.1/apache/Dockerfile)
- [`7.1-zts`, `7-zts`, `zts`](7.1/zts/Dockerfile)
- [`7.0-cli`, `7.0`](7.0/Dockerfile)
- [`7.0-fpm`](7.0/fpm/Dockerfile)
- [`7.0-apache`](7.0/apache/Dockerfile)
- [`7.0-zts`](7.0/zts/Dockerfile)
- [`5.6-cli`, `5-cli`, `5.6`, `5`](5.6/Dockerfile)
- [`5.6-fpm`, `5-fpm`](5.6/fpm/Dockerfile)
- [`5.6-apache`, `5-apache`](5.6/apache/Dockerfile)
- [`5.6-zts`, `5-zts`](5.6/zts/Dockerfile)
- [`5.4-cli`, `5.4`](5.4/Dockerfile)
- [`5.4-fpm`](5.4/fpm/Dockerfile)
- [`5.4-apache`](5.4/apache/Dockerfile)
- [`5.4-zts`](5.4/zts/Dockerfile)

Extensions enabled
------------------

| Extension   | PHP 5.4 | PHP 5.6 | PHP 7.0 | PHP 7.1 |
| ----------- | ------- | ------- | ------- | ------- |
| mcrypt      |    x    |    x    |    x    |    x    |
| iconv       |    x    |    x    |    x    |    x    |
| intl        |    x    |    x    |    x    |    x    |
| mbstring    |    x    |    x    |    x    |    x    |
| gd          |    x    |    x    |    x    |    x    |
| curl        |    x    |    x    |    x    |    x    |
| dom         |    x    |    x    |    x    |    x    |
| soap        |    x    |    x    |    x    |    x    |
| simplexml   |    x    |    x    |    x    |    x    |
| xmlreader   |    x    |    x    |    x    |    x    |
| xmlwriter   |    x    |    x    |    x    |    x    |
| sockets     |    x    |    x    |    x    |    x    |
| zip         |    x    |    x    |    x    |    x    |
| pgsql       |    x    |    x    |    x    |    x    |
| mysqli      |    x    |    x    |    x    |    x    |
| sqlsrv¹     |         |         |    x    |    x    |
| pdo_pgsql   |    x    |    x    |    x    |    x    |
| pdo_mysql   |    x    |    x    |    x    |    x    |
| pdo_sqlsrv¹ |         |         |    x    |    x    |
| pdo_dblib   |    x    |    x    |    x    |    x    |
| pdo_sqlite  |    x    |    x    |    x    |    x    |
| memcached   |    x    |    x    |    x    |    x    |
| redis       |    x    |    x    |    x    |    x    |
| apcu        |    x    |    x    |    x    |    x    |
| opcache     |    x    |    x    |    x    |    x    |
| ftp         |    x    |    x    |    x    |    x    |
| xdebug      |    x    |    x    |    x    |    x    |

¹ Microsoft only provides support SQL Server for PHP 7.0 or above.

Extras
------

- composer
- phpunit
- wget
- vim
- git
- unzip

About Oracle extensions
-----------------------

In this version, the extensions `pdo_oci` and `oci` have been remove.
This change happened because these extensions depend on `Oracle Instant Client`. 

To download this package, the user will need a login and password on the Oracle portal.
 
Including Oracle extensions
---------------------------

Create a `Dockerfile` extending some `merorafael/php` image.
**Example:**
```
FROM merorafael/php:7.1-fpm
```

Use the commands below to install `Oracle Instant Client` on the container.

**Attention!** You need change versions referecences and replace `<ORALCE_INSTANT_CLIENT_URL>`
with `Oracle Instant Client` download URL.

```
# Install Oracle Instantclient
RUN mkdir /opt/oracle \
    && cd /opt/oracle \
    && wget <ORACLE_INSTANT_CLIENT_URL> \
    && wget <ORACLE_INSTANT_CLIENT_URL> \
    && unzip /opt/oracle/instantclient-basic-linux.x64-12.1.0.2.0.zip -d /opt/oracle \
    && unzip /opt/oracle/instantclient-sdk-linux.x64-12.1.0.2.0.zip -d /opt/oracle \
    && ln -s /opt/oracle/instantclient_12_1/libclntsh.so.12.1 /opt/oracle/instantclient_12_1/libclntsh.so \
    && ln -s /opt/oracle/instantclient_12_1/libclntshcore.so.12.1 /opt/oracle/instantclient_12_1/libclntshcore.so \
    && ln -s /opt/oracle/instantclient_12_1/libocci.so.12.1 /opt/oracle/instantclient_12_1/libocci.so \
    && rm -rf /opt/oracle/*.zip
```

Install `OCI8` and `PDO_OCI` using the commands bellow.

```
# Install Oracle extensions
RUN docker-php-ext-configure pdo_oci --with-pdo-oci=instantclient,/opt/oracle/instantclient_12_1,12.1 \
       && echo 'instantclient,/opt/oracle/instantclient_12_1/' | pecl install oci8 \
       && docker-php-ext-install \
               pdo_oci \
       && docker-php-ext-enable \
               oci8
```

Now just build the image and use it in your containers.

#### Complete `Dockerfile` example

```
FROM merorafael/php:7.1-fpm

# Install Oracle Instantclient
RUN mkdir /opt/oracle \
    && cd /opt/oracle \
    && wget <ORACLE_INSTANT_CLIENT_URL> \
    && wget <ORACLE_INSTANT_CLIENT_URL> \
    && unzip /opt/oracle/instantclient-basic-linux.x64-12.1.0.2.0.zip -d /opt/oracle \
    && unzip /opt/oracle/instantclient-sdk-linux.x64-12.1.0.2.0.zip -d /opt/oracle \
    && ln -s /opt/oracle/instantclient_12_1/libclntsh.so.12.1 /opt/oracle/instantclient_12_1/libclntsh.so \
    && ln -s /opt/oracle/instantclient_12_1/libclntshcore.so.12.1 /opt/oracle/instantclient_12_1/libclntshcore.so \
    && ln -s /opt/oracle/instantclient_12_1/libocci.so.12.1 /opt/oracle/instantclient_12_1/libocci.so \
    && rm -rf /opt/oracle/*.zip
    
# Install Oracle extensions
RUN docker-php-ext-configure pdo_oci --with-pdo-oci=instantclient,/opt/oracle/instantclient_12_1,12.1 \
       && echo 'instantclient,/opt/oracle/instantclient_12_1/' | pecl install oci8 \
       && docker-php-ext-install \
               pdo_oci \
       && docker-php-ext-enable \
               oci8
```
