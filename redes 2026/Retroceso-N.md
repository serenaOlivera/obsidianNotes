#### ¿En qué situaciones se usa Retroceso-N?
- La latencia es grande (RTT alto -> se justifica el pipelining)
- La proporción de errores o pérdida de paquetes es muy baja
- Rara vez se demoran los paquetes
Razonamiento: Si los errores son raros, el receptor puede ser más simple y eficiente. No necesita buffer para reordenar paquetes, sólo descarta los que llegan fuera de orden. El costo de retransmitir todo es bajo porque rara vez ocurre. Si los errores son frecuentes, la repetición selectiva será más eficiente.

#### ¿Qué pasa si se pierde un paquete?
Tenemos una restricción clave: la CT receptora debe entregar datos en orden a la capa de aplicación. Retroceso N, descarta los paquetes correctos que llegaron despues del perdido. Entonces:
- El receptor descarta todos los paquetes posteriores al perdido.
- No envía ACK para los paquetes descartados
- El emisor no recibe ACK -> expira el temporizador.
- El emisor "retrocede" y retransmite todos los paquetes desde el perdido en adelante.
### Comportamiento del receptor
El receptor usa ACK acumulativo: confirma hasta el mayor N° de secuencia recibido en orden. Al recibir paquete n:
- Caso 1 n está en orden y correcto: Envía ACK (n) y entrega los datos del paquete n a la capa superior.
- Caso 2 n está fuera de orden, dañado o duplicado. Descarta paquete n y reenvía ACK del último paquete recibido en orden
**El receptor no necesita buffer**

### Comportamiento del emisor
El emisor mantiene un único temporizador para el paquete más antiguo no confirmado. Si expira el temporizador, retransmite todos los paquetes no confirmados (desde el más antiguo). Si llega un ACK nuevo:
- Si quedan paquuetes sin confirmar, reinicia el temporizador
- Si todos están confirmados, detiene el temporizador

Supuestos del emisor:
- Todos los búferes son del mismo tamaño (un paquete por búfer)
- La cantidad de búferes es fija - calculada para llenar el "tubo" durante un RTT.

**ventana del emisor:**  Es el conjunto de N° de secuencia asignados a esos búferes. Define cuántos paquetes puede tener 'en vuelo' simultáneamente. Se 'desliza' hacia adelante cuando llegan ACKs confirmando paquetes.

La ventana permite hasta N paquetes consecutivos sin confirmar. Ventana emisora = tramas enviadas sin ack positivo o tramas listas para ser enviadas![[Pasted image 20260428144057.png]]
timeout (n): retransmite paquete n y todos los paquetes de mayor N° de secuencia en la ventana.

### ACK acumulatico y expectedSeqnum
El ACK lleva el N° de secuencia más alto recibido en orden consecutivo. Esto se llama ACK acumulativo: confirma todo hasta ese punto

¿Qué pasa si se pierde un paquete intermedio?
	Los paquetes siguientes generan ACKs duplicados (repiten el último ACK en orden)

**expectedSeqNum=** N° de secuencia más chico que aún no llegó.
![[Pasted image 20260428145231.png]]

### Tamaño máximo de la ventana emisora
El tamaño máximo de la ventana emisora es MAX_SEQ (no MAX_SEQ+1). Si fuera igual al espacio de secuencia completo, el receptor no podrá disitnguir paquetes nuevos de retransmisiones.

El tamaño de la ventana emisora no puede superar MAX_SEQ cuando
hay MAX_SEQ + 1 números de secuencia. Esto garantiza que nunca se reciclen N° de secuencia mientras haya paquetes sin confirmar → elimina la ambigüedad.

### Problema principal de Retroceso N
- El uso ineficiente del canal cuando hay segmentos perdidos o demorados.
- Un solo paquete perdido obliga a retransmitir todos los siguientes, aunque hayan llegado bien.
- En redes con alta tasa de pérdida, esto desperdicia mucho ancho de banda.