# Dockerize Drupal using NGINX and the FPM image

> **Warning** The DB credentials have been exposed intentionally. Please change them before use.

## Launch Drupal fast

### Using Docker Compose

Docker and Compose v2 are required. Compose v2 comes with the latest versions of Docker.

In the [Compose file](compose.yml) , Change the values of these variables to whatever you prefer:

```
      MARIADB_USER: melvincv
      MARIADB_PASSWORD: )#4s<NgiHZoMCA"){kL)
      MARIADB_ROOT_PASSWORD: <~#9[(n%K./'(_3$|[DR
      MARIADB_DATABASE: mcvdrdb
```

Build the NGINX image and bring up the stack:
```
docker compose up -d --build
```

Go to localhost on your browser - in an Incognito / Private window.

[localhost](http://localhost/)

Start Drupal installation and enter the database values given in the compose file

```
Host: mariadb
DB User: MARIADB_USER
DB Password: MARIADB_PASSWORD
DB Name: MARIADB_DATABASE
```

## Explanation

### NGINX and PHP FPM

[NGINX config file](nginx/default.conf)

The compose file brings up 4 services: drupal, nginx, mariadb and adminer. Drupal and NGINX depends on the mariadb service.

There are 2 docker volumes: www-data and db-data.
These are for the drupal files and the MariaDB respectively.
The www-data volume has to be shared between the nginx and drupal service for this to work.

There is a [Dockerfile](nginx/Dockerfile) that is used to build a new nginx based image. In it, we specify the nginx image to use and copy the nginx config to the right location.

## Compose Backups

[compose-20230309](compose-backups/compose-20230309.yml) : This can be used to launch Drupal too. But this uses the default image, not the FPM one.
