# Teórico -post parcial 1
caché!!!
Tienen niveles, la cache más cercana que tiene una computadora para trabajar son los registros, son como un amemoria caché.
EL problema es que son poquitos   y tienen poco tamaño 

>[! tip] Principio de Localidad
>Se basa en la capacidad de predecir. Tenemos la MMU = Memory Management Unit.
>El porcesador tiene que tener incorporado una unidad que se encargue d la memoria.
>Dos tipos de localidad:
>- Temporal: los items recientemente accedidos, son más likely de ser accedidos de vuelta
>- Espacial: items cerca de los recien accedidos tambien son más likely de ser accedidos


Jerarquia de memorias
Cache 1
cache 2 
memoria principal
discos duros
nube
although a mayor vlocidad, menor tamaño

**con la MMu queremos mejorar la cantidad de aciertos y disminuir la penallidad.**

Todo el resto que viene de este tema, es implementar estas ideas :))

Ya no traigo una sola palabra, traigo bloques (o lineas también se les dice)

Hit: el sistema acertó a tener el bloque que necesitaba en el nivel mas cercano del procesador, de esa manera no necesito stallear el sistema. El hit ratio es $$\text{Hit ratio}  = \frac{\text{hits}}{\text{accesses}}$$
misses es no haber acertado (duh)
$$\text{Miss ratio} = \frac{\text{misses}}{\text{accesses}} = 1- \text{hit ratio}$$

¿Porque tenemos jerarquia, hit, misses, tiempos de accesos? -> por la plataaaa

el banco tiene filas (son las columnas del diagrama) leo una fila, y la llevo a mi 

buses = misma cantidad de bits de mis registros

si yo hago hit, no tengo penaldad. si no lo encuentro en la cah+e voy a tner que hacer un acceso a la memoria principal. Chequeate el ejemplo p.11

si mi word es 4 bytes, busco 4 word wide memory
si no lo encuentro en la primera cache, pierdo 1 pulso de reloj, despues como no lo encontre en la memoria, tarda 15 pulsos de reloj, y después para volver, tardo 1 más.e

ejemplo de address subdivision diagrama profe
![[Pasted image 20260925101635.png|418]]

me fijo con el tag si es la misma dirección, pero SOLAMENTE si el bit es válido, se hace el hit, (por eso la compuerta AND).
El prumer cache se llama de correspondencia de vector, porque el dato solo tiene un lugar a donde estar alojado con respecto a su dirección digamos.

Si en cambio, como en filminas más adelante, tengo 4 cachés, para mejorar el hit rate. Tenemos una caché asociativa de 4 bits.

diagrama de 1 via o 4 vias
todo ese bloque tiene 16 palabras (4 by)
p.20 tenemos cache de 8 entradas, si yo la hago asociativa de 2 vias, con el tag voy a idnetificar 

# Lab
principio de localidad es EL principio estadistico de accesos a memoria.

la memoria cara es buena, no es buena de que "te acaricia a las noches" -Agus Laprovitta
![[Pasted image 20260925113306.png|427]]
%p = performance

 nuestro procesador solo trae una palabra de la memoria.
 La unidad de acceso del procesador si es una palabra, pero si quiero traer a mis vecinos, traigo a un bloque (una cantidad determinada de palabras).

NO  traigo el bloque y la que sigue 
Ni el procesador ni la memoria principal saben que hay una caché. La caché es un proceso autónomo.
no hay retardo al momento de determinar el hit or miss. (es despreciable)

el procesador es de 32 bits, desde la cache a la memory hay 128 bits, osea 4 palabras de 32 bits. 

RAM que sea memoria de acceso aleatorio. El tiempo de acceso de la memoria es constante, independiente de lo que se accede, eso significa RANDOM (aleatorio).

La caché es de acceso asociativo, por más que se catalogue como RAM, es de nombrecito nomas, no sirve para nada :)
Una memoria asociativa guarda lineas, con etiquetas asociadas (tags). 

Cuando bajo a buscar algo a un nivel más bajo de memoria no me trae una palabra, me trae un bloque completo de palabras (¿Cuántas?, depende)

Trae el bloque que contiene la dirección que quiero 
El bloque tiene que ser de tamaño k* el tamaño de la palabra.

Si todos los bits de validación dicen 0, significa que esa información en toda esa cache es inválida.
¿Qué bloque de memoria se va a usar en que línea de caché?

Ojo con leer el patterson porque solo trae siempre 1 bloque fuese 1 palabra del procesador. No hacemos eso nosotros.


Partimos la memoria en partes iguales que la caché. Entonces la cache entra 4 veces ahi. La ubicación en caché es la misma ....?
El problema del acceso directo, es que no puedo acceder a distintas direcciones 

**los bits menos significativos de linea  me dicen el numero de palabra adentro del bloque.**
La cantidad de bits de linea se va a volver conforme crezca o reduzca la cache

la etiqueta es cualquier valor. 
