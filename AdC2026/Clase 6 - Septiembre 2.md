## Terórico
ancho de banda: cuántas instrucciones..... --> completar!!!

si tengo n instrucciones,
k cantidad de etapas (5 en neustro caso)

al haber pipeline, podemos tener hazards.
si yo no paralelizo --> no hay peligro
cuando paralelizo si, porque se quieren acceder al mismo espacio varias instrucciones.

forwarding: toma el dato chabon!!, no necesito stallear
nop  = skip = add xzr, xzr, xzr --> no hizo absolutamente nada más que ganarme tiempo :)

filimina 40
1y3 dependencia de datos
2 y 3 dependencia de datos
literalmente repitio todo lo mismo que la clase pasada.

------------------------------------------------------------------------

## Lab

ejemplos dispositivo entrada-salida: teclado, mouse
todo aquello que le haga llegar datos al sistema computacional.

yo direcciono y viene una palabra de memoria de 1 byte
si yo quiero traer 64 bits tengo que traer 8 palabras seguidas.

en vez de llamarle palabras le llamamos registros de entrada/salida.
quiero acceder a espacio direccionable de registros de entrada/salida.

una no quita espacio, la otra no complejiza la isa, ejemplo: cortex A9

Tecnicas atadas a una evolución histórica, 

**Interrupción**
me voy, voy a ejecutar otra cosa que no tenga q ver con esto.
el procesador si chequea que este, pero es automático, no consume ciclos.

la isr esta contenida en un vector
¿Dónde está el vector?
