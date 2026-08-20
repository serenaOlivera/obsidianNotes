chequear reinstalar vivado, programa en home, falta ejecución para llevarlo al opt
#### Modulos:
- Comportamentales:
   le estoy diciendo al sintetizador como quiero que se comporte ese modulo
- Estructurales: 
	un nuevo modulo que conecta los modulos descriptos. port mapping

dos formas distintas de hacer lo mismo, depende la ocasión.
usamos comportamental para escribit la alu ahora, not like odc.

`assign`
todos se analizan y se ejecutan en paralelo
si a vector `&a` compara todos los elementos del mismo. 

`always`
forma que el lenguaje me da para hacer logica más complejo. Si necesito hacer un case, for, if, las hago adentro del  bloque always.
Mientras la secuencialidad se interpreta, no se ejecuta.
el  sintetizador infiere un circuito que se comporta como la secuencia que di. Genera los mismos resutlados, en tiempo cero pero NO es explicitamente la secuencia.
3 tipos de always "siempre que ocurra uno de estos eventos, va a pasar lo siguiente * inserte bloque *"

**always_comb:** la lista de sensibilidad sirve para q se ejecute de vuelta c/ vez que cambien las entradas especificadas. si no pones nada, se ejecuta c/ vez que cambian TODAS las entradas.

la lista de sensibilidad se especifica con @(aca todo lo que entra en la lista)
**always_latch** 
**always_ff** si yo no pongo el reset en la lista de sensibilidad, entonces va a ser síncrono. Si esta es asíncrono, y en el instante en q baje el clock, se resetea
posedge: flanco positivo del clock
negedge: flanco negativo del clock


