flarum3xt/vagrant
===
[![Join the chat at https://gitter.im/flarum3xt](https://img.shields.io/gitter/room/nwjs/nw.js.svg)](https://gitter.im/flarum3xt/Lobby)

A vagrant script for [Flarum Skeleton][flarum-app].   

Main features
---

- [x] Base on Ubuntu Xenial 64bit
- [x] Installing NGINX
- [x] Installing MariaDB 10.x
- [x] Installing Redis server
- [x] Installing PHP 7.0 FPM
- [x] Installing NodeJS 6.x
- [x] Making database for Flarum application

#### Directories structure

```
/
|-- app
|   |-- config
|   |-- log
|   |-- script
|   `-- source
`-- vagrant
```

Requirements
---

* [Vagrant 1.9+][vagrant]

Usage
---

#### Create project

Using `composer` to create new project:

```shell
$ composer create-project flarum/flarum . --stability=beta
```
Read the [Installation Guide][install-guide] for more information.


#### Change configurations for vagrant script

Change your configurations and recipes in `Vagrantfile`

```ruby
my = {
  :cf_box_version           => "20161214.0.1"      ,
  :cf_hostname              => "flarum.dev"        ,
  :cf_timezone              => "UTC"               ,
  :cf_private_ip            => "10.10.10.10"       ,
  :cf_private_key_path      => "~/.ssh/id_rsa"     ,
  :cf_public_key_path       => "~/.ssh/id_rsa.pub" ,
  :cf_app_source_path       => "../app"            ,

  # configuration for nginx or httpd service
  :cf_http_port             => 80                  ,
  :cf_http_user             => "www-data"          ,
  :cf_http_group            => "www-data"          ,

  # configuration for basic authentication
  :cf_basic_auth_enabled    => true                ,
  :cf_basic_auth_user       => "dev"               ,
  :cf_basic_auth_password   => "devpass"           ,

  # configuration for php-fpm service
  :cf_php_fpm_listen        => "/run/php/php7.0-fpm.sock",

  # configuration for mysqld service
  :cf_mariadb_root_password => "rootpass"          ,
  :cf_mariadb_port          => 3306                ,
  :cf_mariadb_remote_access => true                ,

  # configuration for redis-server service
  :cf_redis_port            => 6379                ,
  :cf_redis_remote_access   => true                ,

  # configuration for forwarded_port
  :cf_host_port_ssh         => 50022               ,
  :cf_host_port_http        => 50080               ,
  :cf_host_port_mariadb     => 53306               ,
  :cf_host_port_redis       => 56379               ,
};

recipes = [
  "common.sh",
  "nginx.sh",
  "mariadb.sh",
  "redis.sh",
  "php70.sh",
  "nodejs.sh",
  "cleanup.sh",
  "flarum.sh",
];
```

#### Make virtual machine

```shell
$ vagrant up
```

Open web browser with address http://127.0.0.1:50080 and install application (only the first time).

#### Database configuration:

- Host: **localhost**   
- Port: **3306**   
- User: **flarum**   
- Pass: **flarum**   
- Name: **flarum**   

Changelog
---
See all change logs in [CHANGELOG.md](CHANGELOG.md)

Contributing
---
All code contributions must go through a pull request and approved by
a core developer before being merged. This is to ensure proper review of all the code.

Fork the project, create a feature branch, and send a pull request.

If you would like to help take a look at the [list of issues](issues).

License
---
This project is released under the MIT License.   
Copyright © 2017 Flarum3xt Team.   
Please see [License File](LICENSE.md) for more information.

[vagrant]:       https://www.vagrantup.com/downloads.html
[flarum-app]:    https://github.com/flarum/flarum
[install-guide]: http://flarum.org/docs/installation
