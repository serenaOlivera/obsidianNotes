La capa de aplicación define **cómo las aplicaciones usan la red** para intercambiar información y coordinarse. Es donde se diseña la lógica de interacción entre programas distribuidos.Todo lo demás (transporte, red enlace) existe para que esta capa pueda funcionar.
El propósito es entender cómo se construyen las aplicaciones distribuídas y porqué se diseñan así.

La capa de aplicación responde a tres preguntas clave:
1. ¿Quién habla con quién?
	   Para esto se definen arquitecturas de red: Cliente-servidor, P2P, Híbridas. Tienen implicancias en escabilidad, desempeño y robustez.
2. ¿Qué mensajes se intercambian y qué significan?
	   Para esto se definen protocolos de aplicación. Partes constitutivas: tipos de mensajes, sintaxis, semántica, reglas y estado. Derivaremos un ejemplo de diseño de un protocolo de transferencia de archivos (inspirado en FTP)
3. ¿Cómo se implementa esa comunicación?
	   Para esto se usarán tecnologías de implementación:
	    - sockets(bajo nivel)
	    - Web (alto nivel) como plataforma de aplicaciones
	    - Abstracciones y compromisos

# Bloque 1: Arquitecturas de las aplicaciones de red

¿Qué es una arquitectura para aplicaciones de red?
	Tipos de nodos. Cada tipo de nodo tiene responsabilidades o se ocupa de ciertas tareas. La comunicación entre nodos de dos tipos sigue un conjunto de reglas.
	La importancia de usar una arquitectura para aplicaciones de red es que sirve de guía para diseñar una aplicación de red.

## Arquitecturas cliente-servidor

![[Pasted image 20260326152205.png]]
- Tenemos nodo cliente y nodo servidor
- El servidor es la componente dominante que controla el estado, coordina los clientes, almacena datos y es el único punto de acceso.
- El cliente hace pedidos de diferentes tipos y el servidor los procesa y responde.
- Características: control fuerte, simplicidad, pero poca escabilidad sin infraestructura adicional.

## Arquitecturas Peer 2 Peer
los nodos dejan de ser meros consumidores y pasan a ser participantes activos en la red. 

Nodos:
- Hosts llamados peers ( compañeros)
- Puede haber dos estilos de P2P
	- ningún apoyo en servidores : P2P puro.
	- Mínimo apoyo en servidores: predominantemente P2P

**Responsabilidades:**
- Peers:
  - Piden servicios de otros peers
  - Proveen servicios en retorno a pedidos de otros compañeros
- Servidor mínimo:
  - Mantiene la lista de nodos activos semipermanentes
  - Entrega algunos compañeros iniciales a un compañero que recién entra.
  - Autenticación básica.

| Criterio&nbsp;            | Cliente- servidor                                                  | Predominante P2P                                                | Híbrida                                                                                                |
| :------------------------ | :----------------------------------------------------------------- | :-------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------- |
| Escalabilidad             | Limitada por capacidad del servidor.&nbsp;                         | Muy alta: la carga se reparte entre los nodos.&nbsp;            | Alta: los servidores ayudan, pero los pares trabajan.                                                  |
| Robustez                  | Baja: si el servidor falla, el servicio se cae.                    | Alta: la red funciona cuando algunos nodos se desconectan.      | Media-Alta: los servidores ayudan a estabilizar, pero no son únicos puntos de falla.                   |
| Control                   | Centralizado: el servidor decide y organiza todo.&nbsp;            | Distribuido: cada nodo participa sin jefe central.              | Mixto: algunas cosas se controlan desde servidores, otras desde los pares.                             |
| Costos de infraestructura | Altos: el servidor debe ser potente y estar siempre disponible.    | Bajo: la mayor parte lo hacen&nbsp; los nodos.                  | Medios: se necesitan servidores más capaces que en P2P, pero no tan críticos como en cliente-servidor. |
| Rendimiento bajo carga    | Puede degradarse si muchos clientes acceden al mismo tiempo.&nbsp; | Mejora con más nodos: cuantos más participantes, más capacidad. | Suele ser estable: los servidores ordenan y los pares distribuyen la carga.                            |

## Bloque 2: protocolos de aplicacion
Un **protocolo** es el lenguaje de la aplicación distribuida: sin él, no hay coordinación posible. 
El propósito, es comprender cómo dos aplicaciones acuerdan qué mensajes intercambiar, cómo interpretarlos y cuándo enviarlos, para lograr una interacción coherente y predecible.

### ¿Qué cosas definir en un protocolo de aplicación de red?
- Tipos de mensajes
- Sintaxis del mensaje
- Semántica del mensaje 
- Reglas
- Estado de la aplicación 


El **estado** es la información relevante sobre la interacción en curso que la aplicación mantiene entre mensajes, es la memoria que permite que una aplicación distribuída tenga continuidad, coherencia y sentido a lo largo de una interacción.
El estado es necesario, porque sin estado cada mensaje sería ambiguo, no habría forma de interpretar acciones en contexto, no se podrían mantener sesiones, transferencias ni operaciones compuestas y la aplicación no podría coordinarse con otras.