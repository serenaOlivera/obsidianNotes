Este bloque responde a ¿Cómo logramos que varias máquinas compartan un medio y se comuniquen de forma confiable?

## Conexiones punto a punto
Hay conexión punto a punto cuando, dos dispositivos  están conectados directamente entre sí, sin intermediarios ni compartición del medio con otros usuarios. Por ejemplo, dos máquinas conectadas por un cable.

Si tenemos n máquinas y las queremos conectar entre si, usando conexiones punto a punto usando cables, necesitaríamos n*(n-1)/2 cables y cada máquina necesitaría n puertos para enchufar esos cables. 

Claramente no es escalable.

## Canales de difusión 
¿Cómo crear un medio compartido? 
- Si lo queremos hacer físicamente usando cables, podemos usar un Hub (como en los cibers)![[Pasted image 20260311190155.png|514]]
- Si lo queremos hacer inalámbricamente, por ondas de radio, podemos usar WiFi, o redes móviles ad hoc.

A los medios compartidos se los llama canales de difusión, sin embargo, usar un medio compartido trae nuevos problemas como: si varias máquinas transmiten al mismo tiempo, sus señales se superponen y se destruyen, a eso llamamos **colisión**

Tenemos dos soluciones propuestas para las colisiones:
1. Si dos máquinas colisionan entonces esperan un tiempo aleatorio (diferente) cada una y pasado ese tiempo retransmiten (usada en Ethernet).
2. Una máquina coordina el orden de transmisión de las demás máquinas (usada en WiFi).

## Control de errores
Las colisiones son solo una de las formas en que un mesaje puede dañarse. Incluso si evitamos o controlamos las colisiones, el medio físico sigue introduciendo ruido, interferencia y atenuación. Por eso necesitamos mecanismos que permitan detectar si un mensaje llegó con errores.

Supongamos que mandamos un mensaje entre dos computadoras, y pasa por 10 computadoras antes de llegar a destino, y en el medio el mensaje es alterado. Para poder detectar que es un mensaje errado, ambos emisor y receptor acuerdan usar una función f que aplicada al mensaje da una secuencia de bits. Si el mensaje a mandar es M, se envía entonces M ++ f(M)

Si M fue alterado a M', el receptor va a recibir M'++f(M), el receptor va a calcular f(M') y va a descubrir que no concuerda con f(M), entonces se va a dar cuenta que el mensaje recibido contiene error.

La alteración puede ser causada por ruido

## Comunicación confiable
Saber que un mensaje llegó dañado es solo la mitad del trabajo. La otra mitad es lograr que el mensaje correcto llegue finalmente al destino. Ese es el objetivo de la **comunicación confiable**.

Supongamos que un mensaje se recibió con error;  ideas de cómo hacer para recibirlo de nuevo :
1. El receptor envía un mensaje NAK (Negative Acknowledgement) con el número de mensaje que se recibió mal. Luego, el emisor lo manda de nuevo. El receptor manda ACK con número de mensaje que recibió bien.
2. El emisor manda mensaje y dispara un temporizador; si el temporizador del mensaje expira, significa que el mensaje llegó mal o se perdió y hay que reenviarlo.

### Fragmentación de mensajes
Si el mensaje dañado es muy largo, no conviene retransmitirlo todo, es re costoso.
Debemos dividir el mensaje en tramas, en lugar de mandar el mensaje entero se mandan tramas. Si una trama llega dañada, entonces se retransmite.
Para esto, es necesario la numeración de tramas y reensamblado (en ese orden), confirmación de tramas buenas recibidas, y retransmisión de tramas dañadas.

## Repetidores 
Debemos resolver como hacer que la señal llegue lo suficientemente lejos como para que los mecanismos para tratar con mensajes dañados tengan sentido. 

Para extender el alcance de la red usamos repetidores. Un repetidor es un dispostivo que recibe, amplifica (regenera) y retransmite señales en ambas direcciones. Los repetidores introducen un retardo.
Para permitir redes mayores que un segmento, conectar multiples cables mediante repetidores.
![[Pasted image 20260311194709.png]]

## Conmutadores
Cuanto más grande es el medio compartido, más colisiones hay. Para que la red escale sin que las colisiones exploten, necesitamos algo más inteligente que un repetidor.

Usando repetidores, todos los segmentos de cable forman un único canal. Entonces la probabilidad de colisiones aumenta. Usamos conmutadores (switches) 

Tenemos varios dominios de colisiones y aumentamos mucho la velocidad para mandar de una máquina de un dominio de colisiones a una máquina en otro dominio de colisiones
![[Pasted image 20260311195234.png]]

Hay dos opciones: 
- Cada tarjeta es un dominio de colisiones (todas las máquinas conectadas en la tarjeta están conectadas directamente entre sí)
- Cada puerto es un dominio de colisiones


## Redes de área local (LAN)
Repetidores extienden el alcance. Conmutadores segmentan el tráfico. Los canales de difusión permiten compartir el medio . La combinación de estos elementos define una red organizada dentro de un área limitada: una red de área local (LAN).

Las redes de área local suelen cubrir el área de una casa, edificio o hasta un campus. 
Ejemplos de redes de área local:
- Un canal de difusión con computadoras conectadas.
- Un conjunto de canales de difusión interconectados usando repetidores.
- Un conjunto de canales de difusión interconectados usando conmutadores .
- ![[Pasted image 20260311200203.png]]
- ![[Pasted image 20260311200236.png]]
- ![[Pasted image 20260311200308.png]]

