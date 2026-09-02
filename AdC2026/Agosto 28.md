filmina: "Chapter 4: The proccesor"
Nos queremos interesar en la performance "estamos obsesionados con que la computadora ande más rápido". 

Una instrucción arranca en el flanco ascendente de un pulso de reloj 
**foto 1**
CPI: clock per instruction
**Latencia:** tiempo que le lleva a una instrucción 

**grafico de FDEMW en el cuaderno  **
(TF)Quien determina el timepo del fetch es la memoria de instrucción. Si la memoria es muy lenta, se aumenta el tiempo. 
(TD)El tiempo de decode es más rápido
(TEx)la  alu hace operaciones bastante más rápido (alu esta en parte de excute)
(Tmem)La MEM, es la memoria de datos (dmem) 
(Twb)

EL T mínimo de un clock, es la suma de todos esos tiempos. Pero en realidad tengo que considerar el peor caso, porque yo no puedo cambiar el clock en función de la instrucción que tengo.
	El clock corresponde al camino crítico.  El camino crítico es el que tiene el tiempo más largo, y ese es el que marca el tiempo de todo. 

Pipeline: 
Básicamente, a medida que avanzo (FDEMW), hay 5 estaciones de trabajo y como ya hice fetch, ya lo libere (el resto no accede a esa parte del procesador, entonces puedo ocuparo por otro). ESO es pipeline, usar el tiempo eficientemente de alguna manera (lavarropas ejemplo)

k=5 y n= nro de instrucciones (en este caso 10)
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


ojo, no se que onda esto: = $\frac{\frac{1}{TP_PL}}{\frac{1}{TP_{1C}}}$
si tenemos suerte y todo nos va bien, la ganancia real es k (despejando y operando)
ejemplo ejercico parcial:
	si es de un solo ciclo, el tiempo de clock tiene que ser de 800ps, porque es quien más se tarda.
	si yo pipelineo ese ejemplo, el reloj más chico debe ser de 200, porque es el que más tarda de todas las etapas.

lo ideal sería que todas las etapas duren lo mismo. (No sucede tho)
![[Pasted image 20260828100727.png]]
SI mejoro los tiempos, el tiemmpo de procesador de un ciclo sigue siendo 800ps, pero si mejoro p ej 160ps en c/ etapa, mejora el procesador de pipeline. 

Este ejemplo:
Latencia procesadoor de 1 ciclo: 800ps
Latencia de procesador con pipeline: 800ps, hago una isntruccion cada 200ps, pero el tiempo es el mismo para hacer 1 instrucción

El ancho de banda de procesador con pipeline es de 200ps

>[!tip] 
>El tiempo de procesador de un ciclo, no es k veces el tiempo de procesador con pipeline.
>No estan balanceadas. 

Entonces.. ¿Cómo se aplica esto a nuestro procesador LEGv8?
alineacion significa p ej que cada instruccion puede estar en un múltiplo de 4 (porque las instrucciones son de 32 bits)

### **Hazard**
Peligro significa peligro, no que pasó algo (safety hazard, fire hazard)
En un procesador de un ciclo, el único peligro que tenemos es que un programa no nos ande bien :|
El peligrp en un pipeline, es p ej, cuando tenemo MEDF, porque M es la memoria de datos y F es la memoria de instrucciones, ambos acceden a la memoria al mismo tiempo. En este caso no hay drama porque nuestra estructura tiene 2 memorias separadas. Si estuviesen juntas, habría problema.
Tengo peligro en WMEDF porque W escribe en los registros y leo los registros (en fetch creo)
hago trampita, me conviene primero escribir los registros y despues leerlos (me lo escribio en primera mitad y me lo leyo en la segunda mitad)
foto 3 capaz
siempre el tiempo de escribir debe ser la mitad del tiempo de lo leido, asi va más rápido. 

Si la segunda instrucción quiere leer el registro de la primera, lee mal. Eso es un hazard de datos 

Tipos de hazards
**estructurales:**
**datos:**



## Presentación Lab 1
todavia no tenemos el conocimiento, pero quieren presentarlo cuanto antes.

si podemos hacer branches, pero el codigo final debe estar en la main. pq su script de correción no contempla las branches.
ej 2 necesario para promocion 

#### Desarrollo 
leer las explicaciones técnicas :) 
parametro de simulacion cambia la frecuencia del clock, lo necesitamos lento para que se vea en la placa, pero al

ludmi tiene un blind hatred por ajedrecistas con ego alto y gente que le quema el cafe 


solamente podemos usar movz movk

