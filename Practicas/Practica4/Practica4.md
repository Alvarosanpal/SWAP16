#Práctica 4

Ésta práctica consistirá en la comprobación de rendimiento de los servidores y los balanceadores
instalados en prácticas anteriores.

##Apache BenchMark

Esta utilidad se instala junto con el apache, ya la tenia instalada en mi máquina anfitrión, pero en caso de no tenerla,
basta con hacer "apt-get install apache".

Una vez instalada, solo tenemos que introducir el comando "ab -n 1000 -c 10 http://<IP a analizar>" y se procederá a
realizar 1000 peticiones en grupos de 10 a la ip puesta en el comando.

Aqui unas captura con el resultado de ejecutar dicho comando directamente sobre la IP de uno de los servidores:

![imagen] (AB1Maq1.png)

![imagen] (AB2Maq1.png)

Tras realizar dicho comando 10 veces con la IP de un servidor, la IP del balanceador con NginX activado y la IP
con el balanceador HaProxy, y recoger los datos importantes, adjunto captura de las tablas resultantes:

![imagen] (TablasAB.png)

En las tablas también se puede observar la media de los valores y la desviación típica.

A continuación procedo a adjuntar los gráficos realizados con los datos de las tablas, y a poner algún comentario
si fuese necesario.

-Captura de las 10 pruebas a las tres IP's de Time Taken for Test.
Se puede observar que tarda considerablemente menos cuando se trata de realizar los test a un servidor sin balanceador,
y tratandose de balanceador, Haproxy tarda un poco menos que NginX.

![imagen] (GraficoTTfT.png)

-Captura de las 10 pruebas a las tres IP's de Request per Second.
Se puede observar que el servidor solo recibe mas peticiones por segundo, mientras que al usar el balanceador recibe
menos peticiones por segundo porque las reparte entre los dos servidores finales.

![imagen] (GraficoRpS.png)

Hasta aqui los gráficos relacionados con Apache BenchMark, el gráfico de Failed Request no lo he hecho puesto que siempre
daba como resultado 0.

##Siege

Puesto que este software no viene instalado es lo primero que haremos. Basta con hacer "apt-get install siege":

![imagen] (InstalacionSiege.png)

Una vez instalado procedemos a usar el comando "siege -b -t60S -v http://<IP a analizar>", la opción -b es para que no
deje tiempo de espera entre cada petición, y la opción -t para configurar el tiempo que estarán realizandose las
peticiones, en este caso será 60 segundos.

A continuación una captura del resultado al ejecutar dicho comando:

![imagen] (SiegeMaq1.png)

![imagen] (SiegeMaq1(2).png)

Después de realizar el comando a las IP's 10 veces, y recoger los datos importantes, dejo la tabla resultante:

![imagen] (TablasSiege.png)

Al igual que con Apache BenchMark, en las tablas y los gráficos se puede observar la media de los valores.

A continuación los gráficos relacionados con este software:

-Captura de Availability.
Como se puede observar en el gráfico a continuación, tanto con el servidor solo como con el balanceador HaProxy me
fallaban algunas peticiones, por lo que su procentaje de exito no es 100% como en el caso deNginX.

![imagen] (GraficoA.png)

-Captura de Elapsed Time.
El tiempo transcurrido es inversamente proporcional a la cantidad de peticiones fallidas, de ahí que Haproxy tenga
el mas bajo, puesto que fallaban mas peticiones.

![imagen] (GraficoET.png)

-Captura de Transaction Rate.
Sucede lo mismo que con el Apache BenchMark, el servidor solo recibe mas tasa de transacciones que los balanceadores.

![imagen] (GraficoTR.png)

-Captura de Failed Transaction.
Como se puede ver en el gráfico, el nginX es el único que se completó en las 10 ocasiones sin ninguna petición fallida.

![imagen] (GraficoFT.png)

-Captura de Longest Request.
En este caso NginX solía tener el valor de la petición mas larga bastante bajo, aunque en una de las pruebas salió
muy alto, pero en general, tal y como muestra la media, las peticiones mas largas de todas las pruebas y de los tres casos
está mas o menos equilibrada, teniendo Haproxy un nivel ligeramente inferior.

![imagen] (GraficoLT.png)

###Conclusión

La conclusión en definitiva no está clara, ya que en algunos casos el mejor resultado lo tiene NginX y en otros Haproxy,
pero si tuviese que elegir con que balanceador me quedaba, elegiría NginX, no solo por simplicidad a la hora de
configurarlo, iniciarlo y pararlo, sino también porque es el único que no tuvo ninguna petición fallida haciendo los test
con Siege.

###Fin de la Práctica 4.
