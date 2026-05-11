Una arquitectura por sí sola, no alcanza para que los nodos puedan colaborar: saber quién hace qué no explica cómo se comunican ni qué reglas siguen para coordinarse. Para que una aplicación distribuida funcione, los nodos necesitan un lenguaje común, un conjunto de mensajes y normas que les permita interactuar de manera coherente. 

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

Ejemplos típicos de estado:
- Quién es el otro extremo (identidad, autenticación)
- En qué parte del diálogo estamos (fase del protocolo)
- Qué recursos estamos usando (p. ej: directorio actual, archivo abierto, etc)
- Qué se envió o recibió antes (para interpretar lo que viene después)
- Configuraciones activas: son decisiones o parámetros que la aplicación negocia o establece durante la interacción

### Ejemplo: protocolo de transferencia de archivos
El protocolo puede tener mensajes de comandos, de feedback (de respuesta a comandos), y mensajes con información (directorios, archivo)
![[Pasted image 20260331102408.png]]
Este protocolo puede manejar la siguiente información de estado: directorio corriente, y autenticación previa.
