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

## [[Retroceso-N]]

## Repetición Selectiva
#### ¿En qué situaciones usar Repetición Selectiva?
- La latencia es alta (como GBN (Go Back N))
- Además la tasa de errores/pérdida de paquetes es significativa
- Los paquetes pueden demorarse y llegar fuera de orden
El enfoque de repetición selectiva, está en un receptor más complejo: acepta paquetes fuera de orden, usa buffer, envía ACK individuales.
**Tradeoff:** código más complejo, pero mucho más eficiente con alta tasa de errores.

Repetición selectiva guarda en buffer los paquetes que llegan después del paquete perdido. Sólo se retransmite el paquete perdido.

### Estrategia del receptor (buffer)
Los paquetes correctos que llegan después de un paquete dañado E, se almacenan en un buffer (no se descartan).
Cuando el paquete E finalmente llega correcto, el receptor entrega a la capa de aplicación, en orden, tanto E como todos los paquetes consecutivos almacenados en el buffer.

### Retransmisiones y NAK
Mecanismo básico de retransmisión:
- El temporizador del paquete E expira, el emisor lo retransmite.
- Cada paquete tiene su propio temporizador (a diferencia de GBN que usa uno solo). Es más complejo.
Mejora: (uso de NAK)
	El receptor detecta que falta un paquete y envía un NAK al emisor. El emisor retransmite antes de que expire el temporizador (mejor rendimiento).

Entonces el receptor:
- Confirma individualmente cada paquete recibido correctamente (ACK por paquete)
- Almacena en buffer los paquetes fuera de orden hasta poder entregarlos en secuencia a la aplicación.
El emisor:
- Solo retransmite paquetes cuyo ACK no llegó o que recibieron un NAK (confirmación negativa)
- Mantiene un temporizador individual para cada paquete no confirmado (a diferencia de GBN que usa uno solo)
### Ventana del Emisor
Estructura de la ventana emisora: contiene *N* N° de secuencia consecutivos. Limita la cantidad de paquetes no confirmados en tránsito.

Tipos de paquetes dentro de la ventana del emisor:
- Enviados y confirmados: aún en ventana porque antes hay paquetes sin confirmar (no puede avanzar la ventana)
- Enviados y NO confirmados: en tránsito, esperando ACK
- Listos para enviar: en buffer, esperando turno 
A diferencia de GBN, aquí pueden haber "huecos" de paquetes confirmados entre no confirmados.

### Ventana corrediza del receptor
El receptor necesita almacenar paquetes que llegan fuera de orden mientras espera el paquete faltante. Para representar qué paquetes puede almacenar el receptor, usamos una ventana corrediza (sliding window):
- Un intervalo de N° de secuencia dentro del espacio total.
- Define qué paquetes el receptor está dispuesto a aceptar y guardar en buffer
- Se desliza hacia adelante a meida que se entregan paquetes a la aplicación
### Tipos de paquetes en ventana receptora

- Esperados y no recibidos (los que faltan)
- Recibidos y fuera de orden (almacenados en buffer, esperando al faltante)
- aceptables pero no llegados (dentro de la ventana, todavía en tránsito)
Un paquete en buffer se entrega sólo cuando todos los que le preceden ya fueron entregados a la capa de aplicación.
![[Pasted image 20260430180108.png]]

### Recepción de paquetes en el receptor
La ventana emisora comienza en tamaño 0 y crece hasta MAX_SEQ. El receptor tiene un buffer dedicado para cada N° de secuencia en su ventana.

¿Que ocurre cuando llega un paquete?
1. Se verifica si su N° de secuencia car dentro de la ventana receptora 
2. SI está dentro y no fue recibido aún -> se acepta y almacena en el buffer correspondiente
3. Si está fuera de la ventana -> se descarta (puede ser un duplicado)
![[Pasted image 20260430180509.png]]
### Ejemplo:
![[Pasted image 20260430180755.png]]

### Tamaño máximo de ventana receptora
```
ventana receptora = (MAX_SEQ + 1)/2
```
¿Porqué?
	Con ventanas más grandes, el receptor no puede distinguir entre paquetes nuevos y retransmisiones de la ronda anterior. La mitad del espacio de secuencia, garantiza que las ventanas de emisor y receptor nunca se solapan. Con tamaños mayores de ventana, el protocolo no funciona correctamente

### Piggybacking
Resuelve el problema de transmitir datos eficientemente en ambas direcciones.
Cuando llega un segmento S con datos, el receptor espera a que la aplicación le pase el siguiente paquete P para enviar. El ACK de S se anexa a P usando el campo ACK del encabezado del segmento de salida.
![[Pasted image 20260430190948.png]]

En comunicación bidireccional, en lugar de enviar ACKs en paquetes separados, se puede superponer el ACK dentro de un paquete de datos que viaja en dirección contraria.

**Cómo funciona:**
	La CT espera a que haya un paquete de datos para enviar en la dirección de regreso. El ACK se incluye (va a caballito) dentro de ese paquete de datos
	Ventaja: reduce el tráfico en la red (menos paquetes de ACK independientes).
	
Problema con piggybacking: ¿qué pasa si no hay tráfico de regreso?
El ACK se retrasa indefinidamente y el emisor cree que el paquete se
perdió.
Solución: temporizador auxiliar (start_ack_timer)
– Al recibir un paquete en secuencia, se arranca un temporizador
auxiliar.
– Si aparece tráfico de regreso antes del timeout → el ACK va a caballito
(piggybacking).
– Si expira el temporizador sin tráfico → se envía un ACK independiente.

El timer auxiliar debe ser corto para asegurarse que la ack de un paquete correctamente recibido llegue antes que el emisor termine su temporización y retransmita el paquete.

## [[Ejercicios (CT)]] 
(transferencia de datos confiable)