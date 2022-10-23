# docker-phpmyadmin
A documentation on installing phpmyadmin via docker (Mac M1 only)

## Install Docker
- [Register a new account](https://hub.docker.com/signup) or [Signin an existing account](https://login.docker.com/u/login/identifier?state=hKFo2SBoSDBFNUxTSlVuelF4R2E5WlFWaUVWcGtHMVo4SUdpLaFur3VuaXZlcnNhbC1sb2dpbqN0aWTZIGgwTzM0VTQ5NGExUXhid196MUcyUVJJbHRRSDhURVlPo2NpZNkgbHZlOUdHbDhKdFNVcm5lUTFFVnVDMGxiakhkaTluYjk)
- [Get Docker](https://www.docker.com)

## Install MySQL
In order to let phpMyAdmin run smoothly, we have to ensure MySQL has been installed.

```bash
# docker run -itd --name your_hub_name -p your_host_port：your_virtual_host_port -e MYSQL_ROOT_PASSWORD=user_root_password mysql_image_name_with_dashes
docker run -itd --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root arm64v8/mysql
```

Check [here](https://hub.docker.com/r/arm64v8/mysql/tags) for more information of hub `arm64v8/mysql`

## Install phpMyAdmin

```bash
# docker run --name your_hub_name -d --link mysql_hub_name_to_be_linked -e -p PMA_HOST="mysql" your_host_port：your_virtual_host_port phpmyadmin_image_name_with_dashes
docker run --name phpmyadmin -d --link mysql -e PMA_HOST="mysql" -p 8080:80 phpmyadmin/phpmyadmin

# Which outputs a warning if this command is executed using M1 devices
WARNING: The requested image's platform (linux/amd64) does not match the detected host platform (linux/arm64/v8) and no specific platform was requested
```

- only tested success for 8080:80
- [MAYBE USEFUL List_of_TCP_and_UDP_port_numbers](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers)

## Verify installation

- In Docker Desktop > Container section, it is found that these two hub instances should be found running.
- navigate [http://localhost:8080](http://localhost:8080)
  - username: root
  - password: root

## Cannot connect mysql via PHP

Change `localhost` to `127.0.0.1`

```
database.default.hostname=127.0.0.1
```
