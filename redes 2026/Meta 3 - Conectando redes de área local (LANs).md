De la comunicación local  pasamos a la necesidad de unir múltiples redes y decidir por donde deben viajar los mensajes. Para lograrlo aparecen los enrutadores, las tablas de reenvío, las colas, el almacenamiento y reenvío, y los algoritmos de enrutamiento.

Este bloque responde a: ¿Cómo conectamos múltiples LAN para formar redes más grandes que funcionen de manera eficiente?

## Enrutadores
Los enrutadores son nodos intermedios para conectar varias LAN.

- Para saber por qué línea de salida mandar un mensaje a una de las máquinas debemos definir una tabla para ello(tabla de reenvío).  
  ![[Pasted image 20260312162859.png]]
- Para que el  enrutador pueda manejar recibir tantos mensajes que se van acumulando para ser enviados por una línea de salida, se usa una cola de mensajes en la línea de salida.
## Almacenamiento y reenvío
Necesitamos entender cuánto tarda el enrutador para mandar mensajes, por eso descomponemos la demora total en sus partes constitutivas.

¿Cómo hace el enrutador para mandar un mensaje de A a F??
1. El enrutador consulta la tabla de reenvío y descubre que hay que usar la línea l2.
2. Encola mensaje en cola de línea l2
3. Cuando el mensaje llega a la cabeza de la cola el enrutador lo reenvía
A esto se le llama almacenamiento y reenvío

### ¿Cuánto demora el almacenamiento y reenvío?
![[Pasted image 20260312164555.png]]


## Redes de área amplia
Si intentamos conectar cientos o miles de LAN a un solo enrutador, simplemente colapsa. Ahí es donde necesitamos pasar a una estructura más grande: las redes de área amplia (wide area network- WAN).
Una WAN puede cubrir desde un país hasta un continente entero.

- Si hay demasiadas LAN para conectar en un sólo enrutador, usamos más de uno y conectamos los enrutadores entre sí mediante cables (conexiones punto a punto)

![[Pasted image 20260312165247.png]]
Las tablas de reenvío en su conjunto determinan la ruta que se usa.

## Algoritmos de enrutamiento
Al pasar de unas pocas LAN interconectadas a redes de área amplia, la escala cambia por completo. Tenemos decenas o cientos de enrutadoes distribuídos geográficamente, cada uno con su propia tabla de reenvío y su propio tráfico.

En este escenario, elegir por dónde enviar un paquete deja de ser trivial, ningún enrutador puede tener una visión completa y perfecta del estado global. Por eso, en las WAN aparece un nuevo desafío arquitectónico: necesitamos mecanismos sistemáticos para calcular, actualizar y coordinar rutas.

Hay rutas mejores que otras para ir a un destino, la mejor ruta entre dos dispositivos es la ruta más corta entre esos dispositivos (en el sentido de matemática discreta). Para llegar a esto, debemos modificar las tablas de reenvío con ese propósito. Los algoritmos que modifican esas tablas, se llaman algoritmos de enrutamiento. 

## Ejemplos de redes de área amplia 
Las WAN que usamos todos los días, como las redes de fibra hasta el hogar o las redes telefónicas, son ejemplos donde estos mecanismos se aplican a gran escala, con miles de enrutadores y múltiples tecnológicas físicas.

- Sistema de fibra a la casa: 
  - Divisor óptico para subdividir un cable de fibra óptica en varios (cada uno va a una casa), usualmente menos de 100.
  - Cada casa tiene un terminador de red óptica para convertir entre señales ópticas y eléctricas.
  - Tasas de transferencia de 100 mbps o 300 mbps
  - ![[Pasted image 20260314175940.png]]
-  Sistema telefónico fijo (p. ej: DSL):
  - Cada domicilio está conectado or un cable de cobre a una End office (oficina central)
  - Toda oficina central está conectada a una Toll office
  - Toll offices con usadas para reenvío de mensasjes y están unidas por cables (de fibra óptica)
  - ![[Pasted image 20260314180126.png]]