# Volúmenes
## NOMBRADO

### Crear volumen

```
docker volume create vol-postgres
```

### ¿Cuál es el Mountpoint de vol-postgres?

Para saber el Mountpoint del volumen podemos usar el comando:

```
docker volume inspect vol-postgres
```

### ¿Cómo acceder a ese Mountpoint?

Se utilizó el siguiente comando Docker para acceder al Mountpoint:

```
docker run -it -v vol-postgres:/tmp ubuntu bash
```

Este comando crea un contenedor de Ubuntu que tiene acceso al contenido del volumen vol-postgres a través del directorio /tmp, lo que te permite explorar y modificar los datos dentro de ese volumen desde el contenedor Ubuntu.

Al acceder al directorio “tmp” no tendremos datos porque aún no está montado a un contenedor:

### Crear una red para postgres

```
docker network create net-postgres -d bridge 
```

### Servidor postgres usando el volumen nombrado

```
docker run -d --name server-postgres -e POSTGRES_DB=db_drupal -e POSTGRES_PASSWORD=12345 -e POSTGRES_USER=user_drupal -v vol-postgres:/var/lib/postgresql/data --network net-postgres postgres
```

### ¿Qué ha sucedido en vol-postgres?

Ahora contiene los datos del contenedor al que está montado, en este caso “server-postgres”.