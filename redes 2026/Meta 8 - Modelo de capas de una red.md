Este bloque responde a ¿Cómo oranizamos toda la complejidad de una red en una arquitectura clara, modular y escalable?
![[Pasted image 20260318120923.png]]
![[Pasted image 20260318120948.png]]![[Pasted image 20260318121021.png]]
[[TCP-IP]]
Interfaces entre capas: operaciones y servicios primitivos ofrecidos por una capa a capa superior.

Significado de una capa:
- Una capa n se piensa como una conversación entre la capa n de una máquina con la capa n de otra máquina
- para especificar cómo es esta conversación se definen protocolos.
Protocolo de capa n : reglas y convenciones usadas en la conversación entre la capa n de una máquina y la capa n de otra máquina
arquitectura de red: conjunto de capas y protocolos 

![[Pasted image 20260318121351.png]]
**En la máquina receptora el mensaje pasa hacia arriba de capa en capa, perdiendo los encabezados conforme avanza.**

Procesos de aplicación (capa 5 o capa de aplicación):
	Produce un mensaje y lo pasa a la capa 4 para su transmisión. Por ejemplo: browser, e-mail, chat, ftp, etc. 
Capa de transporte (capa 4):
	Pone un encabezado en el mensaje para identificarlo y pasa el resultado a la capa 3.
	 El encabezado contiene números de secuencia para que la capa 4 en la máquina de destino entregue los mensajes en el orden correcto.
Capa de red (Capa 3):
	 Hay limitaciones en el tamaño de los mensajes de capa 3. Divide en paquetes los mensajes que llegan. A cada paquete se le coloca un encabezado, decide cuál de las líneas que salen usar ( cuando la máquina es un enrutador). Pasa los paquetes a la capa 2.
Capa de enlace de datos (Capa 2):
	Agrega un encabezado y un terminador, a cada pieza. Pasa la unidad resultante a la capa 1 para su transmisión.

![[Pasted image 20260318122217.png]]