## Teórico
el tiempo de acceso de la memoria en promedio va a depender de la cache (ancho, banda, etc).

$\frac{\text{accesos a memoria(por programa)}}{\text{Programa}} \ \ X \ \ \text{Miss rate} \ \  X \ \ \text{Miss penalty} + \frac{\text{Instructions}}{Program} \  \ X \ \ \frac{\text{Misses}}{\text{Instruction}}\ \  X\ \  \text{Miss penalty}$
en la cache de instrucciones tambien tendra su miss rate

Con toda esta info podemos calcular el AMAT (Average access time)
$$AMAT = \text{Hit time} + \text{Miss rate} \ \ X\ \ \text{Miss penalty}$$
### Técnicas que nos disminuyen el CPI (Clock Per Instruction)
(y aumentan el IPC (instruction per clock))

**mira el example larger block size** 

dado el programa (generalmente)
l numero de bloque determina el set 
>[!notes] numero de bloque modulo # de sets en cache


LRU : Least Recently Used 
Reemplazamos al que lleva mas tiempo en la cahce
Cada miss es un monton de pulsos de relojes 

No es cuestion de poner a lo bestia asociatividad porque la asociatividad se plancha a más asociatividades (pensa  grafico logaritmo)

para mejorar los miss rate, lo unico que nos queda es asociatividad, pero también queremos mejorar la miss penalty, para eso utilizamos las caché multinivel .
que red



### Instruction Level Parallelism
si tengo 2 issue pipe stages, es como que tengo 2 pipelines y se ejecutan en paralelo, (está bueno porque ejecutas más instrucciones en menos tiempo de clock)
La unica restricción que tiene 

El concepto es que en una de las vías de pipeline solamente puede haber una instrucción de alu o branch, y en la otra solo puede haber load o store 
(por los otros recursos que tenemos que usar)

En un **mismo** paquete, no puede haber dependencia de datos entre ellos. No hay forma de 
solucionarlo si sucediera.

RAW  (Read After Write) sigue existiendo (todos los hazards que vimos hasta ahora basicamente)
WAW: (write after write)- dependencia real de datos
para mantener la semantica ejecuto secuencial, pero si estan en el mismo paquete, como lo aseguro? La solución 

we do have waw condicionales y raw condicionales 

static multiple issue 
- compiler groups instructions to be issued toghether
- packages them into issue slots 
- compiler detects and avoids hazards

dinamic multiple issue 
- CPU examines instruction stream and choosees instructions to issue each cycle
- compiler can help by reordering instructions
- CPU resolves hazards using ....

Microarquitectura ARM Cortex A53 es dinámica 

clase q viene tomasulo!

multi threading (multi hilos)


## Lab
si dieron algo importante en el practico pasado, me podrias mandar foto despues? el viernes no pude ir al final 