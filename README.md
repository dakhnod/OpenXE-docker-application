# OpenXE Docker application

This repository provides a fast way to launch everything needed to run OpenXE inside Docker, including nginx, php-fpm and mariadb.
Everything is preconfigured, except for OpenXE itself.

## Running

After cloning/downloading this repository, inside of it run `docker compose up -d`. This will build all containers, launch them, put them in an own network. You need to know nginx's ip to access it.

To use port localhost:80 (for example), type 
```
docker compose up -d php-fpm mariadb
docker compose run -p 80:80 -d nginx
```
instead. The OpenXE instance will then be available on [http://localhost](http://localhost).

The Database host is `mariadb`, the database is `openxe`, user `openxe` and password `openxe`.