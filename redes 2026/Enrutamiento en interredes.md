## Introducción
Organización del enrutamiento en 2 niveles
	El modelo de dos niveles permite escalar el enrutamiento sin que cada enrutador deba conocer la topología completa de la interred. Los dos niveles de enrutamiento que vemos, son:
		 ❑ Protocolo de puerta de enlace interior (PPEI). Cada red usa su propio protocolo interno. Pueden ser distintos entre sí. 
		 ❑ Protocolo de puerta de enlace exterior (PPEE). Es el protocolo en común para enrutar entre redes. Todas las redes deben usar el mismo PPEE. 
			 
>[!question] ¿Cuántos protocolos distintos PPEI pueden usarse? 
>La interred puede usar diferentes protocolos PPEI en sus redes

Es necesario estudiar protocolos de puerta de enlace exterior (PPEE) porque:
	 o Las tablas de reenvío deben permitir mandar mensajes entre máquinas conectadas a redes diferentes.  El PPEE permite agregar información a ser usada con ese fin a las tablas de reenvío de los enrutadores.
	  o El enrutamiento de PPEE se preocupa de establecer las rutas a usar (que pasan por diferentes WAN) para permitir que se comuniquen máquinas pertenecientes a distintas WAN.

Lo que un protocolo exterior NO puede asumir es que:
- No puede ver la topología interna de otras redes.
- No puede depender de que todos usen el mismo PPEI.
- No puede imponer métricas globales.
- No puede forzar a los enrutadores internos a participar. 
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

## [[Bloque 1- Enrutamiento basado en inundación ]]

## [[Bloque 2- Hacia BGP desde Primeros Principios]]

## Idea unificadora de los protocolos de interred
 1. Anunciar destinos: Toda interred comienza cuando una red informa qué destinos existen detrás de ella.
 2. Propagar rutas: Esas rutas deben viajar entre dominios autónomos, con mecanismos que eviten ciclos y mantengan coherencia.
 3. Filtrar con políticas: Cada red decide qué acepta y qué anuncia, preservando su autonomía administrativa. 
 4. Comparar rutas: Los avisos pueden llegar por múltiples caminos; cada puerta de enlace debe evaluarlos según criterios locales. 
 5. Elegir la mejor ruta: La selección es siempre local; cada dominio decide qué camino prefiere hacia cada destino. 
 6. Instalar el siguiente salto: La ruta elegida se traduce en un next-hop concreto, reutilizando el enrutamiento interno.
 7. Mantener coherencia sin conocer toda la red: El desafío central: enrutar globalmente con información parcial, sin topología completa, sin métrica universal y sin control centralizado.