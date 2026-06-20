## Introducción 
El problema de fondo
	• La interconexión de múltiples WAN no escala con inundación, porque:
		-  Cada WAN tiene su propio PPEI.
		- Los protocolos intra-WAN no ven rutas externas. 
		- Si inundamos rutas externas dentro de cada WAN: 
			  • los enrutadores internos pasan a participar del protocolo exterior,
			   • las tablas internas crecen sin límite,
			   • cada cambio externo afecta a todos los enrutadores internos. 
		Esto rompe la escalabilidad y mezcla planos que pueden estar separados. 
**Conclusión:** Necesitamos un protocolo PPEE donde solo las puertas de enlace participan, reduciendo el tamaño de las tablas internas y aislando los enrutadores internos de la dinámica externa.

#### EGP como advertencia histórica
 EGP es un diseño que no podía escalar. 
 EGP es un protocolo plano, sin jerarquía, sin política y sin agregación. Tenía:
 - Inundación de rutas externas dentro de cada WAN. 
 - Los enrutadores internos terminaban cargando todas las rutas del mundo. 
 - Sin prefijos, sin agregación: cada red era una entrada independiente. 
 - Sin política, sin control administrativo sobre qué anunciar o aceptar. 
 - Sin independencia entre WANs: un cambio externo afectaba a todos.
 Conclusión: EGP no escala: mezcla planos, sobrecarga los enrutadores internos y carece de los mecanismos necesarios para operar en una interred grande y autónoma

**Lecciones del fracaso conceptual de EGP : Qué no debe hacer un protocolo de puerta de enlace exterior**
- No debe inundar rutas externas dentro de la WAN. 
- No debe obligar a enrutadores internos a participar del enrutamiento exterior.
- No debe depender de la topología física.
- No debe anunciar miles de destinos individuales sin agregación. 
- No debe carecer de política para controlar qué se anuncia y qué se acepta.
- No debe carecer de independencia entre WANs (cada cambio externo no debe afectar a todos). 

Conclusión: Un PPEE moderno debe evitar todos estos errores: necesita prefijos, agregación, política, independencia y sesiones punto a punto.

>[!info] En este bloque introducimos ideas nuevas que no existían en el modelo anterior: 
>- Prefijos como unidad de anuncio. 
>- Agregación para reducir el tamaño de las tablas internas. 
>- Sesiones punto a punto en lugar de inundación. 
>- AS-PATH para evitar loops entre dominios. 
>- Relaciones entre sistemas autónomos (proveedor - cliente, par). 
>- Políticas más expresivas que controlan qué se anuncia y qué se acepta. 
>Aquí empezamos a ver cómo se construye un protocolo exterior moderno.


## Requisitos arquitectónicos
Qué debe hacer un protocolo exterior para escalar 
- Mantener autonomía de cada WAN (SA).                        
- Anunciar prefijos, no destinos individuales. 
- Permitir agregación en las puertas de enlace. 
- Usar tablas de reenvío de los enrutadores internos en lugar de inundación. 
- Transportar avisos con fiabilidad (sesiones punto a punto). 
- Evitar loops en rutas anunciadas. 
- Implementar política explícita para controlar qué se acepta y qué se anuncia.

## Separación de PPEI/ PPEE
Separación estricta entre PPEI y PPEE 
- PPEI (OSPF u otro): 
	-  calcula rutas internas, 
	-  no ve rutas externas, 
	- recibe prefijos agregados como LSAs externos. 
- PPEE (BGP): 
	- corre solo en puertas de enlace, 
	- aprende rutas externas, 
	- aplica política, 
	- agrega prefijos, 
	- inyecta LSAsexternos en el PPEI. 
Superposición de grafos, no un grafo global: El PPEI mantiene la topología interna, el PPEE intercambia rutas externas entre WANs.

## Suposiciones iniciales
- Asumimos que tenemos una red donde las WAN son usadas por proveedores de servicios de red. En internet estas WAN se llaman **sistemas autónomos (SA)**. 
- Asumimos que cada WAN corre OSPF. 
- El enrutamiento de PPEE se preocupa de establecer las rutas a usar (que pasan por diferentes WAN) para permitir que se comuniquen máquinas pertenecientes a distintas WAN. 
- Para enrutamiento PPEE encontrar un camino óptimo es imposible en la práctica porque en cada WAN OSPF usa criterios diferentes para determinar costos de enlaces.

## Agregación en la puerta de enlace
La operación clave que permite escalar

La puerta de enlace aprende miles de rutas externas por medio de BGP,  aplica sus políticas y realiza agregación de prefijos de esas rutas para sintetizar varios destinos en uno más compacto. 

El resultado es un prefijo agregado que se inyecta dentro del dominio OSPF como un paquete de estado de enlace externo (que contiene el prefijo agregado y el next-hop hacia la puerta de enlace) que es difundido por OSPF por todas las áreas. De este modo, todos los enrutadores internos pueden reenviar tráfico hacia redes externas sin conocer la complejidad del enrutamiento inter-WAN. Solo ven:  “este prefijo externo está detrás de esta puerta de enlace”. 

La puerta de enlace actúa así como un punto de condensación que protege la red interna del caos externo, manteniendo las tablas internas pequeñas, estables y completamente independientes de la dinámica del protocolo exterior

## Información de rutas
Como no se puede manejar información de caminos óptimos, ¿qué tipo información sobre rutas manejar? 
	• Cuando un enrutador avisa una LAN, incluye con la dirección de la LAN, una ruta que pasa por varias WAN para llegar a la LAN. 
	• Una ruta se compone de los siguientes elementos: 
	- NEXT-HOP: la dirección de la interfaz de la puerta de enlace que comienza la ruta hacia la LAN de destino.
	-  WAN PATH: contiene las WAN por las cuales el aviso de la LAN de destino ha pasado. 
	-  Dirección de LAN de destino: por ejemplo, un rango de direcciones de interfaz o un prefijo
![[Pasted image 20260526160429.png]]
![[Pasted image 20260526191612.png]]


## Relaciones entre las WAN
Si hay una **relación de proveedor-consumidor** en las WAN, los tipos de ruta que publica la WAN proveedor son las rutas a todos los destinos en la interred al consumidor sobre el enlace que los conecta. Así el consumidor va a tener rutas para enviar paquetes para todos lados.
Y el tipo de rutas que publica la WAN consumidora, son rutas a los destinos en su red al proveedor. Esto permite al proveedor enviar tráfico al consumidor solo para esas direcciones.

Si hay una **relación de compañerismo,** los SA (Sistemas Autónomos) compañeros mandan publicidad de enrutamiento de uno al otro para los destinos que residen en sus redes.


## Función de las puertas de enlace
 Para el enrutamiento es necesario encontrar algún camino de WANs para la LAN de destino deseado que es libre de ciclos. Además, los caminos deben respetar las políticas de las WAN a lo largo del camino. 
 
 Tareas que hace una puerta de enlace: 
 - Tiene que hacer una elección de varias rutas a una LAN de destino; 
 - va a elegir la mejor de acuerdo con sus propias políticas locales y esta va a ser la ruta que avisa. 
 - Una puerta de enlace avisa el camino exacto que está usando para cada destino.

## Sesiones BGP
Una vez que la puerta de enlace agrega prefijos y los inyecta como LSAs (Link State Advertisement) externos en OSPF, la red interna queda completamente aislada de la complejidad del enrutamiento entre sistemas autónomos., pero este aislamiento solo es posible si el intercambio de rutas externas se realiza fuera del dominio OSPF, mediante un mecanismo que no dependa de inundación ni de topología interna. 

Aquí es donde aparece la necesidad de **sesiones BGP:** conexiones lógicas punto a punto entre puertas de enlace que permiten transportar rutas externas de manera confiable, controlada y sujeta a políticas. Estas sesiones reemplazan la inundación del modelo anterior y se convierten en el **canal exclusivo por el cual los sistemas autónomos negocian, filtran y actualizan la información** de prefijos que luego será agregada e inyectada hacia adentro.

En otras palabras, para que la red interna permanezca simple, estable y protegida, el intercambio exterior debe pasar a un plano separado, sostenido por sesiones BGP.

>[!question]-  ¿Cómo hacer para evitar inundación? 
La clave: sesiones explícitas entre puertas de enlace. 
Las rutas externas se intercambian a través de una sesión, es decir, una conexión lógica punto a punto entre dos puertas de enlace. Cada sesión se transporta sobre TCP, que brinda confiabilidad y orden, y TCP a su vez, se enruta usando la tabla de reenvío interna construida por OSPF. 
Al apoyarse en el mecanismo de reenvío común, las rutas externas no se inundan dentro de la WAN:
> - No hay duplicados de avisos ni propagación indiscriminada. 
> - La sesión es lógica, no física: no depende de la topología interna de la WAN. 
> -  Cada sesión es explícita, controlada y establecida solo entre puertas de enlace, lo que permite aplicar políticas finas y mantener la independencia entre dominios

Problema: ¿Cómo hacer para propagar información de rutas en BGP de manera confiable?  

En BGP pares de puertas de enlace intercambian información de rutas sobre conexiones TCP semipermanentes usando el puerto 179.  Hay típicamente una conexión BGP TCP para:
-  cada enlace que conecta directamente dos puertas de enlace (o enrutadores BGP) en dos SA diferentes y
-  Entre puertas de enlace dentro del SA 
Para cada conexión TCP, los 2 enrutadores al final de la conexión se llaman compañeros BGP. Los compañeros BGP se avisan rutas.

Sesiones BGP: 
- La conexión TCP con todos los mensajes BGP enviados por la conexión se llama sesión BGP.
- Una sesión BGP entre puertas de enlace de dos SA se llama sesión externa BGP (eBGP) 
- Una sesión BGP entre puertas de enlace en el mismo SA se llama sesión interna BGP (iBGP) 
- **Las líneas de las sesiones BGP no siempre se corresponden con los enlaces físicos.**

![[Pasted image 20260526194327.png]]

Una sesión BGP es una relación lógica entre dos puertas de enlace, no una relación física entre enrutadores adyacentes.

>[!info] ¿Cómo viaja un aviso BGP? 
>- Una puerta de enlace genera un mensaje de aviso. 
>- Este mensaje se encapsula en BGP. 
>- El mensaje TCP se encapsula en IP. 
>- El paquete IP se reenvía usando la tabla de reenvío creada por OSPF. 
>- Los enrutadores internos tratan el paquete IP como tráfico normal, no como control

¿Cómo se garantiza que un aviso de ruta llegue?

 Antes de establecer una sesión BGP, cada puerta de enlace debe verificar que la otra es alcanzable por IP usando el OSPF. Si OSPF puede llevar paquetes IP hasta la otra puerta de enlace, entonces:
 - Establece sesión BGP con la otra pueta de enlace. 
 - La conexión TCP queda abierta durante horas o días. 
 - Los avisos BGP fluyen por esa sesión. 
 - Si la sesión se cae, BGP la vuelve a intentar. 
 Todas las puertas de enlace corren TCP. 
 >[!tip] Una sesión BGP no se crea para cada aviso. Se crea una vez, se mantiene abierta y todos los avisos viajan por ella.
 
## AS-PATH
(Path de Sistemas Autónomos)
Evita loops sin depender de la topología .
La clave: trayectoria explícita, no conocimiento global
- Cada anuncio lleva la secuencia de SAs por la que pasó (AS-PATH). 
- Si un SA aparece dos veces se detecta un loop inmediatamente. 
- No se necesita topología global ni mapas de la interred. 
- Permite política basada en trayectoria (preferencias, restricciones, filtrado por origen o camino)

## Mensajes BGP
Una vez establecidas las sesiones BGP entre puertas de enlace, el siguiente paso es entender qué viaja realmente por esas sesiones. 

La sesión define el canal: confiable, punto a punto, sostenido por TCP y aislado de la topología interna, pero el funcionamiento del protocolo depende de los mensajes que se intercambian a través de ese canal, porque son ellos los que permiten anunciar prefijos, retirar rutas, mantener viva la sesión y negociar capacidades. En otras palabras, si la sesión es el “túnel” que conecta dos sistemas autónomos, los mensajes BGP son el contenido que circula dentro de ese túnel, y constituyen el mecanismo concreto mediante el cual se propagan rutas externas y se aplican políticas.

Los mensajes de BGP son cuatro y cada uno cumple una función específica dentro del establecimiento y mantenimiento de la sesión BGP y el intercambio de información de enrutamiento. 
- **OPEN:** inicia la sesión BGP tras establecer TCP.
- **UPDATE:** anuncia o retira rutas. 
- **KEEPALIVE:** mantiene viva la sesión. 
- **NOTIFICATION:** informa errores y cierra la sesión

#### Mensaje OPEN
 Se envía después de establecer la conexión TCP.  Negocia parámetros esenciales: 
 - versión de BGP, 
 - SA local, 
 - Hold Time, 
 - Router ID, 
 - Capabilities (IPv6, multipath, etc.). 
 Si ambos extremos aceptan los parámetros → la sesión continúa. Normalmente se envía un KEEPALIVE inmediatamente después

#### Mensaje UPDATE 
Anuncia nuevas rutas o retira rutas inválidas. 
 Contiene atributos BGP (AS-PATH, NEXT_HOP, LOCAL_PREF, etc.) y se envía cada vez que cambia la mejor ruta conocida. 
Estructura exacta del UPDATE:
1. Withdrawn Routes Length 
2. Withdrawn Routes (prefijos retirados) 
3. Total Path Attribute Length
4. Path Attributes
5. NLRI (prefijos anunciados)

#### Mensaje KEEPALIVE
Se envía periódicamente si no hay UPDATEs.  Evita que la sesión se cierre por inactividad y el intervalo depende del Hold Time negociado en el OPEN., si el Hold Time = 0 → no se envían KEEPALIVE

#### Mensaje NOTIFICATION
Se envía cuando ocurre un error que requiere terminar la sesión. Indica la causa del error (mensaje mal formado, parámetros inválidos, timeout, etc.).  Tras enviarlo, el enrutador cierra la conexión TCP inmediatamente. **No se usa para advertencias menores: solo para errores críticos**


### Flujo típico de una sesión BGP: 
1. Se establece la conexión TCP entre puertas de enlace. 
2. Se intercambian mensajes OPEN. 
3. Se envía un KEEPALIVE inicial para confirmar la sesión. 
4. Se intercambian UPDATEs para anunciar/retirar rutas. 
5. Se envían KEEPALIVE periódicos si no hay UPDATEs. 
6. Si ocurre un error → NOTIFICATION → cierre de sesión

## Estructuras internas de BGP
Una vez que entendemos cómo se establecen las sesiones BGP y qué mensajes circulan por ellas, el siguiente paso natural es preguntarnos dónde y cómo se almacena toda esa información dentro de una puerta de enlace. 

Los mensajes son el mecanismo de intercambio, pero no son el estado del protocolo: cada puerta de enlace debe mantener registros persistentes de todas las rutas aprendidas, de las rutas seleccionadas y de las rutas que decide anunciar. Para eso, BGP organiza su información en un conjunto de estructuras internas que separan claramente lo que se recibe, lo que se decide usar y lo que se anuncia. 
Estas estructuras permiten aplicar políticas, comparar rutas, elegir la mejor y mantener coherencia sin depender de la topología interna. Pasamos ahora a estudiar estas estructuras, que constituyen el “sistema nervioso” del funcionamiento interno de BGP.

>[!question] ¿Qué necesita almacenar una puerta de enlace BGP? 
Necesitamos guardar todo lo recibido, incluso lo que no vamos a usar. Después procesaremos esas rutas filtrando por política y eligiendo la mejor ruta por destino. También debemos preparar rutas para anunciar hacia afuera. 
Conclusión: necesitamos una estructura para almacenar todas las rutas recibidas

#### Estructura 1: Adj-RIB-In 
Guarda todas las rutas recibidas de cada vecino BGP. 
Hay una Adj-RIB-In por vecino y dentro de cada una se organizan las rutas por prefijo, junto con sus atributos BGP. 
Necesitamos Adj-RIB-In porque no podemos decidir nada sin ver todas las rutas recibidas. • Se actualiza con cada mensaje UPDATE recibido. 
- Si llega una ruta por primera vez para un prefijo de un vecino: se la agrega. 
- Si llega una ruta actualizada para un prefijo de un vecino (p.ej. cambió el AS_PATH o el NEXT_HOP): la ruta actualizada reemplaza la anterior para ese vecino. 
- Si llega un retiro, se elimina la ruta correspondiente de la tabla.

Una vez que se filtran las rutas de Adj-RIB-In por política y se elige la mejor ruta por destino, hace falta una estructura extra para guardar esta información, pues se tiene en cuenta para: 
- decidir si se anuncian hacia otros SA, 
- Inyectarlas en OSPF y, 
- para actualizar la tabla de reenvío. 
Usamos entonces Loc-RIB

#### Estructura 2: Loc-RIB (la tabla de mejores rutas) 
Guarda una única mejor ruta por destino.  Es el resultado del proceso de selección. 
Dedujimos: Adj-RIB-In → selección → Loc-RIB

Con estas estructuras ya podemos: aplicar política, elegir rutas, anunciar rutas, inyectar rutas en OSPF. Esto es suficiente para un protocolo derivado desde primeros principios. • Pero BGP termina agregando dos estructuras más por razones operativas, no conceptuales.

#### Estructura 3: Adj-RIB-Out 
Guarda las rutas preparadas para enviar a cada vecino BGP. 
Permite aplicar políticas de exportación. Se construye a partir de la Loc-RIB aplicando políticas de salida. Puede haber diferencias en las rutas anunciadas a distintos vecinos, incluso para el mismo prefijo. 

#### Estructura 4:  RIB(Routing Information Base) 
Solo las rutas seleccionadas en la Loc-RIB que son mejores que las rutas existentes en la RIB se instalan en la RIB para ser usadas en el reenvío de paquetes. Las rutas de Loc-RIB se comparan con otras rutas en la RIB para decidir cuál ruta se instala para el encaminamiento. 
>[!tip] La RIB no es parte de BGP: es parte del sistema operativo del enrutador


## Política en BGP
Una vez que entendemos cómo BGP organiza internamente la información —separando lo que recibe, lo que selecciona y lo que anuncia mediante sus distintas RIBs— aparece de inmediato la pregunta clave: ¿cómo decide una puerta de enlace qué rutas usar y cuáles propagar? 

Las estructuras internas no son solo un mecanismo de almacenamiento; son el espacio donde se aplican las reglas administrativas que cada sistema autónomo impone sobre el tráfico que acepta y el tráfico que anuncia. En otras palabras, las RIBs son el soporte técnico que permite implementar la política de enrutamiento, que es el verdadero corazón del funcionamiento de BGP. 

**El PPEE como mecanismo administrativo, no solo técnico** 
	La política es el corazón del diseño exterior:
	- Qué anunciar a otros SA. 
	- Qué aceptar de los vecinos. 
	- Qué preferir entre múltiples rutas externas. 
	- Qué evitar según restricciones administrativas. 
	- Cómo influir en el tráfico entrante y saliente. 
	La idea central: La política no es un accesorio, es la función principal del PPEE y la razón por la que existe

En conjunto, estas políticas permiten controlar el flujo de información de enrutamiento, optimizar rutas, evitar bucles, cumplir acuerdos comerciales y mantener la estabilidad y seguridad de la red.  

**Políticas de entrada (import policies)** 
Se aplican a rutas recibidas antes de entrar a la Loc-RIB: 
- Filtrar rutas no deseadas. 
- Modificar atributos (ej. LOCAL_PREF) para influir en la selección. 
- Clasificar rutas para reglas internas (El uso de comunidades para esto queda en material opcional.)

**Políticas de salida (export policies)**
Se aplican a rutas anunciadas a los vecinos: 
- Filtrar rutas que no deben enviarse. 
- Modificar atributos como AS_PATH al anunciar rutas externas. 
- Controlar anuncios según acuerdos o topología. (El uso de comunidades para esto también queda en material opcional.) 

## Atributos adicionales para ruta
Una vez entendidas las políticas en BGP —qué rutas se aceptan, cuáles se descartan y cuáles se anuncian— surge naturalmente la siguiente pregunta: **¿cómo decide una puerta de enlace entre varias rutas aceptables hacia un mismo prefijo?**

 Las políticas permiten filtrar y moldear el conjunto de rutas candidatas, pero no determinan por sí mismas cuál es la mejor. Para eso, BGP necesita información adicional: un conjunto de atributos de ruta que describen propiedades del camino, preferencias administrativas y características operativas.  Estos atributos —como LOCAL_PREF, AS-PATH, MED, NEXT_HOP, entre otros— son los insumos que alimentan el proceso de selección.

Vemos dos atributos adicionales, los cuales introducimos con problemas:
#### LOCAL_PREF
Problema: muchas veces un SA tiene varias puertas de enlace alternativas para salir hacia un destino externo. Pero no todas son equivalentes:
- algunas salidas son mas convenientes por costos, 
- otras tienen mayor capacidad (tasa de datos), 
- otras se prefieren por relaciones comerciales (compañerismo, cliente-proveedor), 
- o se desea privilegiar ciertos acuerdos con otros SA. 
Y el atributo AS-PATH no puede expresar política interna. Solo describe la trayectoria, no las preferencias del SA. 

BGP usa el atributo LOCAL-PREF para asignar preferencias internas. 
LOCAL-PREF se usa dentro del SA y es un  atributo para las rutas: cuanto mayor valor, más preferida la ruta.  Permite expresar política interna de forma simple y determinista. 
¿Cómo se aplica? Basta con asignar distintos valores de LOCAL_PREF a las rutas según la puerta de enlace de salida. 
#### MED
Problema: Un SA puede tener múltiples puertas de enlace por las que un SA conectado a él puede entrar. Pero no todas las entradas son iguales: 
- algunas tienen mayor capacidad, 
- otras están menos congestionadas, 
- algunas son mas baratas o preferidas por acuerdos, 
- otras se quiere desalentar para balancear la carga.
El atributo AS-PATH tampoco puede expresar preferencias entrantes. Solo describe la trayectoria, no cuál entrada conviene usar. 
La necesidad: Si vas a entrar a mi SA, preferí esta puerta de enlace. Pero sin imponerlo, porque BGP es un protocolo entre administraciones independientes. 

BGP usa el atributo MED (Multi Exit Discriminator) 
Cuanto menor el valor, más preferida la entrada. Se envía hacia afuera, al vecino, y permite expresar preferencias entrantes sin modificar el AS-PATH. 
Es una sugerencia, que el vecino puede respetar o no. 

¿Cómo se aplica? Asignando distintos valores de MED a las rutas según la puerta de enlace por la que se desea que entren. 
>[!tip] MED complementa LOCAL-PREF: uno decide por donde salgo y el otro sugiere por dónde entran

## Elección de ruta a un prefijo
Situación: Un enrutador puede recibir múltiples rutas al mismo prefijo. La mejor ruta a un prefijo debe guardarse en la Loc-RIB. 
Problema: ¿Cómo escoge el enrutador una de esas rutas al mismo prefijo? 
Para elegir una sola, hay que aplicar un algoritmo determinista sobre las rutas en la Adj-RIB-In

#### Solución (estándar RFC 4271): 
1. **Verificar NEXT_HOP alcanzable:** el NEXT_HOP debe poder resolverse en la tabla de enrutamiento local. Si no es alcanzable, la ruta se descarta.
2. **LOCAL_PREF**: Las rutas con el mayor valor LOCAL-PREF son elegidas. Este valor puede ser fijado por el enrutador o aprendido dentro del mismo SA. Es un atributo propagado internamente que expresa política del SA. 
3. **Longitud del AS_PATH:** Entre las rutas restantes, la ruta con el AS PATH más corto es elegida (cantidad de saltos SA). 
4. **MED:** Se prefiere la ruta con el MED más bajo. Por defecto, se compara solo entre rutas provenientes del mismo SA vecino 
5. **Preferir rutas eBGP sobre iBGP:** Si aun hay empate, se prefiere la ruta aprendida por eBGP antes que una aprendida por iBGP. 
6. **Costo IGP al NEXT_HOP (hot-potato routing):** Se elige la ruta cuyo NEXT-HOP está más cerca según el PPEI. El SA se saca el tráfico de encima lo antes posible.
7. **Ruta más antigua:** para evitar oscilaciones, se prefiere la ruta aprendida primero. 
8. **Router ID del vecino:** Si persiste el empate, se elige la ruta al vecino con el Router ID más bajo. 
9. **Dirección IP del vecino:** Último desempate: se elige la ruta del vecino con la IP más baja

Algoritmo fijo, política flexible 
Tenemos entonces un único algoritmo estándar: Todos las puertas de enlace usan la misma secuencia para elegir la mejor ruta. Este orden está definido en una RFC y no se modifica

La razón es asegurar la interoperabilidad global entre miles de SA independientes, pero cada SA controla las entradas al algoritmo: Antes de que el algoritmo compare rutas, el SA puede aplicar políticas propias: Cambiar LOCAL-PREF, ajustar MED, filtrar rutas, reescribir AS-PATH, agregar comunidades (material opcional), modificar atributos según acuerdos comerciales.

 Resultado: cada SA toma decisiones diferentes , sin romper el estándar

![[Pasted image 20260526205528.png]]
![[Pasted image 20260526205544.png]]

## Creación de entrada en la tabla de reenvío
Una vez que BGP completa el proceso de selección y determina la mejor ruta hacia un prefijo, el protocolo ya no tiene más decisiones que tomar sobre ese destino. A partir de ese momento, el problema deja de ser “¿qué ruta prefiero?” y pasa a ser “¿cómo hago para que los paquetes realmente sigan ese camino?”. Aquí es donde BGP entrega el control al plano de reenvío: la ruta seleccionada se traduce en un siguiente salto concreto, que debe instalarse en la tabla de reenvío interna del enrutador.

Esta instalación no copia toda la información de BGP, sino solo lo necesario para reenviar paquetes: el prefijo y la interfaz o puerta de salida correspondiente. Con este paso, la decisión de BGP se convierte en acción operativa, y el tráfico real comienza a fluir siguiendo la ruta elegida

Ejercicio: Dado el aviso de ruta al sistema autónomo AS1
- Prefijo 138.16.64/22, 
- AS-PATH: AS2 AS17 ; 
- NEXT-HOP: 111.99.86.55
Supongamos que es el único aviso de ruta a ese prefijo y que respeta las políticas de AS1.o ¿Cómo hace el enrutador 1c para poner entrada para el prefijo anterior en su tabla de reenvío?![[Pasted image 20260526210525.png]]

Solución: 
- 1c provee la dirección IP del atributo NEXT-HOP al algoritmo OSPF. 
- 1c usa OSPF para encontrar el camino más corto de 1c a la subred para el enlace entre 1b y 2a (que tiene 111.99.86.55). 
- Supongamos que el puerto de 1c a lo largo de ese camino más corto es el puerto 4.
- Entonces 1c agrega el puerto 4 de entrada para el prefijo de la red de destino a su tabla de reenvío: o ``(138.16.64/22 , port 4)``
![[Pasted image 20260526210540.png]]


Problema: **¿cómo determina un enrutador por qué puerto reenviar paquetes hacia un prefijo externo (perteneciente a otro SA)?** 

BGP sólo indica qué ruta es la mejor, pero no especifica cómo llegar físicamente al NEXT-HOP. Solución: La RIB contiene la ruta óptima R al prefijo x. Para convertir esta ruta en una entrada de reenvío, el enrutador debe: 
1. Resolver el NEXT-HOP de R usando OSPF. 
2. Usar OSPF para encontrar la mejor ruta intra-SA hacia ese NEXT_HOP.
3. identificar el puerto de salida asociado a esa ruta interna.
4. Instalar la entrada en la tabla de reenvío asociando: prefijo x -> puerto de salida correspondiente al NEXT HOP. 

**Sincronización continua:**  La tabla de reenvío se actualiza automáticamente cuando cambian: la topología interna (OSPF) , las rutas BGP, ó el NEXT-HOP.  De esta forma el plano de reenvío siempre refleja el estado actual del SA.

## Recapitulación
Uso de estructuras internas: 
- Los avisos recibidos se guardan en RIB de entrada (Adj-RIB-In). 
- Sobre esta base se aplican las políticas de entrada y luego se eligen las mejores rutas. 
- Las rutas seleccionadas se guardan en la RIB de decisión (Loc-RIB). 
- Desde las Loc-RIB se aplican las políticas de salida y el resultado se guarda en RIB de salida (Adj-RIB-Out), desde donde se extraen los avisos que se envían por las sesiones BGP.

![[Pasted image 20260526211226.png]]

 Ideas clave del bloque 
 - La separación PPEI/PPEE es esencial para escalar. 
 - Los enrutadores internos no deben ver rutas externas. 
 - Las puertas de enlace agregan prefijos antes de inyectarlos en OSPF. 
 - Las sesiones TCP permiten control fino, confiabilidad y no-inundación. 
 - El AS-PATH evita loops sin necesidad de topología global. 
 - Las políticas determinan qué se anuncia y qué se acepta