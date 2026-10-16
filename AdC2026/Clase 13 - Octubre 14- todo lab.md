objetivo 2 primeras horas:
## Terminar guia
### Repaso predictores
vimos 3 predictores: 
- local :  **info de las ejecuciones de ese mismo salto anteriormente**. En la memoria guardamos 2 bits que no s indican en que estado estamos. Para cambiar la predicción necesito equivocarme 2 veces.  Es muy bueno cuando tenemos saltos que la gran mayotía de veces predicen lo mismo .
- global: es muy distinto porque basa la info que usa para predecir, no tiene que ver con otras ejecuciones del mismo salto, sino que **se fija lo que hicieron los otros saltos del micro.**
diferencia entre este predictor y el local es la info que estoy utilizando para predecir. 
- predictor de dos niveles: combinación de los dos predictores. Básicamente a la memoria, (pht, conde estan los 2 bits) la voy a indexar, no solo con e lglobal register o el program counter, sino la concatenación de los dos. Este predictora mejora a los anteriores, proque tenemos un predictor global pero asociado localmente a los distintos saltos.
  
  Problemas posibles: colisión de dos casos que estan intentando llevar la maquina de estados para distintos lugares:  En este caso como le estoy concatenando los bits menos significativos del programm counter no va a haber conflicto.
  
  Puedo tener el mismo patron para distintos saltos, pero a la vez varios patrones para el mismo salto. 

### Ejercicio 5:
patron: T,T, NT, T (se va a repetir banda de veces)
n: cantidad de bits del global register
m: cantidad de bits que estoy tomando 

el NT es la predicción de cuando j vale 3  (porque incremento la variable y despues salto)
cuando el global register vea 0111 va a decir: lo que yo tengo que decir es no taken 

en la filmina N es not taken, en el pizarron lo referencian como NT 

los bits entran por la derecha
1101 ---> mira como se desliza el 0!!!
1011
0111
1110  --> este es ya del otro loop (el de más arriba con las i)

este predictor es mejor que el de 2 bits, porque el de 2 bits siempre se equivocaria en la slaida del salto 
Voy a tener una predicción de $\frac{2}{3}$


Cada vez q sa un patron, va a  indexar a la memoria que tiene adentro 2 bits. 
Una cosa ees el patron de saltos (lo que va a pasar en la dinamica de salto que tengo) , pero no es lo que va a hacer el predictor. es en combinacion con el program counter
por cada combinacion de gr + pc va  a haber una maquina de estado 

por eso tengo la memoria de 2 bits de ancho por $2^n +m$

ME QUEDO CON LOS 4 BITS MENOS SIGNFICATIVOS DEL PC 

la primera vez que se ejecute, el global register va a tener basura, mientras más ejecutemos nuestro loop, más se va a estabilizar.

en este caso yo espero que sature alguno de los 2 estados.


modelo de ejercicio para parcial: tenes este estasdo, el gr vale tanto, la memoria se inicializa en tanto, corre el codigo y decime como se ve la memoria despues de x iteraciones


### Predictor gshare
3## Ejercicio 6 > no prestaste atencion :)
mejora muy leve al de dos niveles. En lugar de concaternarlos, se hace un hash (or exclusiva)

inicialmente lo más facil que se va a entrenar es un predictor local. El global depende 

LAB2: PREDICTORES!!

### Predictores por torneo
El predictor dle medio acciona el muz que dice, toma la predicción del global o la del local.

### Tagged Hybrid Predictors
es el gshare (de dos niveles con or exclusiva) .
La idea de este predictor es. yo saco la prediccion y despues me fijo cuál funciona mejor y elijo ese. EL base predictor, suele ser un predictor local o algo sencillo para que funcione al principio. 
Es el predictor que más se usa. 


algo tambien muy ussado es el predictor de fin de ciclo: se da cuenta q es un bucle(?) --> not sure 

## Static Multiple Issue Processor

idea de patterson para explicar este tema: en nuestro micro es muy raro, si yo pongo otro sumador, puedo ejecutar un instruccion de memoria y una instruccion tipo r al mismo tiempo, porque si yo aumento algunos recursos, cada vez que yo ejecute una instruccion de tipo r, que use la alu, no necesito acceder a la memoria. 
Son muy pocos los recursos que debo duplicar para poder acceder a 2 instrucciones al mismo tiempo--> este es una porqueria ;)

static two issue datapath. 
- necesito tener 2 instrucciones completamente diferentes
- no tengan dependencias de datos
- si es un salto se ve l adependencia de control, no puedo hacer un cbz con un load en el mismo issue packet, porque siempre se va a cargar el ldur
- si el load esta antes del cbz s lo puedo hacer, porque se va a ejecutar si o si.

el otro gran problema es:
imaginate que tenes un add x0, x1, x2 
					 ldur x0,[x1,#0]
no es una depenencia real de datos, porque ese dato no lo voy a usar en el load 
, si tuviesemos x0, en lugar de x1 en  el ldur, es una dependencia de datos nueva.

issue es una etapa entera que demora un clock. 

cool thing ---> https://docs.openhwgroup.org/projects/cva6-user-manual/


preguntarle a los chicos como vienen con el lab 


### Dependencias de datos
Dependencia: son propiedades del programa que generan hazard o no.
como tenemos dependencia de datos a traves de lso regisros, tambien podemos tener dependencia de datos en memoria. En el micro que venimos viendo eso no existe, pero en un procesador fuera de orden, puede pasar (lo vamos a ver más adelante). Un stur y dur podrian estar apuntandome a la misma posicion de memoria (compliqueti)


ahora se van a dividir en 2.
1. Dependencia real de datos RAW: Read after write. Leo, despues de haber escrito
   `` add x0, x1,x2
   ` ldur xo, [x0, #0]`` dependencia x0
2. Dependencia de nombre: WAW (Write After Write) no hay un flujo real de datos 
   `ver ejemplos filmina`

Ejercicio 6
WAW facil de resolver porque no hay un flujo de datos real. se le cambia el nombre y ya esta :)

a) ![[Pasted image 20261014115637.png]]

b) tambien me evito el stall 
se puede poner el load jutno con el subi, el libro esta crazy loco 

c) Loop unrolling 
en lugar d ejecutar una iteracion ejecute varias de mi loop.

## Ultimo teo para parcial: TOMASULO!!!
(introduccion tho, tomasulo seguro lo explican bien clase que viene)

tomasulo = una de las formas de implementar dynamic scheduling. (multiple issue dinamico)
objetivo de dynamic scheduling ---> reducir stalls 

issue $\equiv$ schedule
mac multiply and acummulate 

**cuando la instruccion espera que el hardware este listo, tengo un hazard estructural**
