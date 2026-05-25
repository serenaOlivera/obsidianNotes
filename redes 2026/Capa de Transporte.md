La capa de transporte (CT) provee comunicación lógica entre procesos de aplicación en diferentes hosts. Es decir, los procesos se comunican como si estuvieran directamente conectados. La capa de red (CR) sólo comunica hosts; la CT va más allá: comnica procesos.
**Se implementa sólo en los sistemas finales (no en routers intermedios)**

Mejora los servicios de la capa de red
- Ej: retransmite paquetes perdidos en redes no orientadas a la conexión.
- Ej: regula la tasa de transmisión ante congestión en la red.

¿Dónde se ejecuta la CT?
	Se ejecuta por completo en los hosts/sistemas finales (computadoras de origen y destino). Los routers y switches intermedios no participan: sólo reenvían paquetes sin inspeccionar la capa de transporte
La capa de transporte depende de la capa de red (IP) para mover paquetes entre hosts pero agrega: entrega confiable, control de flujo y multiplexación.

**Entidad de transporte (ET)**: Es el software (o hardware) que implementa la lógica de la capa de transporte en cada host.

## Problemas que resuelve
La CT soluciona problemas clave de la comunicación en red:
- **Confiabilidad:** uso de temporizadores y retransmisiones para recuperar paquetes perdidos.
- **Direccionamiento:** identificar el proceso correcto en el host destino. El proceso destino podría no estar activo, o el cliente pordría no saber cuál usar.
- **Eficiencia:** uso de búferes para una comunicación confiable sin desperdiciar recursos.
- **Control de flujo:** evitar que un emisor rápido sature a un receptor lento
- **Control de congestión:** regular la cantidad de paquetes inyectados a la red: evitar que los búferes de los nodos intermedios se saturen y pierdan (hagan drop de) paquetes. Si la capa de red pierde paquetes por congestión, la CT puede compensarlo.

## Segmentos y encapsulamiento
![[Pasted image 20260406115839.png]]
Segmento = **unidad de datos del protocolo de transporte (TDPU)**
Los segmentos se encapsulan en paquetes (CR) y luego en tramas (capa de enlace). Encapsulamiento = agregar un encabezado de la capa inferior al contenido de la capa superior, como una carta dentro de un sobre dentro de una caja.

Confirmaciones de recepción (ACK): el receptor notifica al emisor que los datos llegaron bien. 
¿Qué se confirma? Tanto paquetes de datos como paquetes de control (ej: establecimiento de conexión)
### Paquete
Un **paquete** es una **unidad de datos** que viaja por la red.
- Pertenece a la **Capa de Red** (por ejemplo, IP).
- Tiene:
    - **Cabecera** (dirección origen/destino, TTL, etc.)
    - **Datos**    
- Es lo que los routers reenvían.
### Segmento

- Pertenece a la **Capa de Transporte** (TCP o UDP).
- Es la unidad de datos que maneja el protocolo de transporte.
- Contiene:
    - Cabecera de transporte (puertos, número de secuencia, etc.)
    - Datos de la aplicación.
En TCP se llama **segmento** En UDP muchas veces se dice **datagrama UDP**

## [[TCP]]

## Direccionamiento
Problema: El direccionamiento explícito de los destinos.
¿Cómo hacer para que un proceso servidor adecuado atienda a las necesidades de una máquina cliente?

Consideraremos los siguientes casos
### Caso 1: El cliente necesita un tipo de servicio, sin embargo no sabe cuál proceso servidor es adecuado para contactar.

Asumir que los procesos servidores están activos
¿Cómo hacer que el cliente se entere de un proceso servidor para un tipo de servicio?
	Solución: Existe un proceso especial llamado **servidor de directorio** que para cada tipo de servicio sabe cuáles son los puertos de los servidores que prestan ese tipo de servicio. Pasos seguidos:
	1. El usuario establece una conexión con el servidor de directorio (que escucha en un puerto bien conocido).
	2. El usuario envía un mensaje especificando el nombre del servicio.
	3. El servidor de directorio le devuelve la dirección puerto.
	4. El usuario libera la conexión con el servidor de directorio y establece una nueva con el servicio deseado

¿Cómo se hace cuando se crea un servicio nuevo?
	El servicio nuevo debe registrarse en el servidor de directorio, dando su nombre de servicio como la dirección de su puerto. El  servidor de directorio registra esta información en su base de datos.

### Caso 2: Servidor inactivo -> Protocolo Inicial de Conexión
Problema: El cliente conoce al proceso servidor adecuado, pero este se encuentra inactivo y no puede responder a solicitudes. El servidor existe en la máquina remota, pero su proceso no está corriendo en ese momento, entoces se necesita un mecanismo para activar al servidor bajo demanda cuando llega una solicitud.

 **Solución:** Usar un **servidor de procesos** (protocolo inicial de conexión), un intermediario que activa servidores inactivos cuando se los necesita.
 - El servidor de procesos escucha en los puertos de servidores de menor uso que están inactivos.
 - Cuando recibe una solicitud, genera (fork) el servidor correspondiente y le transfiere la conexión del cliente.
 Pasos detallados (con cuadro al final):
1.  **Escucha múltiple:** El servidor de procesos escucha en un grupo de puertos simultáneamente, esperando solicitudes de conexión entrantes de clientes.
2. **Solicitud CONNECT:** Un cliente emite una solicitud CONNECT,  especificando el número de puerto del servicio que desea utilizar.
3. **Redirección:** Si no hay ningún servidor activo esperando en ese puerto, la solicitud llega al servidor de procesos, quien obtiene la conexión.
4. **Generación (fork):** El servidor de procesos genera (fork) el servidor solicitado y le permite heredar la conexión existente con el cliente, de modo que la comunicación continúa sin interrupción
5. **Servicio activo:** El nuevo servidor recientemente activado realiza el trabajo solicitado por el cliente. Mientras tanto, el servidor de procesos vuelve a escuchar en los puertos, listo para atender nuevas solicitudes entrantes.
![[Pasted image 20260406164053.png]]
[[Ejercicios (CT)]]


### Puertos bien conocidos 
Sonlos puertos con números menores a 1024, reservados para servicios estándar del sistema. Esots números están asignados por la IANA (internet assigned numbers Auth)

**Demonios (daemons):** Son procesos servidores que se ejecutan en segundo plano y se asocian a un puerto específico en el momento del arranque del sistema.  Ejemplo: El demonio FTP se conecta al puerto 21 durante el arranque y queda escuchando solicitudes de transferencia de archivo.

Problema: Si cada servicio tiene su propio demonio ejecutándose permanentemente, se podría llenar la memoria con demonios que están inactivos la mayor parte del tiempo, desperdiciando recursos del sistema.
*Solución:* Un único demonio llamado inetd (Internet daemon) reemplaza a múltiples demonios individuales. Este proceso:
- Escucha simultáneamente en un conjunto de puertos y espera solicitudes de conexión entrantes. 
- Cuando un cliente emite un pedido CONNECT a un puerto específico, inetd verifica si ya hay un servidor escuchando en ese puerto.
- Si no hay servidor activo, inetd bifurca (fork) un nuevo proceso, ejecuta el demonio apropiado en él, y ese demonio maneja la solicitud del cliente.
#### Archivo de configuración de inetd
- inetd determina qué puertos debe supervisar a partir de un archivo de configuración (generalmente /etc/inetd.conf). Este archivo lista los servicios disponibles, sus puertos y los programas a ejecutar.
- Los demonios asociados a estos puertos solo se activan cuando hay trabajo, ahorrando memoria y recursos del sistema.
- Estrategia híbrida: Demonios permanentes + inetd.
  En la práctica se usa una estrategia combinada: Demonios permanentes en los puertos más utilizados (ej: HTTP puerto 80, SSH puerto 22), porque el costode tenerlos siempre activos se justifica por su alta demanda. Inetd gestiona los demás servicios de menor uso, activándolos bajo demanda para ahorrar recursos. Esta decisión la toma el administrador del sistema, según el perfil de uso de cada servidor.
### Servidores de directorios y servicios en la práctica
**Servidor de Directorio — Ejemplos reales:**
- DNS (Domain Name System): Traduce nombres de dominio a direcciones IP. Es el directorio distribuido más utilizado a escala global. [Capa de Aplicación]
- LDAP: Usado en redes corporativas para localizar servicios y recursos. [Capa de Aplicación]
**Servidor de Procesos (activación bajo demanda) — Ejemplos reales:**
- inetd / xinetd: Implementación clásica en Unix/Linux. [Capa de Transporte – escucha en puertos TCP/UDP]
- systemd socket activation: Reemplazo moderno de inetd en Linux. [Capa de Transporte – sockets TCP/UDP]
- AWS Lambda / Serverless: Los procesos se generan bajo demanda. [Capa de Aplicación]
**Combinación de ambos** 
- En Kubernetes, kube-dns (descubrimiento) + auto-scaling (activación). [Capa de Aplicación]

[[Ejercicios (CT)]]

## Entrega confiable

La CR puede perder paquetes (drop por bufer lleno o en la capa de enlace, perdidos por errores del canal), duplicarlos o entregarlos fuera de orden. La CT debe (o puede) solucionar esto y es responsable de garantizar (o no) entrega efectiva de los segmentos al host destino, y entrega ordenada: que los datos lleguen en el mismo orden en que fueron enviados por la capa de aplicación.

Esto se logra mediante mecanismos como números de secuencia, ACKs y temporizadores 
(fijarse como copiar esto con lo de abajo)
1. El emisor asigna números de secuencia a cada segmento, respetando el orden del flujod e datos.
2. Al enviar un segmento, dispara un temporizador de retransmisión.
3. EL receptor envía confirmaciones de recepción (ACK) por cada segmento recibido correctamente.
4. Si el temporizador expira sin recibir ACK, el emisor retransmite el segmento.
5. El receptor reensambla en orden los segmentos recibidos y los entrega a la capa de aplicación 


La capa de transporte dispone de tres mecanismos fundamentales:
1. ACK (confirmación de recepción):
	   - El receptor envía un paquete ACK para confirmar que recibió los datos correctamente.
	   - Si el emisor recibe el ACK, entonces sabe que el paquete llegó bien.
2. Temporizadores (timers):
	   ¿Cómo saber si un paquete se perdió? Si pasa cierto tiempo sin recibir ACK. EL temporizador mide ese tiempo de espera máximo (timeout)
3. Retransmisiones:
	   Si el temporizador expira sin ACK, entonces el emisor retransmite el paquete.   

Sin embargo, los mecanismos básicos (ACK, temporizadores, retransmisiones) no son suficientes por sí solos. Se necesita un protocolo de entrega confiable que defina reglas precisas para el emisor y receptor. 

¿Porqué hay varios protocolos? Porque el protocolo óptimo depende de las características de la red:
	- Latencia: cuánto tarda un paquete en llegar 
	- Tasa de errores: qué tan frecuente es la pérdida/corrupción
	- Capacidad: tasa de datos que puede manejar la red.

La capa de transporte debe incluir al menos un protocolo de entrega confiable.  La capa de enlace incluye protocolos de entrega confiable enfocados en un solo salto, mientras que los de la capa de transporte lo hacen extremo a extremo (recordar que transporte esta sólo en los sistemas finales )

### Números de secuencia
Cada paquete lleva un número de secuencia único. Cuando llega un paquete, el receptor revisa si ya recibió ese número. Si es duplicado, lo descarta. Si es nuevo, lo entrega a la aplicación.

[[Protocolo de Parada y Espera (CT)]]

Si usamos parada y espera con alta latencia, el emisor pasa la mayor parte del tiempo ocioso esperando el ACK, osea hay una utilización muy baja del enlace.

[[Protocolo de Tubería (CT)]]

# **Hasta acá entró el primer parcial de CT (fijarse en CR tmb)**

## [[Control de flujo (CT)]]
## [[Control de Congestión (CT)]]
## Duplicados Retrasados
No se pueden entregar segmentos duplicados a la capa de aplicación. Como consecuencia, el receptor debe poder decidir para cada segmento que llega, si es duplicado o no.

La manera de detectar duplicados eficientemente es a través de **números de secuencia**:
- Numerar cada segmento con un n° de secuencia.
- Dos segmentos con n° distinto, son distintos 
Esto funcionaría perfecto si los números fueran de tamaño arbitrario, pero el espacio de secuencia es finito.
¿Porqué?
	Los segmentos tienen longitud máxima, el n° de secuencia debe entrar en el campo del encabezado. Este campo tiene longitud fija, sólo hay un número finito de valores posibles.
	Como consecuencia, los números se reutilizan. Numerar los segmentos sólo con eso ya no alcanza.

### Dos escenarios donde aparecen problemas

#### Escenario A - Dentro de una conexión
El espacio de secuencia se cicla,
- Los n° van 0> 1-> 2-> 3, vuelven a 0 y suben hasta 3 de nuevo 
- Un segmento con n°3 queda demorado y llega cuando ya pasó el segundo 3.
- Resultado: El receptor lo acepta como nuevo: el espacio de secuencia se reutilizó y el duplicado vivió demasiado en la red
![[Pasted image 20260503134644.png]]
#### Escenario B - Entre conexiones
En el ejemplo:
- Espacio de secuencia de 2 bits (0-3)
- Antes de la segunda conexión se libera la primera
- La 2da conexión llega rápido al n° 2
- Un duplicado retrasado de la primera conexión con n° 2 aún vive en la red
- Es aceptado por error en la 2da conexión
- ![[Pasted image 20260503134337.png]]

### La idea unificadora: limitar el tiempo de vida 
Asegurar que ningún paquete viva más de T segundos en la red. Aplica a : paquetes de datos, retransmisiones, confirmaciones de recepción (acks). Eliminar paquetes viejos que sigan circulando hace que ambos escenarios sean manejables .
#### Solución para el escenario A 
El origen no debe reutilizar un n° de secuencia dentro de T segundos (tiempo de vida del paquete). 

Funciona porque, cuando se llega a un n° ya usado, ese segmento viejo ya murió hace tiempo en la red. El espacio de secuencia debe ser lo bastante grande para que no se cicle dentro de T segundos.

**Ejercicio**: Una conexión usa segmentos de 1500 B, transmite a 10 Mbps y el tiempo de vida máximo de segmento es T = 30s ¿De cuántos bits debe ser el n° de secuencia?

**Solución**: Hay que contar cuántos segmentos como máximo se pueden transmitir en T segundos.
- Bits transmitidos en T: $10^7 \ bits/s \ * 30s = 3* 10^8 bits$
- Bits por segmento: $1500*8 \ = 12000\ bits$
- Segmentos máximos en T: $3 * 10^8 / 1,2 *10^4 = 25000\ segmentos$
-  Bits necesarios: $log_2(25000) \approx 14,6$ (esto se usa para saber cuantos bits son necesarios para direccionar esos 25000 segmentos)
Respuesta: 15 bits

#### Solución para el escenario B
Si la nueva conexión empieza en 0, puede chocar con duplicados de la conexión anterior.
Entonces, cada conexión elige un n° inicial de secuencia distinto para no entrar en el rango de los duplicados de conexiones anteriores.

**Implementación 1: n° incial aleatorio**
	Al crear una nueva conexión, cada extremo elige un n° aleatorio de 32 bits. Ese n° pasa a ser el n° inicial de secuencia para los datos.
	 Esto tiende a funcionar porque la probabilidad de que un duplicado retrasado caiga en el rango de la nueva conexión es baja gracias a la elección aleatoria.

**Implementación 2: n° incial atado al reloj**
	Cada host tiene un contador binario que se incrementa en intervalos uniformes. El n° inicial de cada nueva conexión se toma del valor actual del reloj. Los relojes de los hosts no necesitan estar sincronizados. 
	Esto funciona porque el reloj avanza monotónicamente: el n° inicial es siempre posterior al usado por la conexión previa, fuera del rango de sus duplicados. 

Ejemplo (con esquema basado en reloj)
- Pulso de reloj cada $4\  \mu s$
- Tiempo de vida máximo de paquete $T=\ 120 s$
- N° de secuencia: $32 \ bits$
- El reloj corre lo bastante rápido como para que cada nueva conexión abra en un valor distinto, y lo bastante lento como para no agotar los 32 bits dentro de T segundos.