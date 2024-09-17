# Instalar backend

Dentro de la carpeta club-simple-back/source duplicar el .env.local e ingresar la siguiente variable:
COMPOSE_PROJECT_NAME=club_simple
esta variable tambien tiene que ser la misma que tenemos en docker-back/.env

1 - Correr los siguientes comando:

```bash
docker-compose up --build -d
dc exec php composer install --ignore-platform-reqs
```

obs: sobre el comando anterior por alguna razon me genera problema la libreria de google/photos-library

2 - Debemos ingresar a la carpeta club-simple-back/source y ejecutar:

```bash
npm install && npm build
```

obs: estos comando lo ejecutamos fuera del los contenedores, luego vere si debo crear un contenedor que contenga node

3-ingresar a la base de datos. Tenemos de la siguiente forma:

```bash
dc exec db /bin/sh
```

Luego ingreso a la base de datos

```bash
msyql -u root -p${MYSQL_ROOT_PASSWORD}
mysql -u ${MYSQL_USER} -p${MYSQL_PASSWORD} ${MYSQL_DATABASE}
```

```bash
CREATE DATABASE comunidad;
SHOW DATABASE;
SHOW TABLES;
GRANT ALL PRIVILEGES ON comunidad.* TO 'app_user'@'%'; -- para dar privilegios al usuario app_user
```

# Instalar frontend

Ver primero de configurar el .env

```bash
NPM_VOLUMEN_PATH='ubicacion donde esta la carpeta de angular'
NPM_PORT=4200
NPM_PORT_CONTAINER=4200
NPM_NODE_VERSION=22.0.0
NPM_NODE_VARIANTE=alpine
```

Luego es ejecutar para instalar las dependencias

```bash
docker-compose run --rm fronte npm install
```

y por ultimo crear el build:

```bash
docker-compose up --build -d
```
