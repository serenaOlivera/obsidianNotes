Antes de hablar de protocolos sofisticados, conviene comenzar por el extremo opuesto: ¿qué pasa si intentamos resolver el enrutamiento entre redes usando solo las herramientas que ya conocemos?

En este bloque vamos a construir un protocolo exterior sin optimizaciones, sin agregación, sin sesiones, sin prefijos. Sólo con: inundación, caminos explícitos, y direccionamiento de enrutadores. Este modelo deliberadamente simple nos permite ver, sin distracciones, qué problemas  estructurales debe resolver cualquier protocolo de enrutamiento entre WANs
El objetivo no es eficiencia, sino transparencia conceptual: ver el mecanismo desnudo.

>[!info]- Suposiciones iniciales:
> • Consideramos una interred formada por varias WAN interconectadas. 
> • Asumimos que las puertas de enlace pertenecen simultáneamente a las WAN que interconectan. 
> • Objetivo:  construir un protocolo de enrutamiento adecuado para este tipo de interredes.
>  • Consideramos  'destinos' a los enrutadores conectados a LAN. Este conjunto es mucho más pequeño que el total de los enrutadores presentes en todas las WAN.

## Abstracción de la interred en los enrutadores
 No tiene sentido que cada enrutador vea toda la topología de la interred de manera detallada, porque una interred completa es demasiado grande para que cada enrutador mantenga toda su topología. Entonces ¿Cómo reducimos la cantidad de información que debe ver un enrutador? Basta con que cada enrutador conozca de otra WAN: 
	 o Sólo algunos destinos. 
	 o Sólo algunas puertas de enlace. 
	 o Sólo alguna otra WAN con la que esta conectada.
No necesita ver la topología interna completa de todas las WAN

## Grafo de interred
¿Cómo podemos representar el grafo de una interred?
	❑ los nodos son enrutadores multiprotocolo, y
	 ❑ un lado entre dos enrutadores multiprotocolo significa que esos enrutadores están conectados vía una WAN.
	 ![[Pasted image 20260525123323.png]]
## Información de rutas
El protocolo no puede calcular caminos óptimos globales, pero igual necesita algún tipo de información de ruta para: 
-  evitar loops, 
- comparar rutas alternativas,
- elegir un camino razonable, 
- exportar rutas entre WANs
La información mínima de rutas que sirve para todo esto:
	• WAN-PATH: lista de pares: <puerta de enlace, WAN> Cada par indica por qué puerta y por qué WAN pasó el aviso en su recorrido hacia al enrutador de destino.
	 • Destino: La dirección del enrutador de destino al que se refiere la ruta
	![[Pasted image 20260525124202.png]]

>[!question] ¿Cómo hacer para propagar información de rutas? 
>• Si la ruta a anunciar entra por puerta de enlace P entonces, se inunda por difusión esa ruta por todas las WAN conectadas a P donde esa ruta es válida, menos por la WAN por la que llegó

El protocolo de enrutamiento que vamos a definir usa únicamente dos tipos de avisos: 
- Aviso de ruta: informa la existencia de un camino hacia un destino. 
- Aviso de remoción de ruta. Invalida un camino previamente enunciado.

## Avisos de rutas
• Un aviso de ruta contiene tres elementos fundamentales: 
- Destino = R (dirección del enrutador al que se refiere la ruta) 
- Secuencia = n (número de secuencia que permite identificar cuál es el aviso más reciente) 
- Camino (WAN-PATH): lista de pares que describe por dónde pasó el aviso en su recorrido hacia el destino.

>[!info] Relación con la tabla de inundación: 
>- La tabla de inundación no guarda rutas completas. 
>- Sólo guarda referencias a los paquetes de aviso. 
>- Los paquetes de aviso con sus caminos explícitos se guardan localmente en el enrutador

#### Inundación:
Tabla de inundación:
-  Guarda entradas de la forma:<puerta de enlace de origen, destino, número de secuencia, id_paquete>
- Para cada puerta de enlace de origen, mantiene una lista ordenada lexicográficamente por:
	   • Destino y 
	   • Número de secuencia.

>[!question] ¿Qué referencia? 
> Cada entrada apunta al paquete de aviso correspondiente, que contiene el camino explícito (WAN-PATH).  Los paquetes referenciados se guardan localmente en el enrutador. 
> 

>[!question] ¿Para qué sirve? 
>-  Mantener un registro histórico de ruta vistas (útil para comparar rutas y elegir la mejor). 
>- Saber cuál es el aviso mas reciente para cada destino (comparando secuencias). 
>- Evitar reprocesar avisos viejos (si llega aviso con secuencia menor o igual, se descarta). 
>- Evitar loops (el camino explícito permite detector si la Puerta ya apareció).

#### Exportación de avisos
Situación: Una puerta de enlace recibe un aviso por la WAN_A a la que pertenece y decide exportarlo a la WAN_B ¿Cuáles son los pasos del proceso? 
1. Aplicar política de salida: la puerta de enlace evalúa: cumple_política_salida(aviso, WAN_B) 
2. Si no cumple: no se exporta. 
3. Si se cumple: extender el camino explícito. Antes de exportar, se agrega al final de la WAN-PATH: . Esto registra por dónde llegó el aviso. Se reenvía el aviso por WAN_B. Se envía el aviso actualizado hacia la WAN vecina, permitiendo que otras puertas de enlace conozcan la ruta

Resultado de la exportación de aviso: El camino explícito crece cada vez que una ruta cruza de una WAN a otra, permitiendo: rastrear el recorrido, evitar loops, comparar rutas, y aplicar políticas de exportación de manera local.

#### Origen del primer aviso de ruta
¿De dónde sale el primer aviso? 
Del propio destino R: R anuncia su propia existencia, genera el primer aviso de ruta, y ese aviso comienza a inundarse dentro de la WAN donde se encuentra.
Esto marca el nacimiento de la ruta. Notar que Si R está en WAN_A: 
	• una puerta de enlace P que está en la WAN_A y WAN_B, recibe aviso emitido por R dentro de WAN_A. 
	• Luego P puede exportarlo a WAN_B (si su política de salida lo permite)

## Avisos de remoción
 Un aviso de remoción indica que una ruta previamente anunciada deja de ser válida.  Incluye el camino a remover.
  Las rutas una vez anunciadas, permanecen vigentes hasta que un aviso de remoción explícito las invalida. 
   ¿Cuál es el comportamiento del enrutador al recibir un aviso de remoción? 
   1. Eliminar la ruta correspondiente: se borra de la tabla de inundación la entrada indicada al camino indicado.
   2. Propagar la remoción: El aviso se reenvía igual que un aviso de ruta, respetando políticas de salida.
   3. Recalcular la mejor ruta: Se elige una nueva ruta entre las restantes (si existen)
   4. Actualizar la tabla de reenvío: si hay una nueva mejor ruta, se instala. Si no la hay, se elimina la entrada

**¿Dónde se genera un aviso de remoción?** 
Cualquier puerta de enlace que detecte que una ruta ya no es válida, puede generar un aviso de remoción. 

**¿Cuándo detecta una puerta de enlace que debe generar un aviso de remoción?**
 Cuando la puerta de enlace G pierde conectividad hacia el destino R en su WAN_A porque el enrutador se apaga o se desconecta. G genera: 
  ``AVISO_REMOVER(destino=R, secuencia=nueva, camino=[], alcance=GLOBAL) ``
 El mismo debe propagarse globalmente. 
 
 Un cambio de política de entrada que invalida rutas ya aceptadas, lleva a generar avisos de remoción.  Esta remoción debe hacerse dentro de la WAN donde se aplica la política. El parámetro alcance en AVISO_REMOVER debe fijarse en LOCAL.
 
  Un cambio de política de salida no genera remociones, porque las rutas ya anunciadas permanecen vigentes hasta que se remuevan explícitamente.
## Independencia entre dominios
Cada WAN funciona como un dominio autónomo: sus decisiones internas no deben afectar automáticamente a otras WAN. 
¿Qué significa la independencia entre dominios? 
- Cada WAN controla qué rutas acepta (mediante sus políticas de entrada.) 
- Cada WAN controla qué rutas exporta (mediante sus políticas de salida.) 
- Los cambios internos no se propagan hacia afuera (por ejemplo, remociones locales de rutas por políticas.) 
- Las rutas exportadas permanecen válidas en otras WAN aunque la WAN de origen cambie sus reglas internas

La independencia entre dominios es importante porque:
- Evita que decisiones locales contaminen toda la interred. 
- Permite que cada WAN tenga sus propias reglas, preferencias y restricciones. 
- Mantiene la coherencia del protocolo: las remociones globales solo ocurren por pérdida real de conectividad, no por cambios internos.

Resumen: Independencia entre dominios = cada WAN es un espacio de inundación autónomo, con políticas propias, y sus decisiones internas no invalidan rutas fuera de ella

### Información confiable
Información confiable vs no confiable
- No todos los avisos de ruta deben aceptarse. La confiabilidad depende de su origen, su trayectoria y sus propiedades.
-  Un aviso se considera confiable cuando:
	  -  Proviene de una puerta de enlace autorizada 
	  - Llega desde una WAN permitida 
	  - Su camino no incluye puertas prohibidas 
	  - Su secuencia es coherente con el estado actual 
	  - Su longitud es razonable 
	  - Cumple las políticas internas de la WAN (restricciones administrativas o de seguridad)
Estos avisos pueden entrar en la tabla de inundación.  Los avisos no confiables deben ser rechazados por las políticas de entrada o no exportados por las políticas de salida.  La distinción entre información confiable y no confiable es la base para aplicar políticas de entrada y salida, y para mantener la independencia entre dominios


## Políticas de entrada
Función de decisión: la política de entrada se modela como una función abstracta. ``cumple_política_entrada(aviso)``
Determina si un aviso puede entrar a la tabla de inundación. 

>[!question] ¿Qué evalúa una política de entrada? 
> A modo de ejemplo, la puerta de enlace puede rechazar un aviso si 
> - El camino pasa por una puerta de enlace prohibida (por razones administrativas o de seguridad.) 
> - La WAN de origen no está permitida (control de dominios de confianza). 
> - El destino pertenece a un conjunto bloqueado (filtrado de destinos no deseados) 
> - El camino es demasiado largo (evita procesar avisos obsoletos) 
> - La puerta de enlace emisora no está autorizada (control de quién puede anunciar rutas

Las políticas de entrada permiten: 
- Controlar qué rutas se aceptan. 
- Proteger la WAN de rutas no deseadas. 
- Mantener la tabla de inundación limpia y coherente

## Políticas de salida
Función de decisión: la política de salida se modela como una función abstracta. 
``cumple_política_salida(aviso, WAN_destino)``
Determina si el aviso puede exportarse hacia una WAN vecina. 
>[!question] ¿Qué evalúa la política de salida? 
> A modo de ejemplo, la puerta de enlace puede decidir no exportar un aviso si: 
> - El destino pertenece a un conjunto bloqueado (filtrado de destinos no deseados hacia ciertas WANs) 
> - No anuncio rutas que no me conviene propagar (criterios administrativos, económicos o de seguridad). 
> - No anuncio rutas que no aprendí por canales confiables (control de confianza sobre el origen de la información)

Las políticas de salida permiten: 
- Controlar qué rutas se propagan hacia otras WAN. 
- Limitar la visibilidad de rutas internas. 
- Proteger la interred de información no confiable 
- Mantener independencia entre dominios.

## Selección de rutas a un destino
¿Cómo decide un enrutador llegar a un destino R? 
Para elegir la mejor ruta hacia un destino R, el enrutador realiza:
1. Búsqueda en la tabla de inundación: Recupera todas las entradas asociadas al destino R (todas las secuencias que recibió).
2. Recuperación de los avisos: Obtiene los paquetes de aviso correspondientes, cada uno con su camino explicito (WAN-PATH).
3. Aplicación del criterio de selección: compara todas las rutas candidatas y elige la mejor.

**Criterios de selección de rutas**
1. Menor cantidad de WAN en el camino: prefiere rutas que atraviesan menos dominios. 
2. Si hay empate: menor costo de salida (se elige la ruta cuyo primer salto tiene el menor costo)
3. Si persiste el empate: función de preferencia local. () Criterio configurable por la WAN o la puerta de enlace (por ejemplo, preferir ciertos vecinos, políticas internas, etc.))

## Construcción de la tabla de reenvío
Construcción de tabla de reenvío (Enrutador E -> Destino R) 
1. Selección de la mejor ruta: El enrutador E elige la mejor ruta disponible hacia el destino R, usando los criterios de selección.
2. Si no existe ninguna ruta hacia R: se elimina la entrada correspondiente a R de la tabla de reenvío de E. 
3. Caso con una ruta válida: Si existe al menos una ruta hacia R:
    a.  Identificar la puerta de enlace de salida P. Es la puerta de enlace por la cual P debe salir de su WAN para seguir el camino hacia R. 
    b. Usar la tabla de reenvío ya existente hacia P. La tabla de reenvío de E ya contiene línea de salida para llegar a P (resultado del algoritmo interno de enrutamiento).
	 c. Reutilizar esa línea de salida. Esa misma línea de salida es la que E debe usar para llegar a R

**Resumen conceptual:** No se recalculan caminos internos cada vez. La tabla de reenvío hacia P ya representa el camino más corto. Para llegar a R, basta seguir el mismo primer salto

## Recapitulación
**Propiedades del protocolo** 
- *Convergencia dentro de cada WAN*: si no hay cambios en la interred, todos los enrutadores de una misma WAN terminan con la misma información de rutas. 
- *Evita loops por inspección del camino:* Cada aviso incluye su camino explícito. Los enrutadores pueden detectar y descartar rutas que formen ciclos. 
- *Permite políticas locales:* cada WAN y cada puerta de enlace puede aplicar criterios propios para aceptar, rechazar o exportar avisos. 
- *Permite múltiples rutas candidatas:* Los enrutadores pueden almacenar varias rutas hacia un mismo destino, y elegir la mejor según criterios definidos. 
- *Permite remoción explícita:* Las rutas no expiran automáticamente. Solo se eliminan mediante avisos de remoción. 
- *No es un protocolo optimizado:* Este protocolo prioriza claridad conceptual sobre eficiencia. No optimiza selección de rutas, no optimiza propagación de avisos, no optimiza convergencia. Es un modelo didáctico para estudiar las ideas fundamentales
