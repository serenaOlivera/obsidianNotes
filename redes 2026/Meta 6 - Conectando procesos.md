Este bloque responde a ¿Cómo logramos que programas específicos en máquinas distintas se comuniquen correctamente, incluso cuando la red es imperfecta?

Para distinguir los mensajes para un programa con los mensajes para otro programa, los mensajes deben indicar cuál es el programa receptor usando un identificador de programa (puerto)

## Ordenamiento de paquetes
Si mandamos dos paquetes de un mismo mensaje, esos paquetes no necesariamente van a seguir la misma ruta, puede que cambien las rutas entre paquetes porque se ejecutó el algoritmo de enrutamiento .
Si los dos paquetes de un mensaje son enviados, no necesariamente van a llegar en orden (uno puede perderse y debe ser renviado, otro puede seguir una ruta más corta), entonces pueden llegar fuera de orden.

Entonces, es necesario ordenar los paquetes de un mensaje porque una aplicación de red necesita procesar el mensje completo ordenado.


## Control de congestión 
 Cuando muchos flujos simultáneos compiten por la misma red, aunque cada flujo pueda ordenar sus paquetes, la red puede saturarse, perder paquetes masivamente o volverse inestable. A este fenómeno se lo llama congestión y requiere mecanismos específicos para evitar que la red colapse cuando múltiples procesos intentan comunicarse al mismo tiempo.
La congestión ocurre cuando la red no puede manejar la carga de paquetes que recibe de manera aceptable.
![[Pasted image 20260318103015.png]]


¿Cómo controlar la congestión?
	Las computadoras emisoras se enteran de la congestión y reducen el tráfico de salida. Esta idea puede ser implementada de muchas maneras. A esto se le llama control de congestión 

## Control de flujo 
El control de congestión evita que la red se sature cuando muchos flujos compiten por los mismos enrutadores. Pero este mecanismo solo considera el estado de la red, no el estado de los procesos que se comunican. 
Incluso si hay congestión, un receptor puede saturarse si el emisor envía datos más rápido de lo que puede procesarlos. Cuando eso ocurre, el receptor pierde paquetes y el emisor probablemente va a interpretar esas pérdidas como congestión reaccionando de manera incorrecta.
Para evitar que el emisor sobrecargue al receptor, es necesario definir un mecanismo adicional de control de flujo.

- Si un emisor envía paquetes a un receptor más rápido que la capacidad del receptor de procesar cada paquete, se satura de paquetes el búfer del recptor hasta que este ya no puede almacenar más paquetes que le llegan y comienza a perder paquetes.
  ![[Pasted image 20260318104455.png]]
  
  Para evitar esto, se debe hacer uso de la retroalimentación al emisor. Osea, el receptor le indica al emisor cuándo y cuánto puede enviar
[[Control de flujo (CT)]]

## Comunicación confiable
EL control de flujo evita que el emisor envpíe datos más rápido de lo que el receptor puede procesar, protegiendo al host de desbordes y pérdidas locales. Pero aún cuando el receptor no se satura, eso no garantiza que la comunicación sea correcta: la red puede perder, duplicar o desordenar paquetes, y los procesos necesitan mecanismos para detectar y corregir esos problemas. Por eso, además del control del flujo, es necesario un proceso que asegure una comunicación confiable entre procesos, permitiendo reconstruir los datos completos y en el orden adecuado.

- Los paquetes pueden perderse por varias razones: 
  - Por congestión en los enrutadores cuando las colas se llenan;
  - Porque el emiso envía más rápido que lo que el receptor puede procesar y este descarta paquetes
  - por errores físicos o daños en los paquetes durante su transmisión 
- Para manejar la pérdida de paquetes:
  - Los paquetes recibidos son confirmados por el receptor.
  - El emisor detecta que paquetes faltan, porqué no recibió sus confirmaciones de recepción durante un cierto tiempo. Ese tiempo se mide con un temporizador asociado a cada paquete.
  - Si un paquete no es confirmado, el emisor lo retransmite
