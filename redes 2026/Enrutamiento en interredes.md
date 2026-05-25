## Introducción
Organización del enrutamiento en 2 niveles
	El modelo de dos niveles permite escalar el enrutamiento sin que cada enrutador deba conocer la topología completa de la interred. Los dos niveles de enrutamiento que vemos, son:
		 ❑ Protocolo de puerta de enlace interior (PPEI). Cada red usa su propio protocolo interno. Pueden ser distintos entre sí. }
		 ❑ Protocolo de puerta de enlace exterior (PPEE). Es el protocolo en común para enrutar entre redes. Todas las redes deben usar el mismo PPEE. 
			 
>[!question] ¿Cuántos protocolos distintos PPEI pueden usarse? 
>La interred puede usar diferentes protocolos PPEI en sus redes

Es necesario estudiar protocolos de puerta de enlace exterior (PPEE) porque:
	 o Las tablas de reenvío deben permitir mandar mensajes entre máquinas conectadas a redes diferentes.  El PPEE permite agregar información a ser usada con ese fin a las tablas de reenvío de los enrutadores.
	  o El enrutamiento de PPEE se preocupa de establecer las rutas a usar (que pasan por diferentes WAN) para permitir que se comuniquen máquinas pertenecientes a distintas WAN.

Lo que un protocolo exterior NO puede asumir es que:
	oNo puede ver la topología interna de otras redes.
	oNo puede depender de que todos usen el mismo PPEI.
	oNo puede imponer métricas globales.
	oNo puede forzar a los enrutadores internos a participar. 
 El diseño debe funcionar con mínima información.

>[!info] Limitaciones fundamentales:
>• Encontrar un camino óptimo hacia un destino es imposible en la práctica, Por que  cada red usa su propio protocolo interno y asigna métricas con criterios independientes. No existe una métrica global coherente para comparar caminos que cruzan por varias redes.
>
Uno podría querer resumir cada WAN e inundar la interred con los resúmenes de WANs para después poder armar el grafo de la interred en cada enrutador, sin embargo, esto no es posible, porque:
>- Un proveedor de servicios de red no quiere que la competencia sepa detalles internos de su WAN (p.ej. cuántas puertas de enlace tiene, cómo están interconectadas entre sí) – esto es **ocultación hacia adentro**. 
>- Un proveedor de red puede querer ocultar con qué otras WAN está interconectada – esto es **ocultación de relaciones con otras WAN**.  Por ejemplo, una WAN puede querer ocultar que esta conectada a otra WAN vecina, porque no le resulta rentable económicamente, aunque sea el camino físico más directo. 
>- Un proveedor quiere que las rutas que se usen hacia un destino sea por acuerdos de negocio con otras WAN o por políticas, para proteger los acuerdos comerciales y visibilidad de terceros.

Por lo tanto:
	o **Visibilidad limitada:** Un enrutador en una inter-red sabe que puede llegar a un destino, pero no tiene idea de cómo es el camino por dentro de las otras WAN.  Cada WAN se comporta como una caja negra para las demás.
	 o **Soberanía de WAN**: Una puerta de enlace tiene el derecho político de decidir qué información comparte y qué tráfico permite pasar.
	 
>[!question] Como no se usan resúmenes de WANs para armar un grafo global, ¿De qué otra manera puede controlar una WAN la información que quiere hacer visible? 
>• Anuncio de caminos: Avisando a WANs vecinas caminos a prefijos (LANs ó agregación de ellas).
>• Listas de ruta: se intercambian caminos que indican la lista de WANs por las que debe pasar para llegar a esos destinos.

>[!question] ¿Qué requisitos pedir para un protocolo de puerta de enlace exterior? 
>**o Robustez y alcance:**
>	▪ Visibilidad global de destinos: Transportar avisos sobre destinos que no están en la misma WAN. 
>	 ▪ Escalabilidad: Abstraer la complejidad interna de otras WAN para no saturar las tablas de reenvío. 
>	 ▪ Garantizar rutas libres de bucles: Encontrar caminos hacia prefijos evitando ciclos de enrutamiento en ellas.
>**o Autonomía y negocio:**
>	  ▪ Selección inteligente: capacidad de elegir entre múltiples caminos posibles hacia un destino basándose en la conveniencia. 
>	 ▪ Soberanía de las WAN : Respetar las políticas de cada WAN a lo largo del camino.

 >[!question] ¿Qué sería una política? 
 >Una política son reglas que expresan:
 > • Preferencias de enrutamiento (qué caminos se prefieren).
 >  • Restricciones de enrutamiento (qué caminos están prohibidos).
 
 ¿Qué información ve un enrutador en el nivel PPEE? 
	 o Abstracción de topología : No ve la infraestructura interna de otras WAN. 
	 o Visión parcial y agregada: Solo percibe prefijos, los identificadores de algunas WAN, algunas puertas de enlace (por ejemplo, de contacto directo).
	 
• Implementación: Los PPEE se ejecutan sobre las puertas de enlace (enrutadores mulitprotocolo). 

• Responsabilidades críticas de las puertas de enlace:
	 Para que la interred sea estable y rentable, la puerta de enlace debe:
		  • Seleccionar Rutas: Evaluar y elegir la mejor opción entre múltiples caminos hacia un mismo destino (basándose en métricas y políticas).
		   • Filtrar Anuncios: Publicar rutas hacia sus vecinos únicamente si cumplen con las políticas y acuerdos comerciales locales. 
		   • Transparencia de Camino: Avisar a sus vecinos el camino exacto (secuencia de WANs) que están usando.
La Puerta de enlace es un ‘guardian’ de los intereses de su WAN

Con esta organización conceptual, ahora podemos derivar dos protocolos concretos: 
	o uno simple basado en inundación controlada,
	 o y otro similar a BGP

## Bloque 1: Enrutamiento basado en inundación 
Antes de hablar de protocolos sofisticados, conviene comenzar por el extremo opuesto: ¿qué pasa si intentamos resolver el enrutamiento entre redes usando solo las herramientas que ya conocemos?

En este bloque vamos a construir un protocolo exterior sin optimizaciones, sin agregación, sin sesiones, sin prefijos. Sólo con: inundación, caminos explícitos, y direccionamiento de enrutadores. Este modelo deliberadamente simple nos permite ver, sin distracciones, qué problemas  estructurales debe resolver cualquier protocolo de enrutamiento entre WANs
El objetivo no es eficiencia, sino transparencia conceptual: ver el mecanismo desnudo.

>[!info] Suposiciones iniciales:
> • Consideramos una interred formada por varias WAN interconectadas. 
> • Asumimos que las puertas de enlace pertenecen simultáneamente a las WAN que interconectan. 
> • Objetivo:  construir un protocolo de enrutamiento adecuado para este tipo de interredes.
>  • Consideramos  'destinos' a los enrutadores conectados a LAN. Este conjunto es mucho más pequeño que el total de los enrutadores presentes en todas las WAN.

### Abstracción de la interred en los enrutadores
 No tiene sentido que cada enrutador vea toda la topología de la interred de manera detallada, porque una interred completa es demasiado grande para que cada enrutador mantenga toda su topología. Entonces ¿Cómo reducimos la cantidad de información que debe ver un enrutador? Basta con que cada enrutador conozca de otra WAN: 
	 o Sólo algunos destinos. 
	 o Sólo algunas puertas de enlace. 
	 o Sólo alguna otra WAN con la que esta conectada.
No necesita ver la topología interna completa de todas las WAN

### Grafo de interred
¿Cómo podemos representar el grafo de una interred?
	❑ los nodos son enrutadores multiprotocolo, y
	 ❑ un lado entre dos enrutadores multiprotocolo significa que esos enrutadores están conectados vía una WAN.
	 ![[Pasted image 20260525123323.png]]
### Información de rutas
El protocolo no puede calcular caminos óptimos globales, pero igual necesita algún tipo de información de ruta para: 
	o evitar loops, 
	o comparar rutas alternativas,
	o elegir un camino razonable, 
	o exportar rutas entre WANs
La información mínima de rutas que sirve para todo esto:
	• WAN-PATH: lista de pares: <puerta de enlace, WAN> Cada par indica por qué puerta y por qué WAN pasó el aviso en su recorrido hacia al enrutador de destino.
	 • Destino: La dirección del enrutador de destino al que se refiere la ruta
	![[Pasted image 20260525124202.png]]
