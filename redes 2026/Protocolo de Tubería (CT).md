Situación: la latencia de la red es alta.
El RTT es mucho mayor que el tiempo de transmitir un paquete, entonces se pueden enviar múltiples paquetes antes de recibir el primer ACK

El protocolo de tubería, permite enviar múltiples paquetes sin esperar confirmación de cada uno. Mantiene el "tubo" lleno, aprovecha mejor el ancho de banda disponible . Necesita: números de secuencia más grandes, buffers y reglas de retransmisión más complejas.

| Retroceso-N (Go-Back-N)                                          | Repetición Selectiva                                              |     |
| :--------------------------------------------------------------- | :---------------------------------------------------------------- | --- |
| Ventana de N paquetes sin confirmar                              | Ventana de N paquetes sin confirmar                               |     |
| Si se pierde un paquete: retransmite ese y todos los siguientes. | Si se pierde un paquete: retransmite sólo ese paquete.            |     |
| Receptor: sólo acepta paquetes en orden (ACK acumulativo)        | Receptor: acepta paquetes fuera de orden (buffer +ACK individual) |     |
| Más simple, pero puede desperdiciar ancho de banda.              | Más eficiente, pero más complejo (buffer en recptor)              |     |

Tubería: el emisor puede enviar múltiples paquetes al vuelo a ser confirmado. El rango de números de secuencia debe incrementarse usando palabras de más de un bit. Hay que usar búferes en el emisor.

![[Pasted image 20260409173920.png]]

La Entidad de Transporte (ET) emisora debe manejar búferes para los mensajes. Esto es necesario porque: puede hacer falta retransmitirlos.
El emisor almacena en búfer todos los segmentos hasta que se confirma su recepción.

### **¿Cuál protocolo elegir?**
Ambos protocolos usan pipelining, pero difieren en en como manejan los paquetes perdidos.
1. Protocolo Retroceso-N (Go-Back-N):
	   Receptor simple: descarta paquetes fuera de orden, ideal cuando la tasa de errores es baja.
2. Protocolo de Repetición Selectiva:
	   Receptor más complejo: guarda paquetes fuera de orden en buffer. Mejor cuando la tasa de errores es significativa.
La elección depende de las condiciones de la red. 

## Retroceso-N
