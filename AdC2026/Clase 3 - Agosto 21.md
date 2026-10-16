### Ensamblado y desensamblado de LEGv8 + Implementación de la ISA

Ya hay repos!
módulos en carpeta source, testbench en carpeta tb
crear el archivo y setearlo como toplevel (click derecho, set as top)

### D-tipos
rm y rn son los operandos
rd el desetino
los shamt se usan para desplazar.

stur gurda datos del procesador **a la memoria**
una palabra de 64 bits del procesador, me ocupa 8 posiciones de memoria 
x22 + 64, que es el elemento 8 de A (array)

en los registros puedo guardar una sola palabra, no me queda otra que el registro este ene memoria ram.
Para el procesador la única memoria que existe es la ram. 

### CBZ
cbz los saltos. Los necesitamos cuando hay una isntrucción donde no siempre queremos ejecutar cbz = compare and branch if 0.
las instrucciones tienen 32 bits, que me ocupan 4 posiciones de memoria, si yo tengo 5 instrucciones que saltar tengo que hacer 54. Yo tengo que poner la cantidad de instrucciones que voy a saltar. El registro rt me dice si salto o no, si vale 0, salto sino no.
si es negativo salto para atras, sino salto para adelante

### Datapath
Empezamos a analizarlo por el PC (programm counter). 
el opcode pasa por la unidad de control (azul)
lo que sale del bloque Regiters son 64 bits. A la salida de a ALU voy a tener la dirección

ejemplo +
STUR x9, x0, #16
	la alu, me va a venir el 0, el 16 no esta en un registro, esta codificado literalmente en la instruccion, entra en el sign extend, se fija que tipo de instruccion es, agarro esos bits y extiendo el signo. 
	La alu dice, ok sumo, y con eso apunto a la memoria. 
	El x9 sale por el registers y tiene el dato que tiene que escribir en el data memory, segun el memread

Lo que elige el multiplexor para el shamt es el programm counter +4 o el otro canal que es el del shift left 2, que multiplica por 4 (porque las instrucciones son de 32 bots y ocupan 4 posiciones de memoria)

suponete que quermeos .. dos posiciones para arriba, pasarlo a complemento a dos es : todos los 0 los paso para 1 ,a lso 1 los paso a 0 y a eso le sumo 1.

1110 me dio en el inmediato
el sign extend me va a extender para que tenga 64 bits, adelante todos 1
tengo que moverlo dos llugares (agregarle dos 0 a la derecha) para multiplicarlo por 4
ahora imaginemos que el pc estaba en 8
sumamos 
pedirle a ludmi o chris este ejemplo (si pueden y lo copiaron) 
eso me queda en 8 porque 16-8=8

ver las señales de control, van a servir para los modulos.
las presentaciones de orga tienen todo eso presentado bonito, repasarlas.


### Nuestro procesador
Nuestro procesador tiene untop level que será la jerarquía más alta de nuestro procesador.
El datapath: "camino de los datos", donde se da el procesamiento.
Después tenemos las memorias: la de instruccion es solo una ROM, 
el cable de imem a datapath es el que no sdice que instrucción está ejecutando el micro, super genial para debbugear.

el controller tiene dos subloques, el main decodder y el alu decoddre, (el contro y el alu control del procesador de odc, una locura)

el datapath esta subdividido en varias etapas.

no tocar el gitignore. verificar que el pipeline este en 0. 