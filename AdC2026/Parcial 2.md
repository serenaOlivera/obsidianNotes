## 1. Caché
--- 

Mientras más rápida querramos nuestra memoria, más cara va a ser. 
La memoria ideal es aquella que tiene un tiempo de acceso de una SRAM (0.5ns ~ 2.5 ns)  y una capacidad y costo/GB de disco. 
![[Pasted image 20261017190655.png|464]]

>[!info] Principio de Localidad
>Los programas acceden a una porción pequeña de su espacio direccionable en cualquier momento.
>>[!info] Localidad Temporal
>>Items accedidos recientemente son más probables de ser accedidos de vuelta en poco tiempo. ejemplo: loops, variables inducidas.
>
>>[!info] Localidad Espacial
>>Items cerca de aquellos accedidos recientemente son más probables de ser accedidos en poco tiempo. Ejemplo: isntrucciones secuenciales, datos de array.

Lo que hacemos es guardar todo en disco, y copiar los items recientemente accedidos, y cercanos desde los niveles más bajos a los más altos.
![[Pasted image 20261017191115.png|599]]

### Niveles de Jerarquía de Memoria
Conceptos:
>[!notes] Conceptos
>**Bloque (línea):** Es una unidad de copiado. Una linea, pueden ser VARIAS palabras de memoria!!! (y usualmente lo son!!)
>Hit: ocurre cuando la data a la que queremos acceder está en el nivel más alto.
>	hit ratio =  $\frac{\text{hits}}{\text{accesses}}$
>Miss: ocurre cuando la data no se encuentra en el primer nivel, y tenemos que traerla de memoria
>	miss ratio =  $\frac{\text{misses}}{\text{accesses}} =$ 1- hit ratio 

![[Pasted image 20261017193855.png|316]]

### Organización de caché
![[Pasted image 20261017193958.png|585]]


### Señales de interfaz 
![[Pasted image 20261017194032.png|597]]

fijate que como de la cpu a la cache hay palabras, y de la cache a memoria hay bloques (de palabras), no siempre son iguales, en este caso, la memoria tiene bloques de 4 palabras.

### Memoria cache
Es el nivel de memoria en la jerarquía más cerano a la CPU.
Dado los accesos $X_1, \dots , X_{n-1}, X_n$ ¿cómo sabemos si la data está presente o no?¿A dónde miramos?
![[Pasted image 20261017194303.png|432]]

![[Pasted image 20261017194319.png|614]]

### Tags y Bits de Validez 

¿Cómo sabemos que bloque particualrmente está guardado en un lugar de la caché?
Guardamos la dirección del bloque asi también como el dato, que en realidad solo necesitamos los bits de alto orden, que es llamado el **tag**.

¿Qué pasa si no hay datos en un lugar de la cache? 
Valid bit: 1 = datos presentes, 0 = no presentes. Inicialmente, valid bit es 0.

### Misses de Cache
En un hit, la CPU procede normalmente. En un miss...
- Stall el pipeline de la cpu
- fetcheamos el bloque del siguiente nivel de jerarquía
- Instruction cache miss: Restart instruction fetch 
- Data cache miss: Complete data access

>[!info] Como calcular modulo cuando tu calculadora no es genial :(
> $\text{A mod B} =  A − \text{(parte entera de (A/B))×B}$

A−(parte entera de (A/B))×B
### !!! Cache de Mapeo Directo !!!!
El lugar está determinado por la dirección. En el mapeo directo, sólo tenes UNA elección 
**(Dirección de bloque) módulo (#bloques en caché)**.
Los bloques son una potencia de dos, y usamos los bits de bajo orden.
![[Pasted image 20261017195319.png|509]]

Subdivisión de Direcciones:
![[Pasted image 20261017195354.png]]

Ejemplo: ![[Pasted image 20261017195837.png|544]]

### !!!Caché asociativa!!!
- Full asociativa:
  - Permite a un bloque dado ir en cualquier entrada de caché.
  - Requiere que todas las entradas sean buscadas inmediatamente
  - Comparador por entrada, muy caro.
- conjuntos de n vías 
  - Cada conjunto (set), contiene n entradas. 
  - El numero de bloque determina cuál set
	    **(número de bloque) módulo (#sets en cache)**
  - Busca todas las entradas en un set inmediatamente
  - n comparadores (menos caro)

Espectros de asociatividad:![[Pasted image 20261017202705.png|535]]

ejemplo de asociatividad
![[Pasted image 20261017202831.png|526]]

Cache full asociada - subdivision de direcciones:
![[Pasted image 20261017203004.png]]

ojo!: el tamaño de bloque siempre es iguall al tamaño de línea, ya que siempre una línea aloja bloque de Memoria Principal (la línea puede estar compuesta de muchas palabras). Fully associative está god, pero no se puede implementar.

**Subdivisión de direcciones de  una cache de k-vías, conjuntos asociada:**
- nro de líneas = l
- cuando hablamos de sets tenemos l/k sets, ya que definimos vías dentro del mismo
- debo comparar los sets en simultaneo, cuando tengo entrada me fijo en el tag con el que viene la dirección para determinar cual es, ese tag lo comparo con el set correspondiente de cada vía.
![[Pasted image 20261017203809.png]]

![[Pasted image 20261017203946.png|556]]

#### Set associative cache organization 
![[Pasted image 20261017204038.png|513]]

Ejemplo super genial para que entiendas las diferencias de cache directo, asociativa fully, asociativa 2-vias 
- Comparar cache de 4 bloques 
- secuencia de acceso A BLOQUES 0,8,0,6,8

![[Pasted image 20261017205244.png|545]]
![[Pasted image 20261017205258.png|552]]


la asociatividad es genial porque nos permite que tengamos un miss rate bajo, pero a gran escala, esto se vuelve logaritmico, no es que mejora infinitamente.
![[Pasted image 20261017205621.png|649]]

>[!note] the big picture
Los principios comunes aplican en todos los niveles de jerarquía de memoria, basados en las nociones de caché. En cada nivel de jerarquía tenemos:
>- Block placement
>- Encontrar un bloque
>- Reemplazar data en un miss
>- Politicas de write

>[!info] Consideraciones para el tamaño de bloque:
Los bloques grandes deberían reducir la miss rate, debido a el principio de localidad espacial. Sin embargo, en una cache de tamaño fijo, los bloques grandes significa que hay menos de ellos, genera más competencia y entonces sube la miss rate. 
Tener bloques grandes genera pollution. Además  tenemos una miss penalty más grande (porque buscar en un bloque que tiene 809534 palabras tarda una banda), entonces esto puede sobrepasar los benificios de haber reducido la miss rate.

### Block placement
Están determinados por asociatividad 
- Mapeo directo: (1-vía asociativa): una sola elección para alocar nuestro bloque
- n-vías set asociativa: n elecciones en un set
- fully asociativa: cualquier lugar 

A mayor asociatividad ----> menos miss rate 
(a cambio incrementas complejidad, costo y tiempo de acceso).

| Asociatividad             | Método de Locación                                         | Comparaciones de tag  |
| :------------------------ | :--------------------------------------------------------- | :-------------------- |
| Mapeo directo             | Index                                                      | 1                     |
| n-vías por set asociativa | Set index, después buscas en las entradas dentro del set   | n&nbsp;               |
| Fully asociativa          | 1. Buscas todas las entradas<br>&nbsp;2. full lookup table | 1. # entradas<br>2. 0 |
### Origen de los Misses
- Misses compulsorios (aka cold start misses): el primer acceso a un bloque
- Misses de capacidad: debido a un tamaño finito de cache, un bloque reemplazado se vuelve a acceder.
- Misses de conflicto (aka misses de colisión): En una cache no completamente asociativa, debido a competencia por entradas en un set. No ocurriría en una cache de asociamiento completo del mismo tamaño total.
### Política de Reemplazo
- Mapeo directo: no tiene elección 
- Asociada por sets: Se prefiere una entrada no válida, si hay alguna. De lo contrario se elige entre las entradas en el set.
- LRU (least recently used): Elegir aquella sin usar por el tiempo más largo. Esto es simple para 2 vías, manejable para 4-vías y muy difícil después de eso.
- Random: Da aproximadamente la misma performance que LRU para alta asociatividad.

### Write Allocation
¿Qué debe suceder en un miss de write?
Alternativas:
- Allocate on miss: fetch el bloque
- Write around: no fetchees el bloque. Dado que los programas usualmente escriben un bloque entero antes de leerlo.
- Para write back, usualmente fetchea el bloque.

### Write-Through
En un hit de data-write, podríamos solo actualizar el bloque en la cache, pero entonces la cache y memoria serían inconsistentes.
Write-trough: también actualiza la memoria. 
Pero hace que los writes tomen más tiempo. Por ejemplo: Si mi CPI = 1, 10 % de las instrucciones son stores, entonces, el write a memoria toma 100 ciclos. 
	CPI efectivo = 1 + 0.1* 100 = 11
Solución: usar un write-buffer 
- Guarda datos esperando a ser escritos en memoria
- CPU continúa inmediatamente y sólo stallea en el write si el buffer está lleno.

### Write-Back
Alternativa: en un hit de data-write, simplemente updatea el bloque en caché. Mantené un registro de que bloque está 'sucio'. 
Cuando un bloque sucio es reemplazado, escribilo en memoria. Podés usar un write buffer para permitir que el bloque que va a ser reemplazado se lea primero.

### Midiendo Performance de Cache!!!!
Componentes del tiempo de CPU: 
- Ciclos de ejecución de progama, incluye el tiempo de hit de cache 
- Stalls de ciclos de memoria (principalmente de los misses de cache)
Con asumiciones simples
$\text{Memory stall cycles} = \frac{\text{Memory accesses}}{Program} * \text{Miss rate} * \text{Miss penalty}$
$$= \frac{\text{Instrucciones}}{\text{Program}} * \frac{\text{Misses}}{\text{Instruction}} * \text{Miss penalty}$$

ejemplo nisu:
![[Pasted image 20261017212848.png|522]]

### Average Access Time
El Hit Time también es importante para la performance
- Average memory access time (AMAT) $$\text{AMAT} = \text{Hit time} + \text{Miss rate} * \text{Miss Penalty}$$
- Ejemplo: CPU con clock de 1ns, hit time de 1 ciclo, miss penalty de 20 ciclos y l-cache miss rate = 5%.  $$\text{AMAT} = 1 + 0.05 * 20 = 2ns$$ osea, 2 ciclos por instrucción.

### Cachés de multinivel
La caché principal está conectada a la CPU. Pequeña, pero rápida. 
La caché de nivel 2, sirve los misses de la caché principal. Más grande. lenta, pero sigue siendo más rápida que la memoria principal.
Memoria principal sirve los misses de L-2. 
Algunos sistema de alto nivel, incluyen L-3 cache.

Ejemplo: Dado 
- CPU base CPI = 1, clock rate = 4GHz --> periodo 1/4ghz = 1/4 * 10^9 Hz = 0,25 * 10
- Miss rate/instrucción = 2%
- Main memory Access Time = 100ns

**Con una caché primaria**
- $$\text{Miss penalty} = \frac{\text{Tiempo de acceso a memoria (ns)}}{\text{Duración de 1 ciclo de reloj (ns/ciclo)}} = \frac{100ns}{0.25ns} = 400 \text{ciclos}$$
- $$\text{CPI efectivo} = 1 + 0.02 * 400 = 9$$
**Si añadimos una L-2 caché:**
- Tiempo de acceso de 5ns
- Miss rate global para la main memory = 0.5%
entonces:
Miss primario con hit de L-2:
$$\text{Penalty} = \frac{5ns}{0.25ns} = 20 \ \text{ciclos}$$
Miss pimario con miss de L-2:
tengo una extra penalidad de 500 ciclos
$$\text{CPI} = 1 + 0.02 * 20 + 0.05 * 400 = 3.4$$
Performance ratiio = 9/3.4 = 2.6

### Consideraciones de Caches de multinivel
- Cache primaria: se enfoca en hit time mínimo
- L-2 cache: Se enfoca en miss rate baja para evitar el acceso a memoria principal. Hit time tiene menos impacto general.
- Resultados: 
  L-1 caché usualmente pequeña que una sola cache
  L-1 bloque es de tamaño más pequeño que L-2 bloques.

### Tradeoffs de Diseño de caches

| Cambio de diseño                 | Efecto en la miss rate         | Performance effect negativo                                                                                                |
| :------------------------------- | :----------------------------- | :------------------------------------------------------------------------------------------------------------------------- |
| Aumentamos el tamaño de la cache | Decrece capacity misses        | Puede incrementar el access time                                                                                           |
| Incrementamos asociatividad      | Decrecen los conflict missess  | Puede incrementar el access time                                                                                           |
| Incrementamos tamaño de bloque   | Decrecen los compulsory misses | Incrementan los misses de penalidad. Para bloques muy grandes en tamaño. puede incrementar la miss rate debido a pollution |

### Pitfalls!! Errores comunes
- Byte vs direccionamiento de palabras:
  Ejemplo: caché de mapeo directo de 32 byte, bloques de 4 bytes.
  Byte 36 mapea a bloque 1  (porque 36 mod 4 es 0, primer bloque)
  Palabra 36 mapea a bloque 4 
- Ignorar efectos del sistema de memoria cuando se escribe o se genera código. 
  Ejemplo: iterar sobre filas vs columnas de arrays.  
- En un multiprocesador con L2 o L3 caches compartidas
  menor asociatividad que cores, resultan en misses de conflicto. Más cores => necesidad de incrementar asociatividad. 
- Usar AMAT para evaluar performance de procesadores out of order 
  Ignora el efecto de accesos no blockeados. En cambio, se evalua performance por simulación.

### Resumen Concluso
- Las memorias rápidas son chiquitas, memorias grandes son lentas. 
  Queremos memorias rapidas y grandes, cache nos da esa ilusión 
- Principio de Localidad
  Los programas usan una parte pequeña de su espacio direccionable frecuentemente
- Jerarquía de memorias
  L1 cache <-> L2 cache <-> ...<-> DRAM memory <-> disco
- memory sistem design es critico para multiprocesadores.

## 2. Técnicas de mejora de rendimiento
---
