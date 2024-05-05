## Instrucciones para levantar el escenario

Este proyecto utiliza PHP 8.

Para ilustrar este despliegue se utiliza una aplicación de muestra, obtenida de aquí: [https://github.com/JeffreyWay/Laravel-From-Scratch-Blog-Project](https://github.com/JeffreyWay/Laravel-From-Scratch-Blog-Project)

Podría desplegarse la aplicación cuando se hiciese el `docker-compose up -d` pero lo he dejado como está para que pueda ser genérico y pueda desplegarse otra aplicación si se prefiere.

Una vez los contenedores están corriendo habría que ir al contenedor del servidor web:

```console
$ docker exec -it apache-laravel
```

Instalar dependencias:

```console
$ composer install
```

Tras ello se debe crear la BBDD que está indicada en el archivo `.env` del proyecto de Laravel, en mi caso *miBBDD*. Esto se podria hacer desde el phpmyadmin que ya estaría corriendo en **http://localhost:8001** o bien mediante instrucciones por terminal desde el mismo contenedor del servidor web en el que estamos.

Tras ello:

```console
$ php artisan migrate --seed
```

Y por último:

```console
$ php artisan key:generate
```

Ya sólo quedaría darle los permisos adecuados a la carpeta del servidor web para que podamos acceder:

```console
$ chown -R www-data:wwww-data /var/www/html
```

Y podremos acceder al blog (o aplicación desplegada) en ***http://localhost:8000***
