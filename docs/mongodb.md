## Instrucciones para levantar el escenario

Este escenario pretende levantar dos contenedores:

1. Base de datos NoSQL **MongoDB**
2. Interfaz de administración web de MongoDB, **Mongo Express**

El `docker-compose.yml`lucirá tal que así:

```yaml
services:
  mongo:
    image: mongo # (1)
    container_name: mongoDB # (2)
    restart: always # (3)
    environment:
      MONGO_INITDB_ROOT_USERNAME: ${USER}
      MONGO_INITDB_ROOT_PASSWORD: ${PASSWORD}

  mongo-express:
    image: mongo-express
    restart: always
    ports:
      - 8081:8081 # (4)
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: ${USER}
      ME_CONFIG_MONGODB_ADMINPASSWORD: ${PASSWORD}
      ME_CONFIG_MONGODB_URL: mongodb://${USER}:${PASSWORD}@mongoDB:27017/
      ME_CONFIG_BASICAUTH: false
```

1. Imagen a partir de la cual se creará el contenedor. Podríamos indicarle una versión concreta de MongoDB si fuese necesario.
2. Nombre que le damos a nuestro contenedor
3. Como indica la [documentación](https://docs.docker.com/config/containers/start-containers-automatically/) de Docker, reiniciará automática el contenedor si se para por alguna razón, no así si lo paramos nosotros a mano.
4. Exponemos los puertos del contenedor al mundo para poder acceder a ellos. En este caso el puerto 8081 del contenedor se corresponderá con el puerto 8081 de nuestra máquina. De esta forma accederemos a la interfaz web.

Donde las variables que van precedidas de un símbolo de dólar y entre llaves (*${  }*) son variables de entorno, que están definidas en el archivo `.env`

Para utilizar el escenario en este caso es muy sencillo. Basta con seguir la pauta de siempre:

![](./img/mongo2.png)

Tras descargar las imágenes y construir los contenedores, ya estamos en disposición absoluta de utilizarlos.

Accedemos a Mongo Express :

![](./img/mongo3.png)

!!!warning "Atención"
    Una vez más, yo estoy utilizando AWS. Si estamos levantando este escenario en nuestro propio equipo, habríamos de poner `http://localhost:8081`.

Y ya podremos interactuar con el servidor MongoDB:

![](./img/mongo4.png)