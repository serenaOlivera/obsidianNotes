Idea rectora
En WiFi, la dificultad no es solo “compartir un canal”. También pasa que:
- no todos escuchan lo mismo;
- una estación normalmente no puede transmitir y recibir a la vez;
- los errores y la interferencia son más frecuentes que en cable;
- la tasa física no coincide con la tasa útil.
Por eso 802.11 usa CSMA/CA: intenta evitar colisiones y confirmar recepción, en lugar de detectarlas mientras transmite.


## 1. Redes inalámbricas
### Dos organizaciones posibles
**Red ad hoc**
	No hay estación base. Los nodos se comunican directamente con otros dentro de alcance. En una red ad hoc:
	- cada nodo tiene alcance limitado;
	- no hay AP coordinando;
	- los nodos compiten por el medio;
	- si hace falta llegar más lejos, se necesitan rutas multi-salto;
	- el modo distribuido es natural.
	DCF (Distributed Coordination Function) está pensado como mecanismo distribuido: todos siguen reglas comunes para competir por el canal.

**Red con infraestructura**
Los hosts se asocian a un access point (AP), que conecta con la red cableada o
con otros AP. En infraestructura:
- cada host se asocia a un AP;
- el AP conecta la celda inalámbrica con un sistema de distribución;
- los AP vecinos idealmente usan canales no conflictivos;
- el AP puede coordinar ciertos períodos de transmisión;
- la movilidad requiere asociación y reasociación.

### BSS, ESS y sistema de distribución
BSS: Basic Service Set.
ESS: Extended Service Set. 
STA: estación. 
AP: access point.

![[Pasted image 20260529124001.png]]
**BSS:** una celda 802.11. En infraestructura está formada por un AP y las estaciones asociadas a ese AP. Comparten un medio inalámbrico y compiten por ese canal.
**ESS**: varios BSS unidos por un sistema de distribución (DS), normalmente una
red cableada con switches. Hacia el usuario puede verse como una misma
WLAN, por ejemplo con el mismo SSID.

### Vocabulario mínimo

| Término | Significado                                          |
| :------ | ---------------------------------------------------- |
| STA     | estación inalámbrica                                 |
| AP      | Punto de acceso                                      |
| BSS     | conjunto básico de servicio                          |
| ESS     | varios BSS conectados por un sistema de distribución |
| DS      | sistema de distribución                              |
| portal  | integración hacia una LAN no 802.11                  |

### Asociación
Antes de enviar o recibir datos de capa de red, una estación debe asociarse con un AP. Servicios relacionados:
**asociación:** establece la relación inicial;
**reasociación**: transfiere la estación a otro AP;
**desasociación:** finaliza la relación.
Esto aparece en teoría como movilidad, handoff y elección de AP.


### Escaneo activo
En escaneo activo, la estación envía tramas de prueba y los AP en alcance responden.Luego la estación elige AP y pide asociación.
![[Pasted image 20260529124334.png]]



### Escaneo pasivo
En escaneo pasivo, los AP emiten beacons periódicos. La estación escucha, compara información y decide si asociarse o reasociarse.
![[Pasted image 20260529124353.png]]


## 2. ¿Por qué WiFi no usa CSMA/CD?

### La idea de CSMA/CD no alcanza
CSMA/CD requiere que el transmisor pueda escuchar el medio mientras transmite. En WiFi esto es difícil porque:
- la señal propia transmitida es muchísimo más fuerte que una señal recibida;
- el circuito receptor se satura;
- las estaciones pueden tener visiones distintas del canal;
- dos transmisores que no se escuchan pueden interferir en un receptor común.
Hay hardware para separar transmisión y recepción, pero no elimina el problema general de WiFi: una cosa es transmitir y recibir en frecuencias distintas; otra mucho más difícil es detectar una colisión débil en el mismo canal mientras estoy transmitiendo.

### ¿Y los duplexores o diplexores?
**Diplexor:** combina o separa bandas/frecuencias distintas sobre una misma antena o cable. 
**Duplexor:** permite transmitir y recibir a la vez cuando el sistema usa frecuencias
separadas, como en FDD: duplexación por división de frecuencia.

Se usan cuando el costo y el tamaño se justifican: redes celulares FDD, estaciones base, repetidoras, enlaces punto a punto, satélite y algunos sistemas de radio especializados.

En 802.11 típico no alcanza con poner un filtro: las estaciones comparten el mismo canal y CSMA/CD debería detectar interferencia en ese canal durante la propia transmisión. Además, el problema de estación oculta (discutido luego) sigue existiendo: la colisión puede ocurrir en el receptor aunque el transmisor no la perciba.

Consecuencia
En Ethernet cableada clásica: escucho mientras transmito -> detecto colisión
En WiFi: escucho antes, espero, uso ACK -> intento evitar colisión
Por eso hablamos de **CSMA/CA: Collision Avoidance.**

### Detección de portadora física y virtual
802.11 combina:
**detección física:** medir si el medio parece ocupado;
**detección virtual:** NAV, un temporizador que dice “alguien reservó el canal”;
**ACKs:** confirmar que el receptor recibió;
**backoff:** separar intentos que podrían colisionar.

### Estación oculta
Situación típica:
![[Pasted image 20260529125820.png]]Si C transmite a B y A no escucha a C, A puede creer que el canal está libre y transmitir también a B. La colisión ocurre en el receptor B.

Cómo reconocer estación oculta
Buscá esta estructura:
- dos posibles transmisores no se escuchan entre sí;
- ambos pueden interferir en el mismo receptor;
- el problema se descubre mirando el alcance de recepción, no solo quién transmite.
>[!tip] Pregunta guía: “¿el transmisor que decide enviar puede escuchar al otro  transmisor que ya estaba usando el receptor?”


### Estación expuesta
Situación típica:
![[Pasted image 20260529125914.png]]C se abstiene de transmitir porque escucha a B, aunque C -> D podría haber sido seguro.

Cómo reconocer estación expuesta
Buscá esta estructura:
- una estación escucha una transmisión cercana;
- por escucharla, se calla;
- pero su receptor estaría suficientemente lejos del receptor actual;
- la transmisión simultánea podría no causar colisión.
La estación expuesta reduce reutilización espacial: se desperdicia una oportunidad de transmitir.


### Oculta vs expuesta

| Problema | Qué sale mal                                                                        | Efecto                      |
| :------- | :---------------------------------------------------------------------------------- | --------------------------- |
| Oculta   | alguien transmite porque no escucha a otro transmisor                               | colisión en el receptor     |
| Expuesta | alguien no transmite porque escucha una transmisión que no le impediría comunicarse | subutilización del<br>canal |

La oculta causa daño directo; la expuesta causa prudencia excesiva

## 3. DCF: Distributed Coordination Function
### DCF en una frase
DCF es el nodo distribuido de 802.11:
- todos los nodos siguen el mismo protocolo;
- se usa contención por el canal;
- se espera DIFS (DCF Interframe Space) antes de iniciar un diálogo;
- se usa backoff aleatorio;
- opcionalmente se usa RTS/CTS (Request-to-Send/Clear-to-Send);
- los ACKs van después de SIFS (Short Interframe Space).

En DCF, contención quiere decir que las estaciones compiten por iniciar el próximo diálogo. Esperan DIFS, aplican backoff aleatorio y transmiten cuando su contador llega a cero. Si dos llegan juntas, puede haber colisión.


### Secuencia RTS/CTS/DATA/ACK
La conversación básica:
RTS -> CTS -> DATA -> ACK
![[Pasted image 20260529135346.png]]


### Qué hace cada trama

| Trama | Quién la envía | Para qué sirve                         |
| :---- | :------------- | -------------------------------------- |
| RTS   | emisor         | solicita reservar el canal             |
| CTS   | receptor       | concede y avisa a vecinos del receptor |
| DATA  | emisor         | transporta carga útil                  |
| ACK   | receptor       | confirma recepción correcta            |

### NAV
NAV significa Network Allocation Vector.
Es un temporizador local:
NAV > 0 -> me quedo callado
Los nodos cercanos al emisor o receptor escuchan RTS/CTS y estiman cuánto durará el intercambio.

### DCF con nodos vecinos
![[Pasted image 20260529140158.png]]
El RTS puede ser escuchado por vecinos del emisor. El CTS puede ser escuchado por vecinos del receptor. Ambos ayudan a reservar el medio.

### RTS/CTS y estación oculta
RTS/CTS ayuda especialmente con estación oculta:
- el nodo oculto quizá no escucha al emisor;
- pero puede escuchar el CTS del receptor;
- al escuchar CTS, configura NAV;
- evita transmitir durante el intercambio.
Ayuda, pero no vuelve imposible toda colisión. Los RTS mismos pueden colisionar.

### RTS/CTS y estación expuesta
RTS/CTS no resuelve necesariamente estación expuesta.
Una estación puede escuchar señales de reserva y callarse aunque su transmisión hacia
otro receptor fuera segura.
La estación oculta se trata de evitar colisión; la expuesta se trata de no desperdiciar
reutilización espacial

### Colisiones en DCF
Dos nodos pueden:
- detectar el canal libre;
- elegir backoffs que terminan al mismo tiempo;
- enviar RTS simultáneamente;
- hacer que los RTS colisionen.
Si no llega CTS, el emisor asume falla y reintenta con backoff.

### Backoff en WiFi
El backoff es una cuenta regresiva aleatoria en ranuras temporales (slots), usada para separar estaciones que quieren transmitir después de que el canal quedó libre.
```
backoff = k * SlotTime, con k elegido en [0, CW]
```
Proceso:
1. la estación espera que el medio esté libre durante DIFS;
2. elige k al azar dentro de la ventana de contención CW ;
3. resta 1 por cada slot libre;
4. si el canal se ocupa, congela el contador;
5. cuando vuelve a estar libre, espera DIFS y continúa desde el valor congelado;
6. transmite cuando el contador llega a 0.

#### Backoff: ejemplo mínimo
Una estación eligió k = 4 
![[Pasted image 20260529135528.png]]
La estación no vuelve a sortear mientras conserva el turno parcial ganado. Si la transmisión falla, aumenta la ventana de contención para reducir la probabilidad de repetir la colisión.


## 4. SIFS, PIFS y DIFS
### Por qué hay espacios entre tramas
Los espacios entre tramas dan prioridad temporal.
SIFS < PIFS < DIFS
Quien debe responder dentro de un diálogo usa SIFS (Short IFS (Interframe Space)). El AP en PCF usa PIFS (PCF IFS). Las estaciones que compiten en DCF esperan DIFS (DCF IFS).

### SIFS
(Short Interframe Space)
SIFS es el espacio más corto. Se usa para respuestas inmediatas dentro del mismo diálogo:
- CTS después de RTS;
- DATA después de CTS;
- ACK después de DATA;
- fragmentos dentro de una ráfaga.
Después de SIFS solo hay una estación que debería responder, por eso se le da
prioridad.

### DIFS
(DCF Interframe Space)
(Distributed Coordination Function Interframe Space)
DIFS lo usan estaciones que quieren empezar una nueva contienda DCF. Proceso típico:
1. medio libre;
2. esperar DIFS;
3. ejecutar o continuar backoff;
4. transmitir si el contador llega a cero.
En cálculos de tasa efectiva, si el ejercicio no da backoff, se deja simbólico o se aclara
que se ignora.

### PIFS
(PCF IFS)
(Point Coordination Function Interframe Space)
PIFS está entre SIFS y DIFS. Lo usa el AP para tener prioridad al iniciar o continuar un período PCF libre de contención.
SIFS < PIFS < DIFS
Así el AP puede tomar el canal antes que estaciones DCF que esperan DIFS.

### Valores del material original
En los ejercicios de las slides se usan:

| Intervalo | Valor |
| :-------- | :---- |
| SIFS      | 28 us |
| PIFS      | 78us  |
| DIFS      | 128us |

Estos valores pueden variar por estándar/PHY, pero en examen se usan los dados por el
enunciado (no hay que aprenderlos de memoria).

## 5. PCF: Point Coordination Function
### PCF en una frase
PCF es un modo coordinado por el AP:
- el AP toma control del medio;
- inicia un período sin contención;
- sondea estaciones con polling;
- las estaciones transmiten si son invitadas;
- se reducen o eliminan colisiones dentro del período coordinado

### Período libre de contención
![[Pasted image 20260529141945.png]]
El AP anuncia el período, fija NAV en estaciones y coordina quién transmite.

### Beacon y polling
El AP puede:
- transmitir un beacon;
- indicar duración del período libre de contención;
- enviar CF-Poll a una estación;
- recibir datos o trama nula;
- continuar con otra estación;
- terminar con CF-End.

### DCF vs PCF

| Característica    | DCF                      | PCF                             |
| :---------------- | :----------------------- | ------------------------------- |
| Control           | distribuido              | AP coordinador                  |
| Acceso            | contención               | sondeo                          |
| Colisiones        | posibles                 | evitadas dentro del período PCF |
| Topología natural | ad hoc o infraestructura | infraestructura                 |
| Intervalo clave   | DIFS                     | PIFS                            |
 

### Ejercicio conceptual típico
“Enumere ventajas de infraestructura sobre ad hoc.”
Buenas respuestas:
- acceso a red cableada/Internet mediante AP;
- administración centralizada;
- coordinación de transmisiones;
- movilidad con reasociación;
- mejor planificación de canales;
- posibilidad de QoS/polling en modos coordinados

## 6. WiFi hoy
### Qué cambió y qué no
Cambió mucho:
- tasas físicas más altas;
- MIMO, OFDMA, canales más anchos;
- 6 GHz y WiFi 6E/7;
- multi-link operation;
- mejoras de latencia, jitter y eficiencia;
- seguridad y privacidad más complejas.
No cambió lo esencial para esta unidad: el medio se comparte y el overhead importa

### 802.11be / WiFi 7
IEEE 802.11be-2024, asociado comercialmente con WiFi 7, define mejoras Extremely High Throughput. Puntos relevantes:
- al menos un modo con throughput máximo de al menos 30 Gbit/s en el SAP MAC;
- operación entre 1 y 7.250 GHz ;
- compatibilidad y coexistencia con dispositivos 802.11 previos;
- mejoras de latencia y jitter en el peor caso.

### Lo que viene: confiabilidad y nuevos usos
En proyectos posteriores aparecen líneas como:
- Ultra High Reliability;
- ambient power communication;
- sensing con WLAN;
- privacidad con direcciones MAC aleatorias o cambiantes;
- operación multi-link más sofisticada.
La capa de enlace moderna no es solo “velocidad”: también es coordinación, energía,
movilidad, privacidad, latencia y coexistencia.}

## 7. Tasa efectiva en 802.11
### Tasa física vs tasa efectiva
La tasa física dice a qué velocidad se modulan bits en el medio. La tasa efectiva pregunta:
```
bits útiles de datos / tiempo total observado
```
El denominador incluye overhead:
- RTS, CTS, ACK;
- SIFS, DIFS, PIFS;
- beacon, poll;
- backoff si el enunciado lo da;
retransmisiones si ocurren.

### Método para tasa efectiva
1. Dibujar la línea de tiempo.
2. Separar tramas de control y datos.
3. Calcular duración de cada trama: bits / tasa.
4. Sumar intervalos SIFS/DIFS/PIFS dados.
5. Definir claramente qué cuenta como datos útiles.
6. Calcular R_eff = bits_utiles / tiempo_total 
#### Cuidado con tasas distintas
En muchos ejercicios:
- RTS, CTS y ACK usan tasa de control;
- DATA usa tasa de datos;
- las tramas de control suelen ir más lento para ser más robustas;
- los intervalos entre tramas no dependen del tamaño de datos.
**Error típico:** calcular todo a la tasa de datos y olvidar SIFS/DIFS.

### Línea de tiempo modelo DCF
![[Pasted image 20260529143158.png]]
Dos conversaciones:
1. B -> D
2. E -> D
Se usan RTS/CTS/DATA/ACK y un DIFS entre diálogos.

#### Datos del ejercicio

| Dato         | Valor     |
| :----------- | --------- |
| Tasa control | 6 Mbits/S |
| Tasa datos   | 12 Mbit/s |
| RTS          | 20B       |
| CTS          | 14B       |
| ACK          | 14B       |
| DATA         | 1500B     |
| SIFS         | 28 us     |
| DIFS         | 128 us    |
No consideramos backoff porque el enunciado no lo da y asume que B gana la disputa
inicial

#### Duración de tramas
T_RTS = 20 * 8 / 6 Mbit/s = 26.7 us
T_CTS = T_ACK = 14 * 8 / 6 Mbit/s = 18.7 us
T_DATA = 1500 * 8 / 12 Mbit/s = 1000 us

#### Tiempo de un diálogo DCF
Un diálogo:
RTS + SIFS + CTS + SIFS + DATA + SIFS + ACK
Números:
26.7 + 28 + 18.7 + 28 + 1000 + 28 + 18.7 = 1148.1 us

#### Tiempo total DCF
Dos diálogos y un DIFS entre ellos:
T_total = 2 * 1148.1 + 128 = 2424.2 us
Datos útiles:
2 * 1500  * 8 = 24000 bits

#### Tasa efectiva DCF
R_eff = 24000 bits / 0.0024242 s = 9.90 Mbit/s
Aunque la tasa física de datos es 12 Mbit/s , la efectiva baja por overhead.
Cada usuario que transmitió una sola trama ve aproximadamente la mitad:
9.90 / 2 = 4.95 Mbit/s

### Línea de tiempo modelo PCF
![[Pasted image 20260529143313.png]]
PCF reemplaza RTS/CTS por beacon y polling coordinado por el AP

#### Datos extra PCF

| Dato   | Valor |
| :----- | ----- |
| beacon | 100B  |
| Poll   | 20B   |
| PIFS   | 78us  |
Se mantienen:
- tasa control 6 Mbit/s ;
- tasa datos 12 Mbit/s ;
- DATA 1500 B ;
- ACK 14 B ;
- SIFS 28 us 

#### Duración de tramas PCF
T_beacon = 100 * 8 / 6 Mbit/s = 133.3 us
T_poll = 20 * 8 / 6 Mbit/s = 26.7 us
T_ACK = 18.7 us, 
T_DATA = 1000 us

#### Tiempo total PCF
Secuencia:
Beacon + SIFS + Poll + SIFS + DATA + SIFS + ACK + PIFS +
Poll + SIFS + DATA + SIFS + ACK
T_total = 2450.8 us

#### Tasa efectiva PCF
R_eff = 24000 bits / 0.0024508 s = 9.79 Mbit/s
Con dos tramas, DCF y PCF dan valores similares. Con más tráfico, el beacon se amortiza
y el poll puede ser más barato que RTS+CTS.

## 8. Ejercicios modelo de teoría

### Ejercicio 1: V/F
Decidir verdadero o falso y justificar.
1. WiFi usa CSMA/CD porque puede detectar colisiones mientras transmite.
2. RTS/CTS ayuda especialmente con estación oculta.
3. Una estación expuesta produce necesariamente colisión.
4. En DCF, SIFS se usa dentro de un mismo diálogo.
5. PCF requiere un AP que coordine el acceso.
6. La tasa efectiva de aplicación suele ser menor que la tasa física.

>[!question]- Respuesta:
>1. Falso. WiFi usa CSMA/CA; detectar colisiones mientras transmite es difícil.
>2. Verdadero. El CTS del receptor puede ser oído por estaciones ocultas al emisor.
>3. Falso. La expuesta se calla innecesariamente; el problema principal es subutilización.
>4. Verdadero. CTS, DATA y ACK responden tras SIFS.
>5. Verdadero. PCF es coordinación puntual desde el AP.
>6. Verdadero. Hay overhead, esperas, control y posibles retransmisiones

### Ejercicio 2: multiple choice
¿Por qué 802.11 (WiFi) no usa CSMA/CD como Ethernet clásica?
A Porque no existen direcciones MAC en WiFi.
B Porque una estación inalámbrica normalmente no puede escuchar colisiones de forma confiable
mientras transmite.
C Porque los ACKs están prohibidos en redes inalámbricas.
D Porque WiFi nunca comparte el medio.

>[!question]- Respuesta:
>B Porque una estación inalámbrica normalmente no puede escuchar colisiones de forma confiable mientras transmite.
Correcta: B. La propia señal transmitida domina al receptor y además existen nodos
ocultos.

### Ejercicio 3: multiple choice
Orden correcto de prioridad temporal:
A `SIFS < PIFS < DIFS`
B `DIFS < PIFS < SIFS`
C `PIFS < SIFS < DIFS`
D `SIFS < DIFS < PIFS`

>[!question]- Respuesta:
>A `SIFS < PIFS < DIFS`
Correcta: A. SIFS da prioridad a respuestas inmediatas; PIFS al AP en PCF; DIFS a
nueva contienda DCF.

### Ejercicio 4: multiple choice
Una estación escucha un CTS dirigido a otro emisor. ¿Qué debería hacer?
A Transmitir inmediatamente porque el CTS no transporta datos.
B Configurar su NAV y deferir durante el intervalo anunciado.
C Enviar un ACK al emisor del CTS.
D Cambiar de AP obligatoriamente

>[!question]- Respuesta:
>B Configurar su NAV y deferir durante el intervalo anunciado.
Correcta: B. CTS reserva el canal visto desde el receptor.

### Ejercicio 5: reconocer oculta/expuesta
Caso A: A y C no se escuchan, pero ambos llegan a B . C está transmitiendo a B y A
quiere transmitir a B .
Caso B: B transmite a A . C escucha a B , pero quiere transmitir a D , que no interferiría
con A .
Clasificar ambos casos.

>[!question]- Caso A, respuesta:
> estación oculta.
A no detecta a C.
A puede transmitir y chocar en B.
RTS/CTS ayuda si A escucha el CTS de B.

>[!question]- Caso B, respuesta
> estación expuesta.
C se inhibe por escuchar B.
Pero C -> D podría ser segura.
El costo es perder paralelismo.

### Ejercicio 6: línea de tiempo !!!!
En DCF con RTS/CTS, A quiere enviar datos a B. No hay colisión y no se considera
backoff.
Armar la secuencia usando SIFS/DIFS.

>[!question]- Respuesta:
>A DIFS -> RTS -> SIFS -> DATA
B SIFS -> CTS -> SIFS -> ACK
Vecinos  A oyen RTS, configuran NAV
Vecinos B oyen CTS, configuran NAV
Secuencia lineal:
DIFS, RTS, SIFS, CTS, SIFS, DATA, SIFS, ACK

### Ejercicio 7: cálculo corto !!!!
Una trama de datos tiene 1000 B y se transmite a 20 Mbit/s . RTS, CTS y ACK suman
60 B y se transmiten a 10 Mbit/s . Hay tres SIFS de 10 us y un DIFS de 50 us . No hay
backoff.
Calcular tasa efectiva para una sola trama si el intervalo medido empieza en DIFS y termina
al final del ACK.

>[!question]- Respuesta:
>Datos útiles:
1000 B * 8 = 8000 bits
Tiempos:
DATA = 8000 / 20 Mbit/s = 400 us
control = 60 * 8 / 10 Mbit/s = 48 us
esperas = 3 * 10 + 50 = 80 us
>
Ejercicio 7: resultado
T_total = 400 + 48 + 80 = 528 us
R_eff = 8000 bits / 528 us = 15.15 Mbit/s
La tasa efectiva es menor que 20 Mbit/s porque incluye control y esperas


### Ejercicio 8: multiple choice
En un cálculo de tasa efectiva, ¿qué se usa como numerador?
A Todos los bits transmitidos, incluyendo RTS, CTS y ACK.
B Los bits útiles de datos que el ejercicio considera entregados.
C Solo los bits de preámbulo.
D La suma de SIFS, PIFS y DIFS.

>[!question]- Respuesta:
>B Los bits útiles de datos que el ejercicio considera entregados.
Correcta: B. El overhead va en el denominador, no en el numerador de tasa útil.