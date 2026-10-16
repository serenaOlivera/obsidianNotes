
Dos tipos de modulos en vivado:
#### Modulos:
- Comportamentales:
   le estoy diciendo al sintetizador como quiero que se comporte ese modulo
- Estructurales: 
	un nuevo modulo que conecta los modulos descriptos. port mapping
	`always`
forma que el lenguaje me da para hacer logica más complejo. Si necesito hacer un case, for, if, las hago adentro del  bloque always.



### Always
Para representar lógica combinacional con un bloque procedural always de propósito general:  La palabra clave always debe ir seguida de un control de evento (el símbolo @).  La lista de sensibilidad del control de evento no puede contener calificaadores posedge o negedge. 

La lista de sensibilidad debe incluir todas las entradas del bloque procedural.  El bloque procedural no puede contener otros controles de evento.  Todas las variables escritas por el bloque procedural deben actualizarse para todas las condiciones de entrada posibles.  Ninguna variable escrita por el bloque procedural puede ser escrita por otro bloque procedural.

Vemos 3 bloques procedurales con always: always_comb, always_latch y always_ff.
Un bloque procedural **always_comb** se dispara automáticamente una vez en el instante de simulación cero.  Si el contenido de un bloque procedural especializado no cumple las reglas de ese tipo de lógica, las herramientas de software pueden emitir mensajes de advertencia.

<= es asignación no bloqueante: ocurre simultáneamente con las demás (para lógica secuencial)
= es asignación bloqueante: ocurre en el orden en que aparece en el archivo (para lógica combinacional)
![[Pasted image 20260920222717.png]]



## El procesador 
CPI: clock per instruction
**Latencia:** tiempo que le lleva a una instrucción 

(TF)Quien determina el timepo del fetch es la memoria de instrucción. Si la memoria es muy lenta, se aumenta el tiempo. 
(TD)El tiempo de decode es más rápido
(TEx)la  alu hace operaciones bastante más rápido (alu esta en parte de excute)
(Tmem)La MEM, es la memoria de datos (dmem) 
(Twb)

EL T mínimo de un clock, es la suma de todos esos tiempos. Pero en realidad tengo que considerar el peor caso, porque yo no puedo cambiar el clock en función de la instrucción que tengo.
	El clock corresponde al camino crítico.  El camino crítico es el que tiene el tiempo más largo, y ese es el que marca el tiempo de todo. 

Pipeline: 
Básicamente, a medida que avanzo (FDEMW), hay 5 estaciones de trabajo y como ya hice fetch, ya lo libere (el resto no accede a esa parte del procesador, entonces puedo ocuparo por otro). ESO es pipeline, usar el tiempo eficientemente de alguna manera

k=5 (nro de etapas) y n= nro de instrucciones (en este caso 10)
El tiempo de programa con pipeline (TP) = k pulsos de reloj para que se llene el pipeline
					$$TP_{pl} = k*T_r + (n-1 *T)$$
cada una de las memorias que sigue, va a necesitar .
t es el pulso de reloj del procesador.

si no tuviese pipeline, FDEMW es 1 pulso de reloj, pero si tengo pipeline F es un pulso, D es otro pulso, Ex es otro pulso, etc. Pero sigue siendo más rápido.
acá asumimos que c/ etapa tarda lo mismo. Que es la única forma de que todo funcione. 

>[!info] Tiempo del mismo programa de un solo ciclo
>$$TP_{1\text{Ciclo}} = n*k * T_{\text{reloj con procesador con pipeline}}$$

La ganancia de velocidad 
TIempo del programa con un solo ciclo, dividido el tiempo que tarda el programa con pipeline
$$G_V = \frac{TP_{1C}}{TP_{Pl}}$$
 $$=\frac{n * k * T_{\text{tiempo de procesador con pipeline}}}{k *TP_{Pl} + (n-1)*TP_{Pl}}$$
ejemplo ejercico parcial:
	si es de un solo ciclo, el tiempo de clock tiene que ser de 800ps, porque es quien más se tarda.
	si yo pipelineo ese ejemplo, el reloj más chico debe ser de 200, porque es el que más tarda de todas las etapas.

lo ideal sería que todas las etapas duren lo mismo. (No sucede tho)
![[Pasted image 20260828100727.png]]
SI mejoro los tiempos, el tiemmpo de procesador de un ciclo sigue siendo 800ps, pero si mejoro p ej 160ps en c/ etapa, mejora el procesador de pipeline. 

Este ejemplo:
Latencia procesadoor de 1 ciclo: 800ps
Latencia de procesador con pipeline: 800ps, hago una isntruccion cada 200ps, pero el tiempo es el mismo para hacer 1 instrucción en el próximo ciclo. Vemos 3 tipos:
### Hazards
Son situaciones que previenen ejecutar la siguiente instrucción en el procesador
- Hazard estructural: un componente que necesitamos está siendo usado.
- Hazard de datos: Necesita esperar que la instrucción anterior termine  su lectura/ escritura.
- Hazard de control: Decidir una acción de control dependiendo la instrucción anterior.

Una solución para el hazard de datos es el forwarding:
Usar el resultado cuando se computa, no esperar a que esté guardado en un registro. Está bueno pero requiere conecciones extra en el datapath.
![[Pasted image 20260920224731.png]]

Can’t always avoid stalls by forwarding  If value not computed when needed  Can’t forward backward in time!
![[Pasted image 20260920224952.png]]

Code Scheduling to Avoid Stalls  Reorder code to avoid use of load result in the next instruction  C code for A = B + E; C = B + F;
![[Pasted image 20260920225206.png]]

**Dependencias de datos:** Una instrucción i tiene una dependencia de datos respecto a j, cuando i produce un resultado que necesita j.
**Dependencia de control:** Una dependencia de control determina el orden en que las instrucciones deben ejecutarse debido a la existencia de un salto condicional.
**Dependencia de datos condicional:** Una instrucción i tiene una dependencia de datos condicional respecto a j, cuando la ejecución de j está sujeta al resultado de un salto condicional.

![[Pasted image 20260921191708.png]]

**Técnicas estáticas:** El procesador siempre toma la misma decisión por defecto 
- Not taken (NT): Por defecto se asume que el salto no se va a tomar y se carga la siguiente instrucción, en caso que el salto deba tomarse, se hace flush y se realiza el fetch de la instrucción correcta. La penalidad es de 3 ciclos de clock.
- Taken (T): Por defecto el procesador asume que el salto se toma y carga la instrucción que indica el salto. Esto en un procesador como el que venimos estudiando tiene una penalidad de 3 clocks siempre (la decisión de si el salto debe tomarse se realiza en la etapa de memory). 

**Técnicas dinámicas:** El procesador decide si saltar o no considerando el historial de saltos propios o global. 
## System I/O y Excepciones

Un microprocesador se comunica con toros dispositivos a través de dferentes interfaces:
- Port-based I/O (Arquitecturas viejas):
  El procesador tiene uno o más puertos de N-bits. El software del procesador lee y escribe un puerto como lo hace con un registro.
  ![[Pasted image 20260914102949.png]]
- Bus-based I/O (actual):
  El procesador tiene dirección, datos y puertos de control que forman un system bus. El protocolo de comunicación esta construido en el procesador. Una sola instrucción lleva el protocolo de lectura o escritura en el bus.
  ![[Pasted image 20260914102957.png]]

### Tipos de bus-based I/O
El procesador se comunica con la memoria y con los periféricos, usando el mismo bus. Hay dos maneras de comunicarse ocn peroféricos:
- Memory-mapped I/O: Los registros de los periféricos ocupan direcciones en el mismo espacio direccionable que la memoria.
  ![[Pasted image 20260914103155.png]]
  No requieren instrucciones especiales. Las instrucciones que incluyen memoria como MOV y ADD trabajan con preiféricos también.
  Standard I/O requiere instrucciones especiales (ej: IN/OUT) para mover datos entre registros periféricos  y memoria.
- Standard I/O (I/O- mapped I/O): Pin adicional (M/IO) en bus indica si es una memoria o un acceso periferico.
  ![[Pasted image 20260914103331.png]]
  No perdemos espacio direccionable por los periféricos. Lógica de decodificación de direcciones más simple en los periféricos: Cuando el número de periféricos es más chico que el espacio direccionable, entonces los bits de alto orden de las direcciones pueden ser ignorados.

### Métodos de Operación I/O
- Polling- driven (E/S programada)
  El manejo se realiza mediante el uso de instrucciones de E/S por código de programa. Principal desventaja: se desperdician muchos ciclos de instrucción en revisar el estado del módulo E/S (polling)
  ![[Pasted image 20260914104654.png]]  ![[Pasted image 20260914104638.png]]
- Interrupción
  Es un recurso de HW propio de la CPU: señal de Int externa para periféricos. Es literalmente una “interrupción” o quiebre de la ejecución normal del código de programa. ![[Pasted image 20260914104850.png]]
  ![[Pasted image 20260914104759.png]]
  Al finalizar cada ciclo de instrucción el CPU verifica automáticamente si hay Int pendientes. De esta forma el “polling” lo realiza la CPU por HW: no consume ciclos de instrucción!!
  Si hay Int, el CPU salta automáticamente a una posición de memoria especifica llamada vector de interrupciones. El vector de interrupciones contiene el código (o su referencia) con los procedimientos necesarios para dar servicio a dicha interrupción. Este código se denomina ISR (Interrupt Service Routine) 
- Direct Memory Access (DMA)
  
Excepciones e interrupts:
Son eventos "no esperados" que requieren un cambio en el flujo de control.

Una **excepción** surge dentro de la CPU (opcode invalida, overflow, syscall).
Una **interrupción** surge de un controller I/O externo.

Para manejar las excepciones, se guarda el PC de la instrucción a la que interrumpimos. (En el Exception link Register ELR)
Además, guardamos la indicación del problema en el Exception Syndrome Register (ESR). Asumimos 1 bit (1 para overflow, 0 para opcode invalido)

Acciones del handler:
- Lee la causa y lo transfiere a un handler relevante,
- Determina la acción requerida
- Si se puede reiniciar, toma acción correctiva y usa el EPC para volver al programa.
- Sino, termina el programa, y reporta error usando EPC, causa, ...

