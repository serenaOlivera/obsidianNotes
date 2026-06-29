# 1
## Organización, Direccionamiento y Reenvío en WAN
Para comprender cómo funciona una WAN y cómo se la diseña, es necesario atender tres cuestiones fundamentales:
1. Cómo está organizada la red en términos de máquinas y sus interconexiones.
2. Cómo se nombran esas máquinas e interfaces mediante un esquema de direccionamiento y
3. Cómo se construyen las tablas de reenvío que permiten que los paquetes avancen hacia su destino.

El primer desafío es lograr un esquema de direccionamiento que sea verdaderamente escalable. Un direccionamiento poco escalable, es aquel cuyas direcciones se agotan rápidamente o no alcanzan para cubrir la demanda creciente de nuevas máquinas, interfaces o LANs.
Resolver este problema es indispensable: sin un espacio de direcciones suficientemente grande y bien estructurado, la red simplemente no puede crecer.

Una vez que garantizamos que el direccionamiento puede escalar, aparece el siguiente obstáculo: incluso con direcciones suficientes, las tablas de reenvío pueden volverse demasiado grandes si cada enrutador necesita conocer demasiados destinos. Esto nos obliga a pensar cómo organizar una WAN grande para evitar que las tablas consuman demasiada memoria y se vuelvan lentas de consultar.

## Direccionamiento de interfaces de máquinas
Es la base para construir tablas de reenvío más correctas y escalables. Este es el enfoque adoptado por internet.

**Interfaz:** conexión entre host/enrutador y enlace físico. Un enrutador tiene muchas interfaces, una por cada línea de salida. Un host tiene una o dos interfaces: con Ethernet cableada, con red inalámbrica 802.11.
Las interfaces están conectadas entre sí por medio de conmutadores y estaciones base.
![[Pasted image 20260413110530.png]]

#### ¿Cómo se definen las direcciones de interfaces de las máquinas de una red local (LAN)?
 Una dirección puede ser un número binario de n bits donde los primeros bits son del número de red y los últimos del número de interfaz. Por ejemplo IPv4 usa direcciones de 32 bits.

¿Conviene que una tabla de reenvío contenga como destinos números de interfaz de máquinas?
	No, porque las interfaces de máquinas son demasiadas y van a ocupar mucho espacio en la tabla de reenvío. Además, solo necesito que el paquete llegue a la LAN adecuada.
Hay muchas menos LAN que máquinas en ellas; por lo tanto, conviene que los destinos de las tablas de reenvío sean LANs expresadas de algún modo conveniente.Por ejemplo:
- <dirección de interfaz de inicio, dirección de interfaz de fin>
- <dirección de interfaz de inicio,  cantidad total de interfaces>
- <dirección de interfaz de inicio, n> 
  tal que hay 2^n interfaces en total
- <dirección de interfaz de inicio, x-n>
  tal que hay 2^n interfaces en total y x es la longitud de las direcciones de interfaz . (usada en IPv4)
Cualquiera de estas soluciones anteriores puede ser usada para indicar destinos en tablas de reenvío. 

Ejemplo de los prefijos usados en IPv4:
Significado del prefijo 128.208.0.0/24:
- la dirección IP de la interfaz más baja en el bloque es 128.208.0.0
- la porción de la red es de 24 bits
- 32-24 =8, por lo tanto, tengo 2⁸ interfaces en total en la red.
#### ¿Cómo se usa la tabla de reenvío cuando llega un paquete?
Extraer la dirección de interfaz de destino del paquete entrante. Luego analizar la tabla de reenvío entrada por entrada, chequear si la dirección de interfaz extraída está entre los valores de las direcciones de interfaz de la fila. Si coinciden entradas múltiples se usa la red más pequeña.
## Limitaciones de escalabilidad de las direcciones de interfaz
El espacio de direcciones puede agotarse si cada máquina o interfaz necesita una dirección única dentro de una WAN cada vez más grande. Este problema no es teórico, ocurrió en la práctica con IPv4. Por eso, antes de pensar en cómo organizar redes enormes, necesitamos resolver primero cómo hacer que el direccionamiento mismo pueda escalar. 

Tenemos dos soluciones posibles:
1. Abandonamos el espacio de direcciones y creamos un espacio de direcciones más grande. Fue lo que se hizo con IPv4: se creó IPv6 con esta finalidad (En lugar de direcciones de 32 bits se usaron direcciones de 128 bits).
2. Seguimos usando el mismo espacio de direcciones inteligentemente con reutilización de direcciones. Se aplicó para el caso de IPv4 para alargar el uso de espacios de direcciones. La solución se llama NAT (traducción de dirección de red natural).

### Direcciones IPv6
Son escritas como 8 grupos de 4 dígitos hexadecimales. Para separar los grupos se usa **":"**.Por ejemplo: 8000:0000:0000:0123:4567:89AB:CDEF
Optimización: Ceros a la izquierda de grupos pueden ser omitidos, grupos con dos **":"**.
Una dirección IPv6 la podemos dividir en:
- **Identificador de red:** identifica la red principal en la que se encuentra el dispositivo. 
- **Identificador de subred:** ayuda a dividir la red principal en subredes más pequeñas.
- **Identificador de interfaz:** identifica de manera única al dispositivo dentro de la subred.
Ejemplo: dada la dirección 2001:0db8:85a:0000:0000:8a2e:0370:7334. 
- identificador de red: 2001:0db8: 85a3
- identificador de subred: 0000:0000
- identificador de interfaz: 8a2e:0370:7334

### NAT

Traducción de dirección de red natural (NAT): Asignar una sola dirección de interfaz a cada organización para el tráfico de internet.
1. Dentro de la organización cada computadora tiene una dirección de interfaz única que se usa para el tráfico interno. O sea, estas direcciones de interfaz no se usan afuera de la LAN; solo adentro de la organización, y se repiten en distintas LAN.
2. Cuando un paquete sale de una organización y va a la WAN, se presenta una traducción de dirección (de la dirección de la  computadora en la organización a la dirección de interfaz única usada por la organización)
**Implementación:** Para que este esquema sea posible, es necesario considerar rangos de distintos tamaños para así permitir organizaciones de distinto tamaño. Por ejemplo, hay 3 rangos de direcciones IPv4 que se han declarado como privados. Las organizaciones pueden usarlos internamente cuando deseen. Las única regla es que ningún paquete que contiene estas direcciones pueda aparecer en la internet. Los 3 rangos reservados son:
- 10.0.0.0    -10.255.255.255/8        (16,777,216 hosts)
- 172.16.0.0     -172.31.255.255/12     (1,048,576 hosts)
- 192.168.0.0   -192.168.255.255/16   (65,536 hosts)

![[Pasted image 20260418195451.png]]

#### Tabla de traducción de la caja NAT
Los índices en la tabla de la caja NAT son números de puerto para identificar la máquina.  Una entrada de la tabla contiene los siguientes elementos:
	 <número de puerto para identificar la conexión, dirección de interfaz interna a la organización>

**¿Cómo tratar un paquete que llega a la caja NAT desde la WAN?**
	 El puerto de origen en el encabezado TCP se extrae y usa como un índice en la tabla de traducción de la caja NAT. Desde la entrada localizada, la dirección de interfaz interna y el puerto TCP se extraen e insertan en el paquete, entonces el paquete se pasa al enrutador de la compañía para su entrega normal usando la dirección de interfaz.

**¿Cómo tratar un paquete saliente que entra en la caja NAT?**
	La dirección de origen interna a la compañía se reemplaza por la dirección de interfaz de la compañía y el puerto de origen TCP se reemplaza por un índice en la tabla de traducción de la caja NAT. 
## Red jerárquica con regiones de igual importancia
Incluso con direcciones suficientes, una WAN grande puede generar tablas de reenvío inmensas si cada enrutador debe conocer demasiados destinos. Es decir, el direccionamiento escalable es necesario, pero no suficiente: también necesitamos que las tablas de reenvío puedan mantenerse pequeñas y eficientes.

**¿Cómo hacer para que las tablas de enrutamiento no crezcan demasiado cuando crece mucho el tamaño de la subred?**
	Dividir los enrutadores de la WAN en **regiones**. Cada región es un grafo separado de las demás regiones, cada enrutador pertenece a una región y hay enlaces entre regiones.
	![[Pasted image 20260419131822.png]]

Los enrutadores y las regiones pueden tener dirección en una red jerárquica de regiones de igual importancia.

**¿Cómo definir las direcciones de los enrutadores y las regiones?**
	Numeramos las regiones y para cada región determinamos cantidad de enrutadores y forma de contar esa cantidad. Un enrutador va a tener como dirección un par <número de región, identificador de enrutador>

¿Cuáles son los destinos de la tabla de reenvío de un enrutador?
	Entradas para todos los enrutadores locales, 
	Entradas para las demás regiones en las que no está el enrutador.
	y denotamos la línea de salida para un destino usando la dirección del enrutador al que se llega por esa línea de salida.
	![[Pasted image 20260419132341.png]]

En las redes enormes, una jerarquía de dos niveles es insuficiente, entonces tenemos distintas soluciones posibles:
- Agrupar las regiones en clústeres,
- Agrupar las regiones en clústeres y los clústeres en zonas 
- Incluso podemos seguir agregando más niveles.

## Red jerárquica con área dorsal
El modelo de regiones de igual importancia nos permitió ver cómo una jerarquía básica ayuda a reducir el tamaño de las tablas de reenvío y a limitar la visibilidad de la topología. Sin embargo, esta falta de centralidad complica la administración y el control del tráfico interregional 

Para resolver este problema surge una organización más refinada: las redes divididas en áreas conectadas a un  área dorsal. Este modelo introduce un backbone que concentra la conectividad global y simplifica el tránsito entre áreas, permitiendo una WAN más modular, eficiente y escalable.
Podemos organizar una red jerárquica (WAN) en áreas donde hay un área dorsal
![[Pasted image 20260419133159.png]]
Las áreas se numeran. El área dorsal tiene número 0


**¿Cómo se clasifican los enrutadores en una red jerárquica con área dorsal?**
- Enrutadores internos:
	  Yacen completamente dentro de un área
- Enrutadores dorsales:
	  Enrutadores en un área dorsal.
- Enrutador de borde de área (EBA)
	  Es parte de una red dorsal y a la vez de una o más áreas.
- Enrutador de borde de WAN:
	  Inyecta en el área rutas a destinos externos en otras WAN. Ya lo veremos con cuidado cuando estudiemos interredes.

**¿Cómo organizar un área?**
	1. Las líneas punto a punto entre dos enrutadores
	2. Redes de multiacceso con difusión (p.ej. la mayoría de las LAN)
	3. Redes de multiacceso con muchos enrutadores, cada uno de los cuales se puede comunicar directamente con los otros (LAN 3 de la figura)
	   ![[Pasted image 20260419135433.png]]

En una red jerárquica con área dorsal, se puede usar de **direccionamiento** las direcciones de interfaz de los enrutadores. También se identifican las LAN de organizaciones.
Se usan las tablas de reenvío de cuando se trabaja con interfaces. Recordar que para estas redes se usan como destinos de las tablas de reenvío las LAN, identificadas como mencionamos antes.

# Algoritmos de enrutamiento para WANs no jerárquicas

Cómo lograr que los paquetes encuentren su camino en una red de enrutadores interconectados, incluso cuando la topología cambia, los enlaces fallan o el tráfico se vuelve impredecible.

Un algoritmo de enrutamiento es un algoritmo que escoge bien las rutas a usarse para enviar paquetes. Las rutas se determinan actualizando y llenando las tablas de reenvío. Un algoritmo de enrutamiento se ejecuta en los enrutadores de la WAN.

## Conceptos básicos
¿Cómo representar una subred como un grafo?
![[Pasted image 20260419165918.png]]
Grafo G= (N,E)
N = conjunto de enrutadores = {u,v,w,x,y,z}
E= conjunto de enlaces = {(u,v), (u,x) (v,x), (v,w), (x,w), (x,y), (w,y), (w,z), (y,z)}

Los arcos tienen etiquetas para el costo de atravesarlos.
c(x, x') = costo de enlace (x,x')

Los costos de los arcos podrían calcularse como función de varios parámetros: la distancia, ancho de banda, tráfico medio, costo de comunicación, longitud media de las colas, retardo medio, y otros factores. El costo de un camino es la suma de los costos.

## Enrutamiento de caminos más cortos
En este bloque ingresamos al primer escenario estable: una red cuya topología no cambia y cuyo tráfico varía muy poco. En este contexto, podemos permitirnos calcular las rutas una sola vez y usarlas durante largos períodos sin necesidad de actualizarlas.

Algoritmo de enrutamiento de caminos más cortos: Para elegir una ruta entre un par de enrutadores, encontrar en el grafo una de las rutas más cortas entre ellos. Uno de ellos es el algoritmo de Dijkstra (1959) 

Pasos para calcular las tablas de reenvío usando el algoritmo de Dijkstra:
1. Construir grafo de la subred con costos
2. Ingresar grafo de la subred con costos en los enrutadores
3. En cada enrutador construir tabla de enrutamiento; para eso:
   a. Ejecutar algoritmos de Dijkstra en el enrutador
   b. A partir del árbol de caminos más cortos con raíz en el enrutador obtenido generar la tabla de reenvío del enrutador.
## Inundación hacia un destino
En una red sometida a fallas frecuentes, por bombardeos, catástrofes naturales o infraestructura extremadamente frágil, queremos mandar un paquete de un nodo de origen u a un destino v.
Los algoritmos de caminos más cortos dejan de ser confiables porque suponen una topología relativamente estable.

La meta aquí es maximizar la probabilidad de entrega de un paquete a un destino específico, incluso cuando la topología cambia cuando el paquete está en tránsito.

Para enviar un paquete de un origen u a un destino v se respetan las siguientes reglas:
- U manda el mensaje por todas las líneas de salida
- Cada paquete que llega a un enrutador distinto de v se reenvía por cada una de las líneas excepto aquella por la que llegó.
**A este algoritmo se le llama inundación.**

Problemas de la inundación 
- La inundación genera grandes cantidades de paquetes duplicados. 
- Árbol de envío de paquetes. Cada arco representa un paquete que se envía. 
- Árbol de envío de paquetes es infinito con infinitos duplicados. O sea, se generan infinitas rutas. La causa es la presencia de ciclos en el grafo de la subred.

¿Qué información deben llevar los paquetes que se difunden?
	El enrutador de origen pone un número de secuencia en cada paquete que recibe de sus hosts (así se distingue entre paquetes distintos del mismo enrutador de origen)

¿Qué información debe recordar un enrutador en su registro de paquetes difundidos?
	Un enrutador recuerda para cada enrutador de origen, los números de secuencia recibidos - i.e pares <enrutador de origen, n° secuencia>

¿Qué pasa cuando llega un paquete a un enrutador?
	Si llega un paquete a un enrutador con par <enrutador de origen, número de secuencia>, verifica si el par está en el registro de paquetes difundidos:
	- Si no está, se lo difunde al paquete
	- En caso contrario, se lo descarta.

Estructura de datos para el registro de paquetes difundidos: 
Para cada enrutador usar tabla de registro de paquetes difundidos.
 ![[Pasted image 20260419183330.png]]
 **Contador:** indica el mayor número de secuencia tal que llegaron paquetes con todos los números de secuencia anteriores desde ese enrutador de origen
 Este mecanismo no controla hasta dónde se propaga un paquete. 

Introduciremos un nuevo mecanismo: el **contador de saltos**. El mismo reducirá la propagación a un radio controlado y evitando que la inundación se extienda más allá de lo necesario.

Al comienzo en el enrutador de origen se inicializa el  contador de saltos del paquete y se reenvía el paquete por todos los enlaces. Cuando llega un paquete a un enrutador se decrementa el contador de saltos. Si el enrutador es el enrutador de destino: el paquete no se difunde más, sino si el contador de saltos es cero: el paquete se descarta, sino el paquete se difunde.

## Inundación de difusión
En este bloque cambiamos de objetivo: queremos difundir un mensaje a todos los enrutadores de la red.

La meta aquí es la entrega del paquete a los nodos sin necesidad de precomputar rutas óptimas.
Vamos a considerar inundación de difusión con registro de paquetes difundidos. El registro de paquetes difundidos es la misma estructura de datos de antes
![[Pasted image 20260419183330.png]]

Si el enrutador de origen no está en la tabla:
1. Se crea una entrada en la tabla para ese enrutador de origen.
2. Si el número de secuencia es 0: se agrega 0 en el contador.
3. Sino se crea un nodo en la lista de números de secuencia.
4. Se difunde el paquete.
• Si el enrutador de origen esta en la tabla:
	- Si el número de secuencia es el siguiente al contador: se actualiza el contador removiendo elementos en la lista de números de  secuencia si es necesario. Luego se difunde el paquete.
	- Si el numero de secuencia está en la lista o tiene el valor del contador: se descarta el paquete.
	- Sino: se agrega un nodo con el número de secuencia a la lista de números de secuencia. Luego se difunde el paquete

Ahora... ¿cómo puede cada enrutador construir una visión consistente de toda la red y actualizarla cuando la topología cambia?

## Enrutamiento de estado de enlace

 ¿Qué tareas hace un enrutador?
1. Descubrir sus vecinos
2. Medir el costo a cada uno de sus vecinos
3. Construir un paquete diciendo lo que ha aprendido
4. Enviar este paquete a todos los demás enrutadores (usando inundación de difusión)
5. Computar el camino más corto a cada uno de los otros enrutadores
• Este algoritmo es valioso porque:
- Responde rápido frente a cambios en la topología de la red.
- Ayuda a derivar algoritmos de enrutamiento más sofisticados como el que usa internet (OSPF)
- Ahora vamos a ver cada una de las tareas anteriores en detalle

¿Cómo se puede averiguar quiénes son los vecinos de un enrutador?
	Se envía paquete Hello a cada línea punto a punto
	Se espera que el enrutador del otro extremo regrese una respuesta indicando quién es

¿Cómo se puede hacer para que enrutador conozca retardo a sus vecinos? (ya sabe quienes son sus vecinos)
	- enviar un paquete ECHO especial a través de la línea
	- Una vez que llegue al otro extremo, éste debe regresarlo inmediatamente 
	- Uso de temporizadores para medir el tiempo.
	- Método: Se mide el tiempo de ida y vuelta y se divide por 2.
•Problema del método: Asume implícitamente que los retardos son simétricos

Cada enrutador construye un paquete de estado de enlace (LSP) conteniendo los retardos a sus vecinos.

>[!question] ¿Qué datos debe tener un LSP?
>	- Identidad del emisor (para saber de quien se trata)
>	- Número de secuencia (para distinguir entre distintos LSP de un enrutador) 
>	- Lista de <vecino, retardo al vecino>

¿Cuándo se pueden construir los LSP?
	- Construirlos a intervalos regulares.
	- Construirlos cuando ocurra un evento significativo, como la caída o la reactivación de la línea o de un vecino, o el cambio apreciable de sus propiedades

![[Pasted image 20260419185723.png]]

Ahora vemos la distribución confiable de los LSP.

• Usamos inundación de difusión con registro de paquetes difundidos.

¿Cómo es la estructura de datos del registro de paquetes difundidos que lleva cada enrutador? 
	Basta con: para un enrutador de origen indicar el último número de secuencia ya visto de ese enrutador de origen (este sería el LSP más reciente recibido).
	
Cuando llega un LSP a un enrutador,
	Si es nuevo (nuevo número de secuencia mayor que los anteriores),se reenvía a través de todas las líneas, excepto aquella por la que llegó.
	Si es un duplicado (número de secuencia mayor visto, pero repetido), se descarta.
	Si llega un paquete con número de secuencia menor que el mayor visto hasta el momento, se rechaza como obsoleto debido a que el enrutador tiene datos más recientes.

¿Para qué son los LSP que llegan a un enrutador?
	- Para construir el grafo de la red de enrutadores interconectados. Por lo tanto es necesario almacenar en búfer en el enrutador los LSP más recientes recibidos de cada origen.

 ¿Qué elementos puede contener una fila de la tabla del búfer de LSP de un enrutador?
	  Enrutador de origen, número de secuencia del último LSP, datos de ese LSP.
![[Pasted image 20260419190503.png]]
¿Cuándo se puede crear o actualizar la tabla de enrutamiento de un enrutador?
	• una vez que el enrutador ha acumulado un grupo completo de paquetes de estado del enlace
• ¿Qué se hace después?
1. Usando los LSP construir el grafo de la subred completa.
   Cada enlace se representa dos veces, una para cada dirección.
   Los dos valores pueden promediarse o usarse por separado.
2. Se ejecuta el algoritmo de Dijkstra para construir la ruta más corta  a todos los destinos posibles.
3. Con los resultados del mismo se actualiza la tabla de enrutamiento

Un protocolo real enfrenta problemas adicionales: por ejemplo, errores en números de secuencia y caída de enrutadores. Además es necesario de reducir la carga sobre la red. En la siguiente parte del bloque veremos cómo resolver estos  problemas técnicos y cómo optimizar el protocolo para hacerlo más eficiente y más robusto.

**Situación:** Si llega a corromperse un número de secuencia y se escribe 65540 en lugar de 4 (un error de un bit), los paquetes 5 a 65540 serán rechazados como obsoletos, dado que se piensa que el número de secuencia actual es 65540.
	• Para protegerse contra errores en las líneas entre enrutadores se 	puede confirmar cada LSP que se recibe. ¿Cómo funciona entonces la protección contra estos errores?
	o Antes de actualizarse el número de secuencia más grande, el enrutador manda una	confirmación de recepción al transmisor y luego espera una respuesta afirmativa o negativa del transmisor.
	 En el primer caso se actualiza el número de secuencia más grande.
	 En el segundo caso se descarta el LSP que se recibió por estar errado


Asumir que una vez que un LSP más actualizado de un enrutador de origen llega a un enrutador, y no se lo encola para difusión inmediata, sino que se espera un tiempo breve. ¿Cómo esto cambia la manera a hacer la difusión?
-  En ese tiempo puede llegar desde otras líneas el mismo LSP, por lo que no va a ser necesario difundir el LSP por esas líneas.
-  También puede llegar un LSP más reciente del mismo origen, por lo que se cambia el LSP en el buffer por otro más reciente evitando así enviar un LSP que se quedó viejo.
- Por lo tanto se puede hacer más eficiente el algoritmo de inundación.

¿Cómo modificar el búfer de LSPs para reflejar esta optimización?
(recordar que además de difundir el LSP hace falta confirmarlo)

Usar Banderas que pueden ser:
- Banderas de confirmación de recepción: indica a dónde tiene que enviarse la confirmación de recepción del paquete.
- Banderas de envío: significan que el paquete debe enviarse a través de las líneas indicadas.
- Si llega un duplicado mientras el original aún está en el búfer, los bits de las banderas tienen que cambiar

![[Pasted image 20260419190526.png]]

**Problema:** Si los números de secuencia vuelven a comenzar, reinará la confusión (el algoritmo de inundación no está preparado para eso). ¿Cómo evitar este problema?
• Usar un número de secuencia de longitud suficiente para que el problema anterior no suceda. Por ej. de 32 bits.
 P.ej. Si un enrutador produce un paquete de estado de enlace cada segundo, llevará 137 años antes de volver a empezar.

**Problema:** Si llega a caerse un enrutador (de origen), perderá el registro de su número de secuencia. Si comienza nuevamente en 0, se rechazará el siguiente paquete.
• Para evitar que esto suceda se puede hacer que la información de un
enrutador caído expire a lo largo de la red luego de caerse.
• Sugerir una implementación de esta idea.
	Una vez identificado que un enrutador está caído:
	- Se propaga la información de este hecho por toda la red.
	- Se hace que la información asociada al enrutador caído expire (paquete pendiente a enviar, 	número de secuencia más grande recibido, etc.).
	- Así que cuando ese enrutador vuelva a la vida, puede comenzar con número de secuencia 0.


# **Hasta acá entro el parcial 1**

# Algoritmos de enrutamiento para WANs jerárquicas
