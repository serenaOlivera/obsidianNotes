#### ¿Cúando usar parada y espera?
- La latencia de la red es baja 
- EL RTT (Round Trip Time o tiempo de ida y vuelta) es bajo comparado con el tiempo de transmitir un paquete.
- Consecuencia: el ACK llega antes de que se termine de preparar el siguiente paquete, entonces sólo se puede tener un paquete "en vuelo" a la vez.
#### Funcionamiento
Parada y Espera: 
- Envía un paquete y se detiene hasta recibir confirmación 
- Si llega ACK, envía el siguiente paquete
- Si expira el temporizador, retransmite el mismo paquete 

Es el protocolo más simple, ideal cuando RTT es bajo.


#### Supuestos del protocolo:
El canal puede perder paquetes de datos y ACKs

Comportamiento del emisor: 
1. Envía paquete P y para (no envía más hasta recibir respuesta)
2. Espera un tiempo razonable (timeout)
3. Si llega ACK, entonces envía siguiente paquete (volver a 1)
4. Si expira timeout, entonces retransmite P (volver a 2)
Si el ACK llega tarde, se retransmite un duplicado, entonces el receptor lo detecta por el número de secuencia y lo descarta 

Ejemplos:
![[Pasted image 20260409165514.png]]
![[Pasted image 20260409165536.png]]

Para evaluar si parada y espera es eficiente, haremos un análisis del mejor caso con simplificaciones. Si aún en el mejor caso el rendimiento es bajo, entonces el protocolo no es adecuado.

variables del análisis de Parada y Espera
L = longitud del segmento (bits)
T = tasa de transmisión (bits/seg)
D = demora de propagación
RTT = ida y vuelta = 2*D

¿Cúanto tarda en enviar un paquete? tiempo de transmisión = L/T
¿Cuánto del RT T se calcula con D? 2*D

$$U_{sender} = \frac{L/R}{RTT + L/R}$$
Este valor es entre 0 y 1 (se puede expresar en %)

Ejemplo de desempeño:
![[Pasted image 20260409170848.png]]