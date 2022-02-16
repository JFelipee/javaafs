# javaafs
Práctica de javaAfs

*********** Día 29  de abril
- He empezado leyendo la práctica y estructurando todo lo que se pedía.
Una vez terminado, he vuelto a leerme los que se pedía en la primera fase, y los ficheros .java
que hay que modificar para esta fase. 
También dedique bastante tiempo a mirar la guía completa sobre la programación en JAVA RAMI ya que, al menos yo no, no estoy familiarizado con esto.
- Este día no programe nada.

******* Día 30 de abril
- Empezamos los primeros pasos  de la Fase 1. Tocando los ficheros "ViceImpl" y "ViceReaderImpl"
realmente no hubo mucha complicación ya que simplemente seguí los pasos de la documentación de
esta práctica, es decir, instanciar métodos que se pedían  y propagar excepciones necesarias.
- EL único método que se complico fue read(), ya que no entendía del todo lo que se pedía.
Pero tras preguntar por el grupo de clase, lo entendí e implemente sin problemas, ya que el 
problema que estaba teniendo es que devolvía la información leída en un parñametro pasado por referencia, donde lo solucione pasándole un parámetro por valor, y para ello realice un simple 
bucle para ir copiando la información en este parámetro pasado por valor.
- No realice más métodos.

****** Día 1 de mayo 
- Empece con la funcionalidad del cliente, es decir, tocando los ficheros "Venus" y "VenusFile".
- En "Venus" realmente no hubo mucho problema, ya que había que acceder a las variables de entorno
que se pedían en el constructor.  Y además, realizar la operación de "lookup" que simplemente miré
la documentación donde implementaban de manera similar esto, y realice algo similar, además de que 
busqué más información sobre esta operación para informarme más de su uso.
*Dejo aquí en enlace donde explican algo mejor para que sirve y su uso=> https://stackoverflow.com/questions/42496369/what-does-naming-lookup-do*
* Aqui la documentación para acceder a variables de entorno en java=> http://chuwiki.chuidiang.org/index.php?title=Acceder_a_variables_de_entorno_desde_Java

- En cuanto a "VenusFile": en la documentación se habla de que en el constructor se debe comprobar 
si el fichero existe. Así que busque documentación para saber como se puede saber si el fichero existe en un directorio. Dejo aquí el enlace => Se adjunta la documentación: https://www.delftstack.com/es/howto/java/java-check-if-a-file-exists/
Para comprobar si el fichero está abierto se usa el paquete de JAVA.io.file.

- Además en "VenusFile": si el fichero no existía, simplemente me descargué el fichero del servidor, abrí un fichero en caché para copiar en este el fichero descargado, ya que se pide que
una copia en caché. Esto anterior se realizó usando un bucle para copiarlo bloque a bloque y cerramos el fichero.
Finalmente abrimos el fichero de cache, es decir, en local y, la documentación especifica que hay
que dejarlo abierto por tanto hicimos esto.
-En caso de que no estuviera el fichero cerrariamos la descarga ya que no necesitamos la descarga
para nada, al tener ya el fichero en local, es decir, en la caché. Y simplemente abririamos el fichero con randoAccesFile.
- En cuanto s alos métodos de "VenusFile" fueron triviales ya que había que trabajar sobre el
fichero local y llamar a los métodos remotos.

********** Día 2 de mayo
- Empecé ejecutando pruebas como se indica en la documentación. Pero tube muchos problemas con la ejecución  ya que me daban errores en "./compila_y_construye_JARS.sh", lo cual no entendía, así que borre todo y volví a descargarme todas los archivos para esta práctica, donde simplemente 
cambié las clases que realizamos en la fase 1. 
- Volví a ejecutrar "./compila_y_construye_JARS.sh" y me seguía dando el mismo error en la línea 7,
error que no debería darme. Así que me pasé de triqui2 a triqui3 e increiblemente me dejo de dar este error, después de estar horas intentando arreglar esto :).

- Finalmente comprobé por encima la fase 1.
- Envié la primera prueba a triqui.

********* Día 3 de mayo
- El resultado de la entrega fue el siguiente:>
"Test.java:24: error: unreported exception NotBoundException; must be caught or declared to be thrown
            VenusFile f = new VenusFile(venus, fich, modo);"
            
- Lo solucioné rápido ya había tocando este fichero al añadir una excepción demás a la clase de "VenusFile"
- Volví a enviar otra prueba.
-El resultado fue el siguiente:>
"PRUEBA 2: ACCESO A FICHERO EXISTENTE EN UNA ÚNICA SESIÓN CON TAMAÑO NO MÚLTIPLO DE BLOQUE SIN SEEK PERO HASTA EOF 
	 NO SE GENERA EXCEPCIÓN SI LECTURA DESPUÉS DE CLOSE (COMPRUEBE SI HA CERRADO FICHERO LOCAL)"
	 
-Efectivamente se me había pasado cerrar el fichero local.
- Volví a enviar otra prueba.

*********** Día 5 de mayo
-Compruebo los resulltados de la anterior entrega y he obtenidos un 3.5, es decir, fase 1 terminada.
-Empiezo con la fase 2.
- Empecé con la FUNCIONALIDAD DEL SERVIDOR:
	-Empecé tocando los archivos "ViceImpl" y "ViceWriterImpl".
		-En viceImpl: simplemente realice una instancia de ViceWriterImpl en el método upload y devolví en el return esta instancia.
		-En ViceWriterImpl: cree un fichero del tipo RandomAccesFile que está asociado al servidor como método de apertura del fichero. 
		Y realice los métodos remotos de esta clase. No hubo mucho problema ya que los método eran del tipo void, por tanto nos olvidamos del problema de javaRmi y las variables pasadas por referencia, como ocurría en "ViceReadImpl".
	- Propagué las excepciones por los métodos, y propague las excepciones del tipo FileNotFoundException, e IOException por las clase-> viceImpl, ViceWriterImpl y ViceWriter.

- A continuación continué con la FUNCIONALIDAD DEL CLIENTE:
	-Se creo una variable booleana que controlara las modificaciones del fichero, además de otra variable que guarda la longitud del fichero original, para comprobar si la longitud ha sido actualizada/cambiada.
	-A partir de los anterior, comence completando el ḿetodo close(), donde se comprueba si el fichero ha sido modificado, en caso de que ocurra eso, se cargará el fichero al servidor.
	Y se empezará a enviar el fichero por bloques, realizando literalmente lo mismo que en "ViceReadeImpl", creando una variable que guarde el tamaño del bloque, y en caso de que el bloque sea mayor a lo que se está leyendo,
	se realizará un bucle para evitar la sobreescritura y se irá copiando en una variable del tamaño de lo que se quiere leer para evitar esta cobreescritura. Importante realizar un seek() en el fichero local.
	-A continuación, cerré el fichero local y el fichero del servidor. 
	- FInalmente comprobé si la longitud del fichero original es igual que el actual, en caso contrario se cargará en el servidor y se actualizará la longitud, y finalmente se volverá a cerrar.
	
-Envié una prueba y el resultado fue el siguiente.  
PRUEBA 7: FICHERO RECORTADO CON SETLENGTH
	 FUNCIONAMIENTO CORRECTO: Valoración de la prueba  .25

PRUEBA 8: ESCRITURA DE UN NUEVO FICHERO
	  SE PRODUCE UNA EXCEPCIÓN IMPREVISTA EN OPEN: java.lang.NullPointerException
	  
	  Fallo en la prueba 8, en concreto un nullPointer en el OPEN. 
-Lo intenté arreglarlo, y toque el código de de "Venusfile" en close() y puse añadí un método a "Venus", este método fue seek(). Con el objetivo de utilizarlo en "venusFile" en concreto en close() con el fichero que se carga al servidor,
Ya que al ser un NullPointer quizás está escribiendo en una zona que no debería del fichero cargado al servidor.

- Envié otra prueba y obtuve el mismo error.
 - Así que para arreglar esto supuse que estária el error en "ViceImpl" o en "ViceWriterImpl", de echo creo que el error estaba en "ViceImpl" ya que estaba instanciandolo mal en el método upload(). A continuación, muestro lo que cambié.
 		    	
 		    	    	ViceWriterImpl instanciaViceUpload= new ViceWriterImpl(fileName, operacion);MAL
				ViceWriter instanciaViceUpload= new ViceWriterImpl(fileName, operacion);BIEN		
Un error bastante de despiste ya que el propio método debe devolver un return del tipo "ViceWriter" además de que no estaría instanciando nada.

- Volví a enviar otra prueba, la cual, lo comprobaré mañana 6 de Mayo ya que se han acabado las pruebas disponible para hoy.

-20 de mayo---
- La he liado mucho, ya que me he dedicado a quitar comentarios inncesarios, y mejorar el código, lo que ha provocado que haya tocado algo que ha hecho que vuelva a tener un 0.5
---> El problema estaba en que cambie el nombre de pueto de blocksize:( sin querer. SOlucionado.
 		 

-23 de mayo---
-Empezamos Fase 3: Se ha implementado venus y venus file la instancia de VenusCB, y en venus Impl se ha añadido la variable de callback en los método de donwload y upload, también he creado en 
vice impl, la estructura de datos para controlar el nombre del fichero y la lista de callbacks.
- He visto que iba a llevarme tiempo, y como el plazo es hasta mañana, día 24 de Mayo he decidido que no vale la pena continuar, ya que aun no he empezado con la tercera práctica de DMUTEX.

- 22 de Junio intente realizar zerocopy y obtener un 10 en la práctica pero no hubo éxito
- Así que decidí realizar esta práctica para obtener un 10 dado que lo tengo más fresco, todos los conceptos de esta práctica, además de que para mi gusto es algo más corta. 

-23 de Junio--------
Realiza toda la tarde, la última parte de esta práctica:
- Cree mi map de fichero y callbacks necesarios, así como la implementación de Lock Manager en 
ViceImpl.java.
- crees los métodos necesarios para poder guardar la solicitud de bloqueos de lectura:
	--> aniadeNameCallb()--> añade el nombre del fichero y su callback corrrespondiente.
	--> close() ---> que se encarga de eliminar el fichero y los callbacks añadidos a mi map.
	
	
-- También tuve que implementar en metodo invalidate()-> de las clase de VenusCBImpl, donde básicamente elimina aquellos que ficheros que primeramente estén en caché, y que contengan el nombre del fichero que se quiere eliminar.

-- Por último añadí en método close() tanto de ViceReaderImpl.java como de ViceWriterImpl.java, 
donde hice uso del LockManager, para solicitar bloqueo de lecturoa o escritura, o bien solicitar
la eliminacion de un bloqueo de lectura o escritura.
