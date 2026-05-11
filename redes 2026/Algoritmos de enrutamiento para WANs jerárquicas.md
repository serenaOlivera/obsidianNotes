## Bloque 1: Introducción
En el bloque anterior introdujimos jerarquía.. Dividir la red en regiones (de igual importancia) o áreas (con un área dorsal) no es solo una cuestión administrativa: cambia la forma en que cada enrutador percibe la WAN.
Ya no todos los enrutadores ven todo. Cada uno ve su región o área con detalle y las demás con resúmenes cuidadosamente construidos para preservar lo esencial sin arrastrar la complejidad completa.

Ahora, vamos a ver cómo se construyen esos resúmenes, cómo se propagan, qué ve cada tipo de enrutador y cómo se arma finalmente el grafo global sobre el que se ejecuta Dijkstra. Veremos que la jerarquía no es un adorno, sino una arquitectura que obliga a repensar el protocolo de estado de enlace: qué se inunda, hasta dónde, quién lo genera y cómo
se combinan las piezas para que toda la red siga funcionando como un sistema coherente.

## Bloque 2: Enrutamiento en red de regiones
### Introducción
La pregunta central es: ¿Cómo adaptar el protocolo de estado de enlace para que funcione cuando cada región solo conoce su topología interna?

Para responderla, vamos a derivar un algoritmo que:  mantiene el estado de enlace dentro de cada región,  construye resúmenes de región para enviar a otras regiones atravesando enlaces desde un enrutador de borde a otro, y distribuye esos resúmenes entre regiones mediante inundación
controlada, que evita bucles y limita el alcance de cada paquete.

El resultado es un protocolo que permite a cada enrutador reconstruir un grafo global híbrido: detallado en su región y resumido en las demás. Sobre ese grafo ejecutará Dijkstra para obtener rutas coherentes en
toda la WAN.

### Tipos de enrutadores
Tipos de enrutadores en una región:
- **Interno:** enrutador que no tiene enlaces hacia otras regiones.
- **De borde:** enrutador que tiene enlaces hacia otras regiones.
 **¿Qué ve un enrutador interno sobre su región?**
	 Todos los enrutadores de la región y los enlaces entre ellos. Ejemplo: grafo de la región 5 que ven sus enrutadores.
	 ![[Pasted image 20260503173115.png]]
**¿Qué ve un enrutador en una región sobre una región ajena?**
	• Ve los enrutadores de borde.
	• Ve arcos entre 2 enrutadores de borde si hay caminos dirigidos entre ellos.
	• Un arco entre dos enrutadores de borde tiene como peso el del camino más corto entre ellos.
	• Ejemplo: si longitud de camino es cantidad de saltos, un enrutador de región 2 ve de la región 5: {5A, 5C} con peso 2.
	![[Pasted image 20260503173350.png]]
**¿Cómo sería el grado de toda la red que ve un enrutador?**
	• Hay que combinar la visión detallada de la región donde está con su visión resumida de las demás regiones.
	• Colocar: grafo de su región, los grafos resumidos de las demás regiones y enlaces entre enrutadores de borde de distintas regiones. 
	• Ejemplo: grafo del enrutador 2C
	![[Pasted image 20260503173515.png]]

### Paquetes de estado de enlace

**¿Cómo sería un paquete de estado de enlace (LSP) de enrutador de dentro de una región?**
	• Ya lo vimos en el protocolo de estado de enlace.
	• Es el LSP con información de retardos a los vecinos de un enrutador.
	• Ejemplo: armar paquete de estado de enlace de 2B.
		o Enrutador 2B, número de secuencia
		o 2A, 1
		o 2D, 1
Ahora que entendemos qué información tiene disponible un enrutador
dentro y fuera de su región, el siguiente paso es preguntarnos cómo sintetizar esa información. Es decir: ¿cómo convertir la topología interna de una región en un resumen que otros enrutadores puedan usar para enrutar sin conocer todos los detalles?

 ¿Cómo sería el paquete de estado de enlace que resume una región?
	 • Nombre de enrutador de borde de región que construye el paquete,
	 • número de secuencia (para distinguirlo de paquetes de estado de enlace previos),
	 • información del grafo que ve un enrutador ajeno a esa región. 
	 • Ejemplo: LSP de la región 5.
		 o Enrutador 5A, Seq 
		 o {5A, 5C} con peso 2

Además, un enrutador de borde necesita construir un segundo tipo de paquete de estado de enlace con los enlaces con otros enrutadores de borde con los cuales está conectado directamente. Lo llamamos LSP de enlaces externos.
Ejemplo: el enrutador 3B construye el paquete de estado de enlace:
-  3B, número de secuencia
- 1C, 1
- 4B, 1
- ![[Pasted image 20260503174827.png]]

### Fases del protocolo
¿Cuáles serían los pasos de un protocolo de enrutamiento para una red de
regiones?

**• Fase 1: Para cada región A hacer lo siguiente:**
1. Se ejecuta el protocolo de estado de enlace dentro de A, hasta  completar la difusión de los LSP internos.
2. Cada enrutador de borde construye LSP de enlaces externos.
3. Entre los enrutadores de borde de A se elige un enrutador de borde designado R. Este enrutador va a ser el único responsable de generar el LSP de resumen de la región.
4. R construye el grafo resumido de A:
	   o los vértices son los enrutadores de borde de A, y
	   o los arcos son todos los pares {E1, E2} con costo C, donde C es el costo mínimo para ir de E1 a E2 dentro de A.
5. Usando el grafo resumido de A, R construye el LSP que resume la región A.


**Fase 2:**
1. Distribución de LSP que resumen en las diferentes regiones.
2. Distribución de LSP de enlaces externos.
3. Construcción del grafo de la red entera de un enrutador
4. Ejecución del algoritmo de Dijkstra sobre esa red.
5. Construcción de tabla de reenvío

#### Fase 1 del protocolo:
¿**Cómo se aplicaba el protocolo de estado de enlace dentro de una región hasta la difusión de los paquetes de enlace inclusive?**
	• Tomamos una región, a ella es aplicable el protocolo de estado de enlace. Entonces cada enrutador de la región hace lo siguiente:
		1.Descubrir sus vecinos (con uso de paquetes HELLO)
		2.Medir el costo a cada uno de sus vecinos (con uso de paquete ECHO)
		3.Construir un paquete diciendo lo que ha aprendido (llamado paquete de estado de enlace - LSP)
		4.Enviar este paquete a todos los demás enrutadores (usando inundación de difusión)
	• Los detalles pueden verlos en la parte 2 de la capa de red (bloque s6) [[Algoritmos de enrutamiento para WANs no jerárquicas]]
Para un enrutador de borde construir un LSP de enlaces externos:
	- Cuando envió paquetes HELLO se da cuenta por los nombres de los vecinos que son enrutadores de borde (toma notas de ellos). 
	- Manda paquetes ECHO a los otros enrutadores de borde con los que está conectado para averiguar el retardo a ellos.
	- Con la información de retardos a otros enrutadores de borde, construye el LSP de enlaces externos

**¿Cómo construye R designado el grafo resumido del área A?**
	a. R Construye el grafo G completo de A (a partir de los LSP internos construidos en el paso 1).
	b. Para cada enrutador de borde B de A: 
		• R ejecuta Dijkstra clásico con raíz B, obteniendo el árbol de caminos mínimos desde B hacia todos los nodos de A.
		• R extrae de ese árbol los costos mínimos de B hacia los demás enrutadores de borde.
	c. Con todos estos costos, R arma el grafo resumido de la región A.
	![[Pasted image 20260503180506.png]]

**¿Cómo se construye el paquete de estado de enlace de resumen de una región entera?**
	• La información de ese grafo resumido de la región se vuelca en un LSP resumido de la región.
	• Ahora estamos en condiciones de explicar en detalle la fase 2 del algoritmo de enrutamiento en una red de regiones.
	• Ya sabemos cómo un enrutador de borde puede representar su región mediante un grafo resumido. Pero un resumen que nadie recibe no sirve para enrutar. El siguiente problema es entonces de distribución: ¿cómo hacemos circular estos resúmenes entre regiones sin inundar toda la WAN ni generar bucles triviales?

#### Fase 2 del protocolo 
**¿Cómo hacer la distribución de los LSP que resumen las diferentes regiones?**
	- **Cada región A genera un único paquete de resumen.**
		   o El enrutador de borde designado R de la región A construye el paquete de estado de enlace P que resume la región.
	-  **Difusión interna del resumen dentro de la región A**
		   o R inunda P dentro de la región A usando inundación por difusión. Así, todos los enrutadores de borde de A reciban P y puedan reenviarlo hacia otras regiones. 
	- **Envío del resumen de A hacia otras regiones:**
		 Para cada enrutador de borde B de A y enlace E desde B con otra región, B envía P por E (recibiéndolo un enrutador de borde de la otra región).
	-**Comportamiento general de un enrutador de borde al recibir un resumen** 
		o Cuando un enrutador de borde recibe un LSP que resume una región distinta de la suya: 
			• Lo inunda dentro de su región, usando inundación por difusión.
			 • El paquete se reenvía por todos los enlaces hacia otras regiones, excepto: hacia una región de donde vino, para evitar bucles triviales.

**¿Cómo hacer la distribución de los LSP de enlaces externos?**
	• Un enrutador de borde de región A que creó el LSP P inunda por difusión dentro de A el paquete P. 
	• Los enrutadores de borde de A al recibir P lo envían por los enlaces que los conectan con otras regiones.
	 • Cuando un enrutador de borde de una región distinta de A recibe P, inunda con difusión su región con el paquete P.
	  • Cuando un enrutador de borde de una región distinta de A recibe P, manda por los enlaces con otras regiones el paquete P.
	  • Una vez que los resúmenes circulan correctamente, cada  enrutador tiene piezas dispersas de información: su topología interna y los resúmenes de las demás regiones.  El paso siguiente es ensamblar esas piezas en un grafo global coherente que   represente toda la WAN desde su punto de vista.

**¿Cuándo se puede hacer la construcción del grafo de la red entera por un enrutador?**