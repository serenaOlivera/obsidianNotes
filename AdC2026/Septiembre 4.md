## Teórico

Seguimos en la misma filmina, so tip: Leete el capitulo 4 del patterson!

Nos quedan por ver los Hazard de control. 
hay metodos para predecir que voy a hacer.

¿Qué tan bueno/malo es una prediccion de algo? depende de 

Es lo mismo que la jerarquia de memoria, trae lo que cree que va a usar y ve dependiendo si lo q trajo estuvo bien o no.

queremos predecir si saltamos o no.
¿entonces, que e puede hacer para mejorar la capcidad de predecir?
La forma más facil sería stallear la computadora hasta que tenga que saltar, pero pierdo el tiempo.
Tengo que sbaer si tengo que saltar o no, y a donde tengo que saltar.

fetch es la dirección de memoria donde esta metida mi instrucción. No se puede saber si puedo saltar en fetch. 
si nos encontramos con  un salto tenemos que stallear hasta que este el write de la anterior para saber que debemos saltar.

stall on branch, se mete a la instrucción que sigue (en el fetch). cuando está en decode, ahí se da cunta si tiene o no que saltar.

entre las etapas se ponen los "registros" o las pipes, que contienen la información producida en ciclos previos.

simple clock:
multiple clock


## Práctico 
### Exeptions and Interrupts 

La guía 3 NO VA EN EL REPO no es entregable. Si queres ponelo en una rama, pero no va en la  main, rompe todo.
La interrupción es la base de las técnicas de mejora de rendimiento, los actuales no la usan ya.
Si no hubiese excepciones, no habría sistema operativo.

una instrucción de salto es un cambio de programa pero controlado. Las excepciones/insterrupciones son no controladas.

La interrupcion no es gratis.
Usan el ESR para vectorizar a donde tiene que saltar el micro

ERET me dice a donde tengo que volver 
el pc dice la direccion de la instruccion de la que estaba eje cutando cuando ocurrio la excepción, pero recién la siguiente instrucción ejecuta la excepción.
no alcanza con tener link register.
ERET se vale de un registro nuevo que se llama exception return register. 

una instrucción tipo s 

>[!example] Ejemplo diferencia entre ELR y ERR
>en la direccion 100 hay una isntruccipn add ejecutandose
cuando salt la excepcion, la siguiente instruccion a ejecutar es la 104 
pero como durante la instruccion de la 100 hubo una excepcion me voy a no se que ISR...
y me fijo donde tengo q ir, ej direccion 800 
cuando termino eso y le hago exception return, y quiero volver, tengo que volver 
a la 104.
> en exception link register quedo el 100 (a donde estaba el micro cuando se ejecuto la instrución)
> y hasta que alguien lo vuelva a cambiar, sigue en 100
> el ERR cuando salte va a valer 104 (proque la prox instrucción era de 104, porque no era un branc). Si yo hubiese puesto un branch a "pepe" y pepe estaba en la 200, tendría que haber vuelto a 200.
> ![[Pasted image 20260904114532.png]]

micro primero termina de ejecutar la instruccion y depsues salta a la excepción.

La guia 3 es básicamente la implementación propuesta, hay que entenderla y saber responder preguntas asociadas a esa arquitectura especificamente. 

nuestro micro solo va a generar 2 excepciones. 

la señal de  salida esync, si se pone 1, todo se pone uno, que significa que habilta que en el sigiente ciclo de clock van a registrar

Analizar el datapath con exceptions!!!
lo que esta en rojo es lo que cambio