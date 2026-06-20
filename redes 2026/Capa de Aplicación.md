Las aplicaciones distribuidas necesitan coordinarse, intercambiar información y entenderse entre sí, aún cuando están en máquinas distintas, usan sistemas operativos distintos, están escritas en lenguajes distintos, se ejecutan en redes heterogéneas.
La red por sí sola no resuelve cómo dos aplicaciones acuerdan qué decirse ni cómo interpretarlo.

La capa de aplicación define **cómo las aplicaciones usan la red** para intercambiar información y coordinarse. Es donde se diseña la lógica de interacción entre programas distribuídos. Todo lo demás (transporte, red enlace) existe para que esta capa pueda funcionar.
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


- [[Bloque 1- Arquitecturas de aplicaciones de red]]
- [[Bloque 2- Protocolos de aplicaciones de red]]
- [[Bloque 3- Tecnologías de implementación]]
- [[La Web]]