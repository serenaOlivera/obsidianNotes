Un protocolo es una idea abstracta: describe la lógica de interacción, no la forma concreta de implementarla. Para que un protocolo cobre vida, necesitamos herramientas que permitan enviar y recibir datos, gestionar conexiones y materializar la comunicación entre nodos. Es aquí donde entran en juego las tecnologías de implementación, que determinan el nivel de control, la complejidad y las capacidades reales de una aplicación distribuida. 

## Sockets
Un socket es un punto de conexión que permite a una aplicación enviar y recibir datos por la red sin conocer los detalles internos de TCP o UDP, usando una interfaz uniforme en cualquier sistema operativo.

Un socket no es un protocolo: es una abstracción para acceder a protocolos de transporte. Los sockets se usan para invocar a TCP o UDP a través del sistema operativo.

Los sockets:
- **Unifican:** la misma interfaz de programación de aplicaciones para TCP y UDP.
- **Simplifican:** esconden la complejidad del transporte.
- **Estandarizan:** permiten que programas escritos en distintos lenguajes se comuniquen igual.
- **Aíslan:** la aplicación se enfoca en su lógica, no en la mecaánica de la red
### Socket API:
Conjunto básico de funciones que permiten a dos programas comunicarse a través de la red enviando y recibiendo datos directamente sobre protocolos como TCP y UDP. Obliga a manejar algunos detalles de transporte como puertos, direcciones, envío y recepción de datos.

Los sockets existen para que las aplicaciones puedan comunicarse por la red sin tener que implementar la red. Son la frontera entre la lógica de aplicación y los mecanismos de transporte.

![[Pasted image 20260331111250.png]]
![[Pasted image 20260331111349.png]] 
El **servidor TCP:** prepara un punto de encuentro
1. **Crear socket (socket)**: Preparar un punto de comunicación.
2. **Asociar a un puerto (bind):** Elegir en qué puerto va a escuchar.
3. **Escuchar (listen):** Indicar que está listo para aceptar conexiones.
4. **Aceptar conexión (accept):** Cuando llega un cliente, se crea una conexión TCP independiente.
5. **Enviar/recibir datos:** Intercambio confiable y ordenado
6. **Cerrar conexión:** Liberar recursos cuando termina la interacción.

**Cliente TCP:** inicia la comunicación.
1. **Crear socket:** Preparar su punto de comunicación.
2. **Conectar (connect):** iniciar la conexión TCP con la IP y puerto del servidor.
3. **Enviar/recibir datos:** Usar la conexión ya establecida para intercambiar mensajes.
4. **Cerrar conexión:** Indicar que terminó de usar el servicio.


## La Web
A medida que las aplicaciones crecieron en complejidad, surgió la necesidad de contar con un nivel más alto de organización: un conjunto de reglas comunes que permitiera a cualquier cliente comunicarse con cualquier servidor sin tener que reinventar todo desde cero.
Ese salto de abstracción es lo que da origen a la Web, donde protocolos como HTTP definen no solo cómo se envían los datos, sino también qué significan y cómo deben comportarse los participantes. 

La web se apoya en sockets, pero los envuelve en un marco mucho más estructurado, estandarizado y fácil de usar. Pasamos así de construir la comunicación "a mano" a trabajar con un ecosistema que ya trae convenciones, formatos y comportamientos bien definidos.

La Web es una plataforma de aplcacones de red basada en protocolos estandarizados (como HTTP/HTTPS) que permite acceder a información y servicios desde cualquier navegador, sin manejar detalles de bajo nivel como sockets.

**Ventajas de la web:**
- Se trabaja con una abstracción más alta al no tener que gestionar paquetes, puertos, ni protocoloes de capa de transporte.
- Cualquier dispositivo con navegador puede usar la aplicación sin instalar nada.
- La Web permite enfocarse en la lógica de la plicación en lugar de la infraestructura de red 
- Permite interoperabilidad entre lenguajes, sistemas y dispositivos
- Es la base de la mayoría de las aplicaciones modernas.

| Criterio                            | Sockets                                                        | Web                                                              |
| :---------------------------------- | :------------------------------------------------------------- | :--------------------------------------------------------------- |
| Nivel de abstracción                | Bajo: control directo sobre el envío y la recepción de datos   | Alto: el protocolo ya define estructura, significado y reglas    |
| Flexibilidad                        | Muy alta: se puede diseñar cualquier protocolo propio.         | Media: se siguen reglas del protocolo HTTP y sus métodos.        |
| Estructura de los mensajes          | La define el programador desde cero.                           | Ya viene estandarizada (p. ej: con métodos, encabezados, cuerpo) |
| Facilidad de uso&nbsp;              | Requiere más trabajo&nbsp; cuidado con detalles                | Más simple: muchas tareas ya están resueltas.<br><br>            |
| Control sobre la comunicación&nbsp; | Total: tiempos, formato, orden, flujo                          | Parcial: HTTP decide gran parte del comportamiento               |
| Interoperabilidad                   | Limitada: ambos extremos debern implementar el mismo protocolo | Muy alta: cualquier navegador puede comunicarse&nbsp;<br><br>    |
| Costos de desarrollo                | Más altos: hay que diseñar y mantener el protocolo.            | Más bajo: usan estándares y herramientas existentes.             |
| Seguridad                           | Depende de lo que programes                                    | HTTPS resuelve cifrado y autenticación básica                    |


Elegir Sockets cuando:
- necesitas máximo control sobre la comunicación;
- quieres diseñar un protocolo propio; 
- la aplicación requiere baja latencia o comunicación continua (juegos, chat, streaming);
- el formato de los mensajes debe ser muy eficiente.

Elegir Web (HTTP/HTTPS) cuando:
- quieres simplicidad y evitar reinventar protocolos; 
- necesitas interoperabilidad con navegadores, móviles o servicios externos;
- vas a crear un sitio web o una aplicación web;
- buscas herramientas maduras, seguridad integrada y facilidad de pruebas.


[[La Web]]