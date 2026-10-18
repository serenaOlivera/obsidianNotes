
## Teo 
estabamos viendo parelilismo de instrucciones, basicamente hay 2 formas 
 buscar paquetes de instrucciones
 1. estaticas: hacia uso del compilador para más paquetes y reacomodar sw, pero genera problemas nuevos.
 2. dinamicas

en el multiple issue, el IPC puede ser >1
podria tener un ipc de 4 si tine un clock de 4ghz, entonces teoricamente, si tenemos un pipeline comun lo máximo que podemos  llegar es a 4g instrucciones. Con lo nuestro podemos hacer 1 pico 16 g instrucciones 

static multiple issue se conocen como  => very long instruction word processor (VLIWP)
y los dinamicos = super-escalares

no puede haber dependencias en 1 paquete!!!
si puede haber entre paquetes, y hacer forwarding.

3b resolución chiquitapia, fijate que el stur le cambia el offset de las cosas?

the most useless class ever 

if u want to understand fully, first read theorical slides, they'll explain everithing to the littlest detail, after, read the lab slides, they are more approached to what the exercises in the exam will look like, BUT theorical is good because it's gonna teach you how to think it, only then you will know how to solve any kind of problem.

## Lab 
ToMaSuLoooOOooOOOO

clase que viene de 9 a 10 lab2
				resto: clase de consulta o si queda de dar algo, eso


lab2 simulador que tiene info de como se ejecutan las isntrucciones en tiempos 

Unidad funcional: alu, unidad de memoria. Son hardware dedicado para ejecutar una o un grupo de instrucciones.

Reservation station: algun tipo de memoria (guarda datos, retiene datos), y los que retiene son todos los operandos que necesita la unidad funcional para computar.
Por un lado tenemos el dato propiamente dicho o el tag de quien lo va a generar.
Address unit: no es una unidad funcional propiamente dicha, pq es un hardware q calcula direcciones pero no computa. Hace una parte de lo que hace una instrucción, entonces no se considera fully unidad funcional.

lo otro que vimis es que los register file ahora tienen campos extra; el bit de validación y el tag,
**bit de validacion:** el valor que esta aca, esta valido, lo podes sacar.
tag:  lugar de la reservation station que vaya a calcular.

hacemos fetch (etapa que no se ve en el diagrama, misma que en anterior), las instrucciones entran en la queue , y se hace issue

>[!warning] OJO
>LA ETAPA CRITICA ES LA DE ISSUE -> cuando salgo de la instruction queue (in order), y cuando las empiezo a asignar

lo que se guarda en la reesvarion station, NO es los datos de la instruccion. L ainstruccion exploto. Que la reservation station diga "la alu tiene que sumar", no significa que la operacion es la suma. No se guarda x0, o x3,  se guarda el valor o ..... tag (porque lo neceistas de otro registro)
desaparece el concepto de registros.

hay varias reservation stations por unidad funcional. 
objetivo de reservation station llenar el procesador de instrucciones que necesitan ejecutarse, y que el procesador vaya ejecutando a medida que estan listas. De manera de que yo tenga más paralelismo.

si yo cambio el orden de programa, tengo riesgo de WAR, escribo luego de leer -> dependencia que existe en procesadores out of order.

>[!warning] no voy a hacer issue de ninguna instrucción, hasta que yo no sepa si el salto se hace o no

no vamos a flushear la instruction queue!!!  
pero vamos a frenar , hasta que se haya resuelto el branch

especulación: Cómo hago para, si ya hice issue de isntrucciones, volverlas atras¿?
tiene un ahrdware especifico (reorder buffer) que tiene la capacidad de, a partir de la reservation stations, ver que instruccion es la que mando ahi. 

