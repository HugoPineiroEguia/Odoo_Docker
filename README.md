# Odoo_Docker

En este documento se va a explicar detalladamente como a través de Docker podemos crear u contenedor de Odoo y de PostgrsSql y enlazarlos para trabajar en remoto.
Lo primero de todo es crear un documento llamado “docker-compose.yml”, en el que definiremos las imagenes, credenciales, puertos y volumenes de cada servicio, en este caso, de Odoo y Postgres.

![ImageODOO](https://media.discordapp.net/attachments/558717825020198922/1087350834565750804/imagen.png?width=583&height=629)

En  este documento usamos las imagenes “postgres:13” y “odoo:14.0”, le asignamos el puerto 5432 a Postgres y el 8069 a Odoo, y le decimos al servicio de Odoo que dependa del servicio db, que es el contnedor de la base de datos.
Además asignamos un nombre, contraseña y usuario a la base de datos, postgres, odoo y odoo respectivamente.

A continuacion lanzamos el comando docker-.compose up -d para levantar los contoenedores.

![ImageODOO](https://media.discordapp.net/attachments/558717825020198922/1087350835140382801/imagen.png?width=931&height=244)

En este caso ha habido un error debido a que el puerto 5432 estba ocupado por otro porceso. Para solucionar este problema buscamos que proceso esta ocupando el proceso con el comando sudo lsof i 5432, cogemos el PID del proceso y lo eliminamos con el siguiente comando: sudo kill 1612. A continuacion lanzamos de nuevo el docker-compose up y funciona

![ImageODOO](https://media.discordapp.net/attachments/558717825020198922/1087350835454947379/imagen.png?width=931&height=244)

Podemos aprovechar que estamos en visual y comprobar desde el IDE que los contenedores están corriendo correctamente:

![ImageODOO](https://media.discordapp.net/attachments/558717825020198922/1087350835727573083/imagen.png?width=276&height=82)

Una vez los contenderos esten corriendo nos vamos al navegador y colocamos en la direccion lo siguiente: localhost/8069, que es el puerto que le asignamos a Odoo.
Una vez nos cargue rellenaremos con los datos que nos pide Odoo y debería dejarnos en una pagina como esta: 

![ImageODOO](https://media.discordapp.net/attachments/558717825020198922/1087350836004409495/imagen.png?width=1248&height=629)

Tras haber realizado esto, ya se habrá creado la base de datos de Odoo en el contenedor de Postgres, para comprobarlo nos metemos en el contenedor con el siguiente comando:

![ImageODOO](https://media.discordapp.net/attachments/558717825020198922/1087350836264443904/imagen.png?width=734&height=105)

Nos aseguramos de que usamos la base de datos que hemos creado: 

![ImageODOO](https://media.discordapp.net/attachments/558717825020198922/1087350836516114442/imagen.png?width=591&height=43)

E insertamos la tabla para probar que todo funciona correctamente:

![ImageODOO](https://media.discordapp.net/attachments/558717825020198922/1087350836746793002/imagen.png?width=503&height=112)

Comprobamos que se haya creado correctamente:

![ImageODOO](https://media.discordapp.net/attachments/558717825020198922/1087350836969086986/imagen.png?width=674&height=370)

Y así es como se instala Odoo, se enlaza a Postgres y todo realizado por Docker, mediante un docker-compose.
