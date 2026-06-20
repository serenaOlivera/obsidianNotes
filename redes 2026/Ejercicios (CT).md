## Capa de transporte y TCP
#### Ejercicio 1 — Verdadero o Falso «La capa de transporte se ejecuta tanto en los hosts como en los routers intermedios.»
**Respuesta:** FALSO. Se ejecuta solo en los hosts/sistemas finales. Los routers solo reenvían paquetes sin inspeccionar la capa de transporte.

#### Ejercicio 2 — Verdadero o Falso «TCP ve los datos de la aplicación como mensajes individuales y los  transmite respetando sus límites.»
**Respuesta:** FALSO. TCP no conoce los límites de los mensajes de la aplicación: ve un flujo continuo de bytes (stream) y lo fragmenta en segmentos según convenga.

#### Ejercicio 3 — Multiple Choice
¿Qué es un «segmento» en el contexto de TCP?
a) Un paquete de la capa de red
b) La unidad de datos del protocolo de transporte (TPDU)
c) Una trama de la capa de enlace
d) Un datagrama IP completo
>[!info]- **Respuesta:** 
>b) El segmento es la unidad de datos de la capa de  transporte. Se encapsula dentro de un paquete IP (capa de red).

#### Ejercicio 4 — Completar (cálculo)
El campo «longitud del encabezado» tiene 4 bits. ¿Cuál es el número máximo de palabras de 32 bits que puede tener el encabezado TCP? 
>[!info]- **Respuesta:** 
>15. Con 4 bits el valor máximo es 2⁴ - 1 = 15, osea puedo direccionar 15 palabras de 32 bits
> 32 bits son 4 bytes ( pues 1 byte son 8 bits, entonces 32/8=4 ). Eso equivale a 15 palabras × 4 bytes = 60 bytes

#### Ejercicio 5 — Completar (cálculo)
Si el encabezado fijo de TCP mide 20 bytes y el máximo es 60 bytes, ¿cuántos bytes pueden ocupar las opciones como máximo? 
>[!info]- **Respuesta:** 
>40 bytes. 60 bytes (máximo total) - 20 bytes (encabezado fijo) = 40 bytes para opciones.

#### Ejercicio 6 — Verdadero o Falso
«Un socket se identifica únicamente con el número de puerto.»
>[!info]- **Respuesta:** 
>FALSO. Un socket = dirección IP + puerto. Dos hosts distintos pueden usar el mismo puerto (ej.: ambos en puerto 80), pero sus sockets son diferentes porque tienen distinta IP.

#### Ejercicio 7 — Completar (cálculo)
Un host recibió correctamente todos los bytes de un flujo TCP hasta el byte 4999 ¿Qué valor tendrá el campo ACK number en su próximo segmento? 
>[!info]- **Respuesta:** 
>5000. El ACK number indica el siguiente byte esperado. Si recibió hasta el 4999,espera el 5000.

#### Ejercicio 8 — Verdadero o Falso
«Si el flag ACK vale 0, el campo número de confirmación contiene un valor válido.»
>[!info]- **Respuesta:**
> FALSO. Cuando ACK = 0, el campo se ignora. Solo es válido cuando ACK = 1.

#### Ejercicio 9 — Completar (cálculo)
Un enlace tiene MTU de 1500 bytes. IP ocupa 20 bytes y TCP ocupa 20 bytes. ¿Cuál es el MSS? 
>[!info]- **Respuesta:**
> 1460 bytes. MSS = MTU - IP - TCP = 1500 - 20 - 20 = 1460 bytes.

#### Ejercicio 10 — Multiple Choice
¿Qué flag del encabezado TCP se utiliza para iniciar una conexión?
a) FIN b) RST c) SYN d) PSH
>[!info]- **Respuesta:**
> c) SYN. SYN (synchronize) se usa para solicitar el establecimiento de una conexión TCP.

#### Ejercicio 11 — Multiple Choice
¿Para qué sirve la opción MSS en el encabezado TCP?
a) Indicar el tamaño de la ventana de congestión
b) Negociar el tamaño máximo de segmento que acepta cada lado
c) Definir el número de secuencia inicial
d) Establecer el tiempo de vida del paquete
>[!info]- **Respuesta:**
> b) MSS (Maximum Segment Size) se negocia al inicio de la conexión para que cada lado informe el tamaño máximo de datos que puede recibir por segmento.

#### Ejercicio 12 — Verdadero o Falso
«Una conexión TCP se identifica de forma única por un solo socket (IP + puerto).»
>[!info]- **Respuesta:**
> FALSO. Una conexión TCP se identifica por el par (socket_origen, socket_destino), es decir, dos sockets: uno en cada extremo.

## Direccionamiento
#### Pregunta 1: ¿Cuál es la diferencia fundamental entre la solución del servidor de procesos y la solución del servidor de directorio?
>[!info]- **Respuesta:** 
>El servidor de directorio resuelve el problema de descubrimiento: el cliente no sabe en qué puerto escucha el servicio, y el directorio le indica la dirección. Asume que el servidor ya está activo. El servidor de procesos resuelve el problema de activación: el cliente conoce el puerto, pero el servidor está inactivo, y el servidor de procesos lo genera (fork) bajo demanda y le transfiere la conexión. 

#### Pregunta 2: ¿En qué escenario haría falta combinar ambas soluciones?
>[!info]- **Respuesta:**
> Cuando el cliente no conoce el puerto del servicio y además el servidor está inactivo. Primero se consulta al servidor de directorio para descubrir el puerto, y luego el servidor de procesos se encarga de activar el demonio correspondiente para atender la solicitud. Se combinan ambos mecanismos en secuencia: descubrimiento + activación

#### Ejercicio 1: Análisis de Escenarios
• Para cada situación, indicar qué mecanismo se necesita: servidor de directorio, servidor de
procesos, ambos o ninguno. Justificar.
>[!example]- Un navegador web quiere conectarse al servidor HTTP de una máquina remota. Sabe que HTTP usa el puerto 80, y el servidor está activo permanentemente como demonio.
> >[!info]- Ninguno. El cliente ya conoce el puerto (80 es well-known) y el servidor está activo como demonio permanente. No se necesita descubrimiento ni activación

>[!example]- Una aplicación necesita un servicio de impresión remota. Sabe que el servicio existe en la máquina destino pero desconoce en qué puerto escucha.
> > [!info] Servidor de directorio. El problema es de descubrimiento: el cliente no sabe el puerto. Consulta al directorio, que le devuelve la dirección del servicio de impresión. El servicio se asume activo.

>[!example]- Un cliente quiere usar el servicio finger (puerto 79) en un servidor Unix. El servicio está configurado en /etc/inetd.conf pero no hay ningún demonio finger corriendo actualmente.
> >[!info] Servidor de procesos (inetd). El problema es de activación: el cliente conoce el puerto 79, pero el demonio está inactivo. inetd escucha en ese puerto, recibe la solicitud, genera (fork) el proceso finger y le transfiere la conexión

>[!example]- Un proceso cliente necesita un servicio personalizado que fue recién instalado en el servidor. No conoce su puerto, y el servicio solo se activa bajo demanda mediante inetd.
> >[!info]- Ambos. Hay dos problemas simultáneos: no conoce el puerto (→ directorio) y el servicio se activa bajo demanda (→ servidor de procesos/inetd). Primero consulta al directorio para descubrir el puerto, luego inetd activa el servicio al recibir la conexión

>[!example]- Un administrador tiene un servidor con 50 servicios distintos pero solo 5 se usan frecuentemente. ¿Qué estrategia de  direccionamiento/activación debería implementar para optimizar el uso de memoria?
> >[!info] Estrategia híbrida. Los 5 servicios frecuentes se configuran como demonios permanentes (evitar la latencia de fork). Los 45 restantes se gestionan con inetd para ahorrar memoria, activándolos solo bajo demanda.**


#### Ejercicio 2: Verdadero o Falso
• Indicar si cada afirmación es verdadera o falsa. Si es falsa, corregirla.
   >[!question]- 1- El servidor de directorio y el servidor de procesos resuelven el mismo problema de direccionamiento.
   >FALSA. Resuelven problemas diferentes: el directorio resuelve el descubrimiento del puerto; el servidor de procesos resuelve la activación del proceso servidor inactivo

   >[!question]- 2- Los puertos bien conocidos (well-known ports) son aquellos con números menores a 1024, reservados para servicios estándar.
   VERDADERA. Los puertos 0-1023 están reservados por IANA para servicios estándar (ej: HTTP=80, FTP=21, SSH=22).

   >[!question]- 3- El demonio inetd necesita tener todos los servidores cargados en memoria permanentemente para poder redirigir las solicitudes.
   FALSA. Justamente lo contrario: inetd evita tener los servidores en memoria. Solo inetd está activo, escuchando en múltiples puertos, y genera (fork) cada servidor bajo demanda cuando llega una solicitud.
   
   >[!question]- En el protocolo inicial de conexión, el servidor de procesos genera (fork) el servidor solicitado y le permite heredar la conexión existente con el cliente.
   VERDADERA. El servidor de procesos hace fork, creando un proceso hijo que hereda los descriptores de archivo (incluida la conexión TCP con el cliente), y el padre vuelve a escuchar.

   >[!question]- 5- Para registrar un nuevo servicio en un servidor de directorio, basta con que el cliente envíe una solicitud de conexión al puerto deseado.
   FALSA. El registro lo hace el servidor (no el cliente): el nuevo servicio debe enviar su identificador y puerto al servidor de directorio para que este lo incluya en su tabla de búsqueda.

>[!question]- 6- En la práctica, todos los servicios de un servidor Unix deberían ser gestionados por inetd para minimizar el consumo de memoria.
   FALSA. La estrategia óptima es híbrida: los servicios de alto tráfico (HTTP, SSH) deben ser demonios permanentes para evitar la latencia de fork; solo los servicios esporádicos se gestionan con inetd.
   
   >[!question]- 7- El servidor de directorio necesita escuchar en un puerto bien conocido para que los clientes puedan contactarlo sin necesitar otro directorio.
   VERDADERA. Si el propio directorio no tuviera un puerto conocido, se crearía un problema de recursividad infinita (¿quién me dice dónde está el directorio?). Por eso el directorio siempre usa un puerto well-known.

#### Ejercicio 3: Diseño de Solución
• Situación: Una universidad tiene un servidor central con 30 servicios disponibles para los alumnos (correo, FTP, SSH, bases de datos, impresoras, consulta de notas, etc.). Solo 4 servicios se usan constantemente (correo, SSH, DNS, HTTP). Los demás se usan esporadicámente.

• Se pide diseñar la estrategia de direccionamiento y activación del servidor, respondiendo:
a) Clasificar: ¿Cuáles servicios configuraría como demonios permanentes y cuáles gestionaría mediante inetd? Justificar el criterio utilizado.

   >[!question]- Respuesta
>Clasificar: Demonios permanentes: Correo, SSH, DNS y HTTP (alto tráfico → evitar latencia de fork en cada solicitud). Gestionados por inetd: Los 26 restantes (FTP, bases de datos, impresoras, consulta de notas, etc.) → uso esporádico, no justifica ocupar memoria permanentemente. Criterio: frecuencia de uso y tiempo de respuesta aceptable

b) Directorio: Un alumno quiere usar el servicio de “consulta de notas” pero no conoce su puerto. ¿Qué pasos seguiría el sistema para resolver esta solicitud?
   >[!question]-  Respuesta
Directorio: 
>1) El cliente del alumno contacta al servidor de directorio (puerto well-known). 
>2) Envía un lookup con el identificador “consulta de notas”.
>3) El directorio busca en su tabla y responde con el puerto asignado. 
>4) El cliente se conecta a ese puerto. 
>5) Como está gestionado por inetd, este recibe la conexión, hace fork del proceso y le transfiere la conexión.

c) Nuevo servicio: Si se agrega un servicio de “reserva de aulas”, ¿qué pasos debe realizar el administrador para que los clientes puedan descubrirlo y utilizarlo?

>[!question]- Respuesta:
>Nuevo servicio: El administrador debe: 
>1) Asignar un puerto al servicio “reserva de aulas”.
>2) Agregar una entrada en /etc/inetd.conf con el puerto, protocolo y ruta del ejecutable.
>3) Registrar el servicio en el servidor de directorio (enviar identificador + puerto).
>4) Reiniciar inetd para que lea la nueva configuración. Los clientes podrán descubrirlo vía directorio y será activado bajo demanda por inetd.

d) Diagrama: Dibujar el flujo completo de mensajes entre el cliente, el servidor de directorio e inetd cuando un alumno accede al servicio de “consulta de notas” por primera vez.

Cliente → 
Srv. Directorio: “¿puerto de consulta de notas?” →
Directorio responde: “puerto N” →
Cliente se conecta a puerto N → 
inetd (escuchando en N) acepta conexión → 
inetd hace fork del proceso “consulta_notas” →
Hijo hereda conexión y atiende al cliente → 
inetd vuelve a escuchar
## Transferencia de datos confiable

>[!info]- P1. ¿Por qué Parada y Espera necesita números de secuencia si solo envía un paquete a la vez?
Para detectar paquetes duplicados. Si el ACK se pierde, el emisor retransmite. Sin N° de
secuencia, el receptor no sabría si es un paquete nuevo o una copia.

>[!info]- P2. En Retroceso-N, ¿por qué el receptor descarta paquetes fuera de orden en lugar de almacenarlos?
R: GBN usa ACK acumulativo: confirma hasta el último paquete recibido en orden. Guardar
los desordenados obligaría a manejar un buffer complejo en el receptor, lo cual contradice
la filosofía de simplicidad del receptor de GBN.

>[!info]- P3. ¿Cuál es la ventaja principal de Repetición Selectiva sobre Retroceso-N?
➤ R: SR solo retransmite el paquete perdido, no toda la ventana. En redes con alta tasa de
errores y ventanas grandes, esto ahorra mucho ancho de banda. El costo: receptor más
complejo con buffer.

### ejercicio 2
Datos: Enlace de 100 Mbps, propagación 25 ms, paquetes de 10.000 bits. ACK
despreciable.
a) Calcule U para Parada y Espera.
>[!question]- Respuesta:
> Denvío = L/R = 10.000 / 100×106 = 0,1 ms. RTT = 2 × 25 ms = 50 ms.
➤ U = Denvío / (RTT + Denvío) = 0,1 / (50 + 0,1) = 0,002 = 0,2% → ¡muy ineficiente!

b) ¿Cuántos paquetes en vuelo necesita un protocolo de tubería para lograr U ≥ 90%?
>[!question]- Respuesta:
>U = N × Denvío / (RTT + Denvío). Queremos 0,9 ≤ N × 0,1 / 50,1 → N ≥ 50,1 × 0,9 / 0,1 = 450,9
➤ Se necesitan al menos N = 451 paquetes en vuelo para alcanzar 90% de utilización.

c) ¿Cuál sería el throughput efectivo con Parada y Espera?
>[!question]- Respuesta:
>Throughput = U × R = 0,002 × 100 Mbps = 200 kbps (¡solo 0,2% del enlace de 100 Mbps!)

### ejercicio 3
Datos: Enlace de 1 Gbps, propagación 15 ms, paquetes de 8.000 bits. ACK despreciable.
RTT = 2 × 15 ms = 30 ms.
a) Calcule U y throughput para Parada y Espera.
>[!info]- Respuesta
>Denvío = L/R = 8.000 / 109 = 0,008 ms
➤ U = 0,008 / (30 + 0,008) = 0,00027 = 0,027% | Throughput = 0,00027 × 1 Gbps = 270 kbps

b) Si se envían 3 paquetes en tubería (como en slide 22), ¿cuánto mejora?
>[!info]- Respuesta:
>U = N × Denvío / (RTT + Denvío) = 3 × 0,008 / 30,008 = 0,0008 = 0,08%
➤ Mejora: ×3 respecto a P&E. Throughput = 0,0008 × 1 Gbps = 800 kbps. Aún muy bajo.

c) ¿Cuántos paquetes en vuelo se necesitan para U = 100%?
>[!info]- Respuesta
> 1 = N × 0,008 / 30,008 → N = 30,008 / 0,008 = 3.751 paquetes
➤ Conclusión: Con alta velocidad y alta latencia, se necesita una ventana enorme para llenar el
enlace. Esto exige muchos bits para N° de secuencia.

### Ejercicio 4
Datos: Enlace de 10 Mbps, propagación 10 ms, paquetes de 5.000 bits. ACK despreciable.
Se usa Retroceso-N.
a) ¿Cuál es la utilización con Parada y Espera?
>[!info]- Respuesta:
> Denvío = 5.000 / 10×106 = 0,5 ms. RTT = 20 ms. U = 0,5 / 20,5 = 0,0244 = 2,44%

b) ¿Cuántos paquetes en vuelo necesita GBN para U ≥ 80%?
>[!info]- Respuesta:
> 0,8 ≤ N × 0,5 / 20,5 → N ≥ 20,5 × 0,8 / 0,5 = 32,8 → N = 33 paquetes

c) ¿Cuántos bits de N° de secuencia necesita GBN para esa ventana?
>[!info]- Respuesta:
> GBN necesita MAX_SEQ ≥ 33, o sea MAX_SEQ + 1 ≥ 34 secuencias. Se requiere 2^k ≥ 34 → k = 6 bits (2^6 = 64 secuencias, ventana máx = 63).

d) ¿Y si se usara Repetición Selectiva con los mismos 6 bits?
>[!info]- Respuesta
> Ventana máx SR = (2^6)/2 = 32 paquetes. U = 32 × 0,5 / 20,5 = 0,78 = 78%. No alcanza el 80%: SR
necesitaría 7 bits (ventana máx = 64).

### Ejercicio 5
Dato: Un protocolo usa N° de secuencia de 3 bits (secuencias 0 a 7, MAX_SEQ = 7).
a) ¿Cuál es el tamaño máximo de la ventana emisora en Retroceso-N?
>[!info]- Respuesta:
> Ventana máx. = MAX_SEQ = 7. No puede ser 8 (= MAX_SEQ + 1) porque el receptor no podría distinguir un paquete nuevo del paquete 0 retransmitido.

b) ¿Cuál es el tamaño máximo de la ventana receptora en Repetición Selectiva?
>[!info]- Respuesta:
> Ventana máx. = (MAX_SEQ + 1) / 2 = (7 + 1) / 2 = 4. La mitad del espacio de secuencia
garantiza que las ventanas de emisor y receptor nunca se solapen.

c) Si se usaran 4 bits para N° de secuencia (0 a 15), ¿Cuántos paquetes en vuelo
permitiría GBN?
>[!info]- Respuesta:
> MAX_SEQ = 2^4 – 1 = 15. Ventana máx. GBN = 15 paquetes. Y para SR: ventana máx. = (15+1)/2 = 8 paquetes.
### Ejercicio 6 
P1. Escenario: Un emisor usa GBN con ventana = 4 y envía paquetes 0, 1, 2, 3. El paquete 1
se pierde. ¿Qué paquetes retransmite el emisor al expirar el temporizador?
>[!info]- Respuesta:
>El receptor acepta pkt 0 (envía ACK 0), pero descarta pkts 2 y 3 (fuera de orden). El emisor
retransmite 1, 2, 3 (toda la ventana desde el paquete perdido).

P2. Mismo escenario con Repetición Selectiva. ¿Qué cambia?
>[!info]- Respuesta:
>El receptor almacena pkts 2 y 3 en su buffer y envía ACK individual para cada uno. Solo
retransmite el paquete 1. Al recibirlo, el receptor entrega 1, 2, 3 en orden a la capa superior.
Ahorro: 2 retransmisiones menos.

P3. ¿Qué es piggybacking y cuándo resulta útil?
>[!info]- Respuesta:
> Piggybacking = incluir el ACK dentro de un paquete de datos que viaja en sentido contrario. Es
útil en comunicación bidireccional porque ahorra un paquete completo. Si no hay datos para
enviar rápidamente, se usa un temporizador auxiliar corto para enviar el ACK solo y evitar que
expire el temporizador del e
## Control de flujo
#### Ejercicio 1
Durante una conexión TCP, el emisor recibe un ACK con WIN = 0.
Responde:
(a) ¿Qué significa para el emisor?
(b) ¿Qué podría ocurrir si se quedase a la espera
de un nuevo anuncio de ventana?
(c) ¿Cómo resuelve TCP esa situación?

##### Solución:
(a) El búfer de recepción está lleno. El emisor debe detener el envío de datos nuevos.
(b) El ACK que libera el búfer podría perderse. El emisor quedaría bloqueado indefinidamente (interbloqueo).
(c) El emisor arranca un temporizador de persistencia y envía periódicamente segmentos de sondeo (1 byte) que fuerzan al receptor a contestar con el WIN actualizado. Así se garantiza que el emisor se entere en cuanto el receptor libere espacio, aun si los ACK se pierden.

#### Ejercicio 2
El receptor tiene un RcvBuffer = 16 KB.
• Ha recibido 12 KB de datos.
• La aplicación ha leído 5 KB.
• El emisor ya tiene 2 KB en vuelo no confirmados.
Calcula:
• (a) el valor de rwnd que anuncia el receptor
• (b) los bytes adicionales que el emisor puede enviar

##### Solución:
Fórmula: rwnd = RcvBuffer − (datos recibidos − datos leídos)
Paso 1 — datos en búfer: 12 KB − 5 KB = 7 KB ocupando búfer
Paso 2 — (a) rwnd anunciada: 16 − 7 = rwnd = 9 KB
Paso 3 — (b) nuevos bytes enviables: rwnd − bytes en vuelo 9 − 2 = 7 KB

#### Ejercicio 3
Traza temporal, ¿Qué WIN se anuncia tras cada evento?
Receptor con RcvBuffer = 10 KB. Estado inicial: búfer vacío, aplicación no ha leído nada. Completa WIN anunciado en cada evento.
![[Pasted image 20260427133152.png]]

##### Solución: 
esta es : ![[Pasted image 20260427133208.png]]

## Control de Congestión (CT)
![[Pasted image 20260502183207.png]]
![[Pasted image 20260502183218.png]]
![[Pasted image 20260502183233.png]]
![[Pasted image 20260502183320.png]]
![[Pasted image 20260502183343.png]]
![[Pasted image 20260502183512.png]]
