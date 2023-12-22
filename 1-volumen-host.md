# Volúmenes

## HOST

### Volumen tipo host con la imagen nginx:alpine 
### ruta carpeta host: directorio en donde se encuentra la carpeta html en nuestro computador, usar \\
### ruta carpeta contenedor: /usr/share/nginx/html desde la documentación

```
docker run -d --name <nombre contenedor> --publish <mapeo de puertos> -v <ruta carpeta host>:<ruta carpeta contenedor> url: <nombre imagen>
```

docker run -d --name nginx-server --publish published=80,target=80 -v C:\VolumenesDocker\nginx\html:/usr/share/nginx/html nginx:alpine

### ¿Qué sucede al ingresar al servidor de nginx?

Da el error 403 Forbidden que básicamente indica que el servidor entendió la solicitud, pero se niega a responderla.

### ¿Qué pasa con el archivo index.html del contenedor?

No hay, se debe crear uno y poner en la carpeta html. Porque no hay un index.html no despliega nada tampoco el nginx.   

### Ir a https://html5up.net/ y descargar un template gratuito - descomprimir en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?

Después, de descargar un template y colocarlo en la carpeta html, podemos visualizar el sitio web que descargamos

### Eliminar el contenedor
### ¿Qué sucede al crear nuevamente el mismo contenedor con volumen de tipo host a los directorios definidos anteriormente?

Después de eliminar el contenedor y volver a crearlo con los volúmenes definidos anteriormente, los archivos que dejaste en esa carpeta del host estarán disponibles de nuevo en el contenedor. Esto significa que se despliega el sitio web que se configuró previamente. 

### ¿Qué hace el comando pwd?

El comando pwd (print working directory) muestra la ruta completa del directorio actual en el que te encuentras trabajando en la línea de comandos o terminal.

### Volumen tipo host usando PWD y PowerShell
```
docker run -d --name server-nginx --publish published=5000,target=80 -v ${PWD}/html:/usr/share/nginx/html nginx:alpine
```