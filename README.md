# sth-docker

## Dockerized Wordpress Environment w/ MySQL

### View Project Structure

.
├── docker-compose.yaml
└── README.md

[_docker-compose.yaml_](docker-compose.yaml)

```yaml
services:
  db:
    image: mysql:8.0.19
    ...
  wordpress:
    image: wordpress:latest
    ports:
      - 81:81
    restart: always
    ...
```

If deployed, `docker-compose` will map port 81 of the Dockerized Wordpress container to port 81 of the host platform.

### Install WP Dependencies

Everything is controlled with `docker-compose`.

```bash
$ docker-compose up -d
Creating network "wordpress-mysql_default" with the default driver
Creating volume "wordpress-mysql_db_data" with default driver
...
Creating wordpress-mysql_db_1        ... done
Creating wordpress-mysql_wordpress_1 ... done
```

### Test Project Configuration

Check containers are running and the port mapping:

```bash
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
5fbb4181a069        wordpress:latest    "docker-entrypoint.s…"   35 seconds ago      Up 34 seconds       0.0.0.0:81->81/tcp    wordpress-mysql_wordpress_1
e0884a8d444d        mysql:8.0.19        "docker-entrypoint.s…"   35 seconds ago      Up 34 seconds       3306/tcp, 33060/tcp   wordpress-mysql_db_1
```

Navigate to `http://localhost:81` in your web browser to access Wordpress. You should see the screen about the "famous 5-minute WP installation."

### Stop/Remove Working Container

```bash
docker-compose down
```

### Delete Project **AND** Resources

Delete the referenced volumes with the `-v` flag:

```bash
docker-compose down -v
```
