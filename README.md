# sth-docker

## Dockerized Wordpress Environment w/ MySQL

### Project Structure

sth-docker

.
├── .gitignore
├── LICENSE
├── README.md
└── docker-compose.yaml

[_docker-compose.yaml_](docker-compose.yaml)

```yaml
services:
  wordpress:
    image: wordpress
    restart: always
    ports:
      - 80:80
    volumes:
      - ./wp:/var/www/html
    ...
  db:
    image: mysql:5.7
    restart: always
    volumes:
      - db:/var/lib/mysql
    ...
volumes:
  db:
```

If deployed, `docker-compose` will map port 80 of the Dockerized Wordpress container to port 80 of the host platform.

### Install WP Dependencies

Everything is controlled with `docker-compose`.

```bash
docker-compose up
```

### Test Project Configuration

Check containers are running and the port mapping:

Verify that a `wp` folder which contains the persistant filesystem has been created at the project root.

Navigate to `http://localhost:80` in your web browser to access Wordpress. You should see the screen about the "famous 5-minute WP installation."

### Stop/Remove Working Container

```bash
docker-compose down
```

### Delete Project **AND** Resources

Delete the referenced volumes with the `-v` flag:

```bash
docker-compose down -v
```
