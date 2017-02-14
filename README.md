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

Extensions enabled
------------------

| Extension   | PHP 5.6 | PHP 7.0 | PHP 7.1 |
| ----------- | ------- | ------- | ------- |
| mcrypt      |    x    |    x    |    x    |
| iconv       |    x    |    x    |    x    |
| intl        |    x    |    x    |    x    |
| mbstring    |    x    |    x    |    x    |
| gd          |    x    |    x    |    x    |
| curl        |    x    |    x    |    x    |
| dom         |    x    |    x    |    x    |
| soap        |    x    |    x    |    x    |
| simplexml   |    x    |    x    |    x    |
| xmlreader   |    x    |    x    |    x    |
| xmlwriter   |    x    |    x    |    x    |
| sockets     |    x    |    x    |    x    |
| zip         |    x    |    x    |    x    |
| pgsql       |    x    |    x    |    x    |
| mysqli      |    x    |    x    |    x    |
| oci8        |    x    |    x    |    x    |
| sqlsrv¹     |         |    x    |    x    |
| pdo_pgsql   |    x    |    x    |    x    |
| pdo_mysql   |    x    |    x    |    x    |
| pdo_oci     |    x    |    x    |    x    |
| pdo_sqlsrv¹ |         |    x    |    x    |
| pdo_dblib   |    x    |    x    |    x    |
| pdo_sqlite  |    x    |    x    |    x    |
| memcached   |    x    |    x    |    x    |
| redis       |    x    |    x    |    x    |
| apcu        |    x    |    x    |    x    |
| opcache     |    x    |    x    |    x    |
| ftp         |    x    |    x    |    x    |

¹ Microsoft only provides support SQL Server for PHP 7.0 or above.

Extras
------

- composer
- phpunit
- wget
- vim
- git
- unzip
