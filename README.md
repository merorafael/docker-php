Docker: PHP and extensions
==========================

Official [PHP docker image](https://hub.docker.com/_/php/) with additional extensions.

Supported tags
--------------

| PHP Version | Type    | Tags                                            |
| ----------- | ------- | ----------------------------------------------- |
| 7.1.1       | CLI     | `7.1-cli`, `7-cli`, `cli`, `7.1`, `7`, `latest` |
| 7.1.1       | FPM     | `7.1-fpm`, `7-fpm`, `fpm`                       |
| 7.1.1       | Apache  | `7.1-apache`, `7-apache`, `apache`              |
| 7.1.1       | ZTS     | `7.1-zts`, `7-zts`, `zts`                       |
| 7.0.15      | CLI     | `7.0-cli`, `7.0`                                |
| 7.0.15      | FPM     | `7.0-fpm`                                       |
| 7.0.15      | Apache  | `7.0-apache`                                    |
| 7.0.15      | ZTS     | `7.0-zts`                                       |
| 5.6.30      | CLI     | `5.6-cli`, `5-cli`, `5.6`, `5`                  |
| 5.6.30      | FPM     | `5.6-fpm`, `5-fpm`                              |
| 5.6.30      | Apache  | `5.6-apache`, `5-apache`                        |
| 5.6.30      | ZTS     | `5.6-zts`, `5-zts`                              |

Extensions enabled
------------------

- mcrypt
- iconv
- intl
- mbstring
- gd
- curl
- dom
- soap
- simplexml
- xmlreader
- xmlwriter
- sockets
- zip
- pgsql
- mysqli
- oci8
- sqlsrv *(PHP 7.0 or above)*
- pdo_sqlsrv *(PHP 7.0 or above)*
- pdo_pgsql
- pdo_mysql
- pdo_oci
- pdo_dblib
- pdo_sqlite
- memcached
- redis
- simplexml
- apcu
- opcache
- ftp
- gearman *(PHP 5.6 only)*

Extras
------

- composer
- phpunit
- wget
- vim
- git
- unzip
