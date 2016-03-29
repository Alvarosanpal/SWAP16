#Práctica 3

Esta práctica se trata principalmente de configurar una tercera máquina virtual en la que instalaremos dos software
diferentes y en la que ambos servirán de balanceador de las peticiones realizadas desde un terminal en el sistema anfitrión.

Se empezará con NginX y se procederá con HaProxy:

##Balanceador NginX

Comenzamos con la instalación de dicho software, para ello lo primero es importar las claves del repositorio del software,
para despues hacer un "apt-get install nginx" y poder instalarlo en nuestra máquina balanceadora. A continuación
adjunto una captura que muestra el final de la instalación de NginX:

![imagen] (InstalacionNginx.png)

Tras la instalación debemos modificar el archivo de configuración por defecto de NginX, y en principio quedaría asi:

![imagen] (ConfiguracionNginx.png)

Despues de guardar dicho archivo y reiniciar el servicio con "service nginx restart", iniciamos un terminal en la máquina
anfitrión, y hacemos dos peticiones con el comando cURL y la dirección IP de nuestra máquina balanceadora, y comprobamos
que nos sirve la página principal de la máquina 1 y despues la página principal de la máquina 2.
Como ambas páginas principales eran idénticas, he modificado los documentos html de las dos máquinas, añadiéndoles
al principio el nombre de cada servidor. En la siguiente captura se observa las dos peticiones y el correcto funcionamiento
del balanceador puesto que sirve una página de cada máquina.

![imagen] (BalanceoPeticionNginx.png)

Después de comprobar la efectividad del balanceador, cambiamos su configuración añadiendole la variable "weight" a las
direcciones de los servidores, lo que nos permite manejar la carga que soporta cada servidor.
En esta ocasión modifico la configuración para que la máquina 1 soporte el doble de peticiones que la máquina 2,
lo que significa que de cada 3 peticiones, la primera máquina servirá 2 mientras que la otra servirá 1.

![imagen] (Configuracion2a1.png)

Y a continuación se muestra la comprobación de la diferencia de carga soportada en los servidores:

![imagen] (Balaceo2a1.png)

Aunque se dan mas conceptos para la modificar la configuración de acuerdo a nuestras necesidades,
con esto se da por finalizado el trabajo a realizar en la práctica 3 en lo referente a NginX.

##Balanceador HaProxy

Da la instalación de este software no he realizado ninguna captura ya que era realizar un simple "apt-get install haproxy"
Tras instalar el software pasamos a modificar su archivo de configuración de forma que queda asi:

![imagen] (ConfiguracionHaproxy.png)

Guardamos el archivo de configuración y lanzamos el comando "/usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg" para iniciar el proceso.

Como tanto el NginX como el HaProxy utilizan el puerto 80, antes de poder iniciar correctamente el HaProxy debemos detener el servicio de NginX con el comando "service nginx stop" paraque deje libre el puerto.
En el caso contrario, no nos vale ese comando para detener HaProxy, por lo que debemos meter el comando "pgrep haproxy" que nos devolverá el identificador de dicho proceso, para despues usar la orden "kill" con ese ID para terminar el proceso y que deje libre el puerto 80 para su posterior uso por parte de otro software.

A continuación adjunto la captura de la prueba del correcto funcionamiento de este segundo software:

![imagen] (BalanceoPeticionHaproxy.png)

Aqui meto una captura de como se vería la petición realizada en en el navegador Google Chrome:

![imagen] (PeticionNavegador.png)

###Fin de la Práctica 3.


