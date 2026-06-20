La capa de transporte de internet, tiene dos protocolos:
- TCP (Transmission Control Protocol):
	  Divide el flujo de bytes entrantes en mensajes discretos y pasa cada uno de ellos a la capa de interred. TCP proporciona entrega confiable y en orden de los mensajes. Esto significa que un flujo de bytes que se origina en una máquina se entregue sin errores en otra máquina en la interred.
	  El reensamblado de los mensajes recibidos se efectúa en el receptor. Para la entrega confiable de mensajes:
	  - Los mensajes recibidos deben ser confirmados
	  - Deben detectarse paquetes duplicados
	  - Los mensajes perdidos deben ser reenviados automáticamente.
	 TCP también manjea el control de flujo y el control de congesitón 
	 
	 Para cumplir con lo que promete, TCP necesita mantener estado. Osea que ambos extremos deben acordar qué números de secuencia usarán, que ambos están vivos y listos, que ambos pueden recibir datos. 
	 El estado ocupa recursos como búferes, temporizadores, entradas de tablas de conexión, ventanas de congestión. Por lo tanto, n TCP necesita crear y destruir esa información de estado.
	 
	 Entonces TCP necesita crear una conexión porque sus garantías requieren que ambos extremos mantengan y sincronicen un estado compartido. Ese estado debe liberarse (a esto se lo llama liberación de conexión), sino el servidor quedaría con informaciones innecesarias.
	 
	 Entonces la comunicación entre dos procesos usando TCP cumple el siguiente orden:
	 - Establecimiento de la conexión: suelen ser 3 mensajes para crear información de estado. 
	 - Transferencia de datos: el emisor envía segmentos y el receptor los confirma con mensajes de confirmación de recepción. Aquí se mantiene actualizada la información de estado. 
	 - Liberación de conexión: suelen ser 4 mensajes para liberar información de estado.
	[[TCP]]
- UDP (User Datagram Protocol):
	  UDP proporciona entrega de mensajes no confiable y desordenada. Esto significa que, un mensaje puede netregarse con errores, o no entregarse, o varios mensajes pueden entregarse en forma desordenada.
	  UDP no tiene:
	  1. Uso de confirmaciones de recepción para los mensajes 
	  2. Control de flujo, control de congestión, retransmisiones cuando se recibe mensaje erróneo.
	 UDP se usa para los siguientes tipos de aplicaciones:
	 - Aplicaciones que no usan el control de flujo ni la secuenciación de mensjes
	 - Aplicaciones que involucran consultas de solicitud-respuesta
	 - Aplicaciones de transmisión de voz y video


## IP
Para distinguir entre las diferentes máquinas que tienen una conexión a internet, se usan direcciones IP.
- Direcciones IPv4(de 32 bits): son  números entre 0 y 255 separados por '.'. Por ejemplo: 200.45.191.35
- Direcciones IPv6(de 128 bits)
Se envían paquetes IP, que tienen su propio formato, y para hacer el enrutamiento hay protocolos de enrutamiento: se usan OSPF (Open Shortest Path First) y BGP (Border Gateaway Protocol) para enrutamiento de paquetes.