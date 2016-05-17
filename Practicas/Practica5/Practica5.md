#Práctica 5

Esta práctica consiste basicamente en hacer copias de seguridad de una base de datos
entre un servidor maestro y otro esclavo.

Empezamos conectandonos a mysql y creando una pequeña base de datos y añadiendole información, como se ve a continuación:

![imagen] (ConectMysql.png)

![imagen] (CrearBD.png)

![imagen] (ConsultaBD.png)

Tras eso, bloqueamos las tablas, hacemos una copia de seguridad de dicha base de datos en nuestro servidor maestro
y procedemos a desbloquear las tablas.

![imagen] (ReplicaBD.png)

Después nos vamos a nuestro servidor esclavo,copiamos el archivo del servidor maestro con la información de la base de datos,
creamos una base de datos y le asignamos dicho archivo que hemos recibido del servidor maestro.

![imagen] (CopiarSql.png)

Como se ve a continuación podemos consultar la tabla y tenemos toda la información introducida en el otro servidor.
En la siguiente captura se ve que el nombre de la base de datos del servidor esclavo es "agenda2" pero mas adelante
me di cuenta que no se sincronizaban ambas bases de datos si no tenian el mismo nombre asi posteriormente se lo cambie a "agenda".

![imagen] (ComprobarMaq2.png)

De la forma vista anteriormente necesitaríamos una persona haciendo el proceso, a continuación vamos a hacerlo de forma que sea automático.

Cambiamos los archivos de configuración tal cual nos muestra el guión, y procedemos a la creación de un usuario en el servidor maestro:

![imagen] (EsclavoMaq1.png)

Tras eso procedemos a indicarle al servidor esclavo cuales son los datos del servidor maestro:

![imagen] (EsclavoMaq2.png)

En la captura anterior esta mal puesta la variable "master_log_file" pero la corrijo apenas me doy cuenta.

Después de introducir los datos, iniciamos el esclavo y preguntamos por su estado, como se ve a continuación todo
está correcto puesto que no me sale null en la variable "Seconds_Behind_Master".

![imagen] (NoNuloMaq2.png)

Por último procedemos a introducir datos en el servidor maestro y a comprobar si se han actualizado en el servidor esclavo.
En la última captura se puede observar a la izquierda el servidor maestro tras introducir nuevos datos, y a la derecha la
consulta a la base de datos actualizada instantaneamente.

![imagen] (ComprobacionFinal.png)

###Fin de la Práctica 5.
