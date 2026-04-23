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
**Respuesta:** b) El segmento es la unidad de datos de la capa de  transporte. Se encapsula dentro de un paquete IP (capa de red).

#### Ejercicio 4 — Completar (cálculo)
El campo «longitud del encabezado» tiene 4 bits. ¿Cuál es el número máximo de palabras de 32 bits que puede tener el encabezado TCP? 
**Respuesta:** 15. Con 4 bits el valor máximo es 2⁴ - 1 = 15. Eso equivale a 15 × 4 = 60 bytes

#### Ejercicio 5 — Completar (cálculo)
Si el encabezado fijo de TCP mide 20 bytes y el máximo es 60 bytes, ¿cuántos bytes pueden ocupar las opciones como máximo? 
**Respuesta:** 40 bytes. 60 bytes (máximo total) - 20 bytes (encabezado fijo) = 40 bytes para opciones.

#### Ejercicio 6 — Verdadero o Falso
«Un socket se identifica únicamente con el número de puerto.»
**Respuesta:** FALSO. Un socket = dirección IP + puerto. Dos hosts distintos pueden usar el mismo puerto (ej.: ambos en puerto 80), pero sus sockets son diferentes porque tienen distinta IP.

#### Ejercicio 7 — Completar (cálculo)
Un host recibió correctamente todos los bytes de un flujo TCP hasta el byte 4999 ¿Qué valor tendrá el campo ACK number en su próximo segmento? 
**Respuesta:** 5000. El ACK number indica el siguiente byte esperado. Si recibió hasta el 4999,espera el 5000.

#### Ejercicio 8 — Verdadero o Falso
«Si el flag ACK vale 0, el campo número de confirmación contiene un valor
válido.»
**Respuesta:** FALSO. Cuando ACK = 0, el campo se ignora. Solo es válido cuando ACK = 1.

#### Ejercicio 9 — Completar (cálculo)
Un enlace tiene MTU de 1500 bytes. IP ocupa 20 bytes y TCP ocupa 20 bytes. ¿Cuál es el MSS? 
**Respuesta:** 1460 bytes. MSS = MTU - IP - TCP = 1500 - 20 - 20 = 1460 bytes.

#### Ejercicio 10 — Multiple Choice
¿Qué flag del encabezado TCP se utiliza para iniciar una conexión?
a) FIN b) RST c) SYN d) PSH
**Respuesta:** c) SYN. SYN (synchronize) se usa para solicitar el establecimiento de una conexión TCP.

#### Ejercicio 11 — Multiple Choice
¿Para qué sirve la opción MSS en el encabezado TCP?
a) Indicar el tamaño de la ventana de congestión
b) Negociar el tamaño máximo de segmento que acepta cada lado
c) Definir el número de secuencia inicial
d) Establecer el tiempo de vida del paquete
**Respuesta:** b) MSS (Maximum Segment Size) se negocia al inicio de la conexión para que cada lado informe el tamaño máximo de datos que puede recibir por segmento.

#### Ejercicio 12 — Verdadero o Falso
«Una conexión TCP se identifica de forma única por un solo socket (IP + puerto).»
**Respuesta:** FALSO. Una conexión TCP se identifica por el par (socket_origen, socket_destino), es decir, dos sockets: uno en cada extremo.

## Direccionamiento
#### Pregunta 1: ¿Cuál es la diferencia fundamental entre la solución del servidor de procesos y la solución del servidor de directorio?
**Respuesta:** El servidor de directorio resuelve el problema de descubrimiento: el cliente no sabe en qué puerto escucha el servicio, y el directorio le indica la dirección. Asume que el servidor ya está activo. El servidor de procesos resuelve el problema de activación: el cliente conoce el puerto, pero el servidor está inactivo, y el servidor de procesos lo genera (fork) bajo demanda y le transfiere la conexión. 

#### Pregunta 2: ¿En qué escenario haría falta combinar ambas soluciones?
**Respuesta:** Cuando el cliente no conoce el puerto del servicio y además el servidor está inactivo. Primero se consulta al servidor de directorio para descubrir el puerto, y luego el servidor de procesos se encarga de activar el demonio correspondiente para atender la solicitud. Se combinan ambos mecanismos en secuencia: descubrimiento + activación

#### Ejercicio 1: Análisis de Escenarios
• Para cada situación, indicar qué mecanismo se necesita: servidor de directorio, servidor de
procesos, ambos o ninguno. Justificar.
a) Un navegador web quiere conectarse al servidor HTTP de una máquina remota. Sabe que HTTP usa el
puerto 80, y el servidor está activo permanentemente como demonio.
**Ninguno. El cliente ya conoce el puerto (80 es well-known) y el servidor está activo como demonio permanente. No se necesita descubrimiento ni activación**

b) Una aplicación necesita un servicio de impresión remota. Sabe que el servicio existe en la máquina
destino pero desconoce en qué puerto escucha.
**Servidor de directorio. El problema es de descubrimiento: el cliente no sabe el puerto. Consulta al directorio, que le devuelve la dirección del servicio de impresión. El servicio se asume activo.**

c) Un cliente quiere usar el servicio finger (puerto 79) en un servidor Unix. El servicio está configurado en
/etc/inetd.conf pero no hay ningún demonio finger corriendo actualmente.
**Servidor de procesos (inetd). El problema es de activación: el cliente conoce el puerto 79, pero el demonio está inactivo. inetd escucha en ese puerto, recibe la solicitud, genera (fork) el proceso finger y le transfiere la**
**conexión**

d) Un proceso cliente necesita un servicio personalizado que fue recién instalado en el servidor. No conoce
su puerto, y el servicio solo se activa bajo demanda mediante inetd.
**Ambos. Hay dos problemas simultáneos: no conoce el puerto (→ directorio) y el servicio se activa bajo demanda (→ servidor de procesos/inetd). Primero consulta al directorio para descubrir el puerto, luego inetd activa el servicio al recibir la conexión**

e) Un administrador tiene un servidor con 50 servicios distintos pero solo 5 se usan frecuentemente. ¿Qué estrategia de  direccionamiento/activación debería implementar para optimizar el uso de memoria?
**Estrategia híbrida. Los 5 servicios frecuentes se configuran como demonios permanentes (evitar la latencia de fork). Los 45 restantes se gestionan con inetd para ahorrar memoria, activándolos solo bajo demanda.**


#### Ejercicio 2: Verdadero o Falso
• Indicar si cada afirmación es verdadera o falsa. Si es falsa, corregirla.
1. El servidor de directorio y el servidor de procesos resuelven el mismo problema de direccionamiento.
   FALSA. Resuelven problemas diferentes: el directorio resuelve el descubrimiento del puerto; el servidor de procesos resuelve la activación del proceso servidor inactivo
2. Los puertos bien conocidos (well-known ports) son aquellos con números menores a 1024, reservados para servicios estándar.
   VERDADERA. Los puertos 0-1023 están reservados por IANA para servicios estándar (ej: HTTP=80, FTP=21, SSH=22).
3. El demonio inetd necesita tener todos los servidores cargados en memoria permanentemente para poder redirigir las solicitudes.
   FALSA. Justamente lo contrario: inetd evita tener los servidores en memoria. Solo inetd está activo, escuchando en múltiples puertos, y genera (fork) cada servidor bajo demanda cuando llega una solicitud.
4. En el protocolo inicial de conexión, el servidor de procesos genera (fork) el servidor solicitado y le permite heredar la conexión existente con el cliente.
   VERDADERA. El servidor de procesos hace fork, creando un proceso hijo que hereda los descriptores de archivo (incluida la conexión TCP con el cliente), y el padre vuelve a escuchar.
5. Para registrar un nuevo servicio en un servidor de directorio, basta con que el cliente envíe una solicitud de conexión al puerto deseado.
   FALSA. El registro lo hace el servidor (no el cliente): el nuevo servicio debe enviar su identificador y puerto al servidor de directorio para que este lo incluya en su tabla de búsqueda.
6. En la práctica, todos los servicios de un servidor Unix deberían ser gestionados por inetd para minimizar el consumo de memoria.
   FALSA. La estrategia óptima es híbrida: los servicios de alto tráfico (HTTP, SSH) deben ser demonios permanentes para evitar la latencia de fork; solo los servicios esporádicos se gestionan con inetd.
7. El servidor de directorio necesita escuchar en un puerto bien conocido para que los clientes puedan contactarlo sin necesitar otro directorio.
   VERDADERA. Si el propio directorio no tuviera un puerto conocido, se crearía un problema de recursividad infinita (¿quién me dice dónde está el directorio?). Por eso el directorio siempre usa un puerto well-known.

#### Ejercicio 3: Diseño de Solución
• Situación: Una universidad tiene un servidor central con 30 servicios disponibles para los alumnos (correo, FTP, SSH, bases de datos, impresoras, consulta de notas, etc.). Solo 4 servicios se usan
constantemente (correo, SSH, DNS, HTTP). Los demás se usan esporadicámente.

• Se pide diseñar la estrategia de direccionamiento y activación del servidor, respondiendo:
a) Clasificar: ¿Cuáles servicios configuraría como demonios permanentes y cuáles gestionaría mediante inetd? Justificar el criterio utilizado.

Clasificar: Demonios permanentes: Correo, SSH, DNS y HTTP (alto tráfico → evitar latencia de fork en cada solicitud). Gestionados por inetd: Los 26 restantes (FTP, bases de datos, impresoras, consulta de notas, etc.) → uso esporádico, no justifica ocupar memoria permanentemente. Criterio: frecuencia de uso y tiempo de respuesta aceptable

b) Directorio: Un alumno quiere usar el servicio de “consulta de notas” pero no conoce su puerto. ¿Qué pasos seguiría el sistema para resolver esta solicitud?

Directorio: 
1) El cliente del alumno contacta al servidor de directorio (puerto well-known). 
2) Envía un lookup con el identificador “consulta de notas”.
3) El directorio busca en su tabla y responde con el puerto asignado. 
4) El cliente se conecta a ese puerto. 
5) Como está gestionado por inetd, este recibe la conexión, hace fork del proceso y le transfiere la conexión.

c) Nuevo servicio: Si se agrega un servicio de “reserva de aulas”, ¿qué pasos debe realizar el administrador para que los clientes puedan descubrirlo y utilizarlo?

Nuevo servicio: El administrador debe: 
1) Asignar un puerto al servicio “reserva de aulas”.
2) Agregar una entrada en /etc/inetd.conf con el puerto, protocolo y ruta del ejecutable.
3) Registrar el servicio en el servidor de directorio (enviar identificador + puerto).
4) Reiniciar inetd para que lea la nueva configuración. Los clientes podrán descubrirlo vía directorio y será activado bajo demanda por inetd.

d) Diagrama: Dibujar el flujo completo de mensajes entre el cliente, el servidor de directorio e inetd cuando un
alumno accede al servicio de “consulta de notas” por primera vez.

Cliente → Srv. Directorio: “¿puerto de consulta de notas?” → Directorio responde: “puerto N” → Cliente se
conecta a puerto N → inetd (escuchando en N) acepta conexión → inetd hace fork del proceso “consulta_notas” → Hijo
hereda conexión y atiende al cliente → inetd vuelve a escuchar