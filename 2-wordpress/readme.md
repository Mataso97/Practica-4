# Wordpress

### Crear red net-wp

```
docker network create net-wp -d bridge 
```

### Para que persista la información es necesario conocer ¿en dónde mysql almacena la información?

La parte -v /my/own/datadir:/var/lib/mysql del comando monta el directorio /my/own/datadir desde el sistema host subyacente como /var/lib/mysql dentro del contenedor, donde MySQL de forma predeterminada escribir sus archivos de datos.

### ruta carpeta host: db
### Crear contenedor de MySQL en la red net-wp

```
docker run -d --name server-mysql --env-file=variablesMySQL.txt -v ${PWD}/db:/var/lib/mysql --network net-wp mysql:8
```

### Para que persista la información es necesario conocer ¿en dónde wordpress almacena la información?

La información almacenada de WordPress esta en el directorio /var/www/html.

### ruta carpeta host: www
### Crear contenedor de Wordpress en la red net-wp

```
docker run -d --name server-wordpress -v ${PWD}/www:/var/www/html -e WORDPRESS_DB_HOST=server-mysql -e WORDPRESS_DB_USER=georgeq -e WORDPRESS_DB_PASSWORD=123 -e WORDPRESS_DB_NAME=gr2DB --network net-wp --publish published=9300,target=80 wordpress
```

### Personalizar la apariencia de wordpress y agregar una entrada

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?

Al realizar esta acción, las modificaciones que se realizó en la página y la entrada creada siguen existiendo, es decir, no dependen de si existe o no el contenedor, en otras palabras, los datos persistieron. 

```
docker rm server-wordpress
```