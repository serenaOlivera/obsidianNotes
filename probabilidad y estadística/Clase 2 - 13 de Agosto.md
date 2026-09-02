## Nociones para práctico:
****
$n$ es el número total de elementos disponibles en el conjunto inicial
$r$ es el número de elementos que vas a *seleccionar*, agrupar o tomar de ese total.

**Permutaciones:**
- importa el orden y se usan TODOS los elementos
- Sin repetición: $P_n = n!$
- Con repetición: $P_n^{a,b,c,...} = \frac{n!}{a!*b!*c!*...}$

**Variaciones:**
- Importa el orden y no se usan todos los elementos
- Sin repetición: $V_n^r = \frac{n!}{(n-r)!}$
- Con repetición: $VR_n^r = n^r$

**Combinatoria:**
- No importa el orden y no se usan todos los elementos
- Sin repetición: $C_n^r = \binom{n}{r} = \frac{n!}{r! (n-r)!}$
- Con repetición: $CR_n^r = \binom{n+r-1}{r} = \frac{(n+r-1)!}{r! (n-1)!}$

## Probabilidad
**** 
Demostración de las propiedades de probabilidad
- Si $A = \emptyset$ , entonces $P(A)=0$
  $P(\emptyset) = P(\Omega ^c) = 1 - P(\Omega) = 1-1 =0$
- Si $A \subset B$ entonces $\mathcal{P}{A} \leq \mathcal{P}(B)$
  Si $A \subset B$ entonces podemos escribir
  $$B = A \cup (B \cap A^c)$$
  La cual es una unión disjunta. Por lo cual $P(B) = P(A) + P(B \cap A^c)$ y despejando, $$P(A)= P(B) - P(B \cap A^c) \leq P(B)$$
  pues toda probabilidad es no negativa.
- Sea A un evento, entonces $\mathcal{P}(A^c) = 1 - \mathcal{P}(A)$
  Como $A$ y $A^c$ son eventos disjuntos con $A \cup A^c = \Omega$, $$P(A) + P(A^c) = P(\Omega) = 1$$
  Despejando resulta 
  $P(A^c) = 1- P(A)$
- Si A y B son eventos entonces $\mathcal{P}(A \cup B) = \mathcal{P}(A) + \mathcal{P}(B) - \mathcal{P}(A \cap B)$
  Obervemos que $A \cup B = (A \cap B^c) \cup (A \cap B) \cup (A^c \cap B)$ en forma disjunta. También, $A = (A \cap B) \cup (A \cap B^c)$ en forma disjunta, y $B = (A\cap B) \cup (B\cap A^c)$ por lo cual $$P(A)+P(B)=P(A\cap B)+P(B\cap A^c) +P(A\cap B) + P(A\cap B^c)$$$= P(A\cup B) + P(A \cap B)$
  y resulta $P(A \cup B) = P(A) + P(B) - P(A\cap B)$

>[!info] Observación
>Creo un espacio $\Omega$ que no es equiprobable. Es más, es infinito numerable. Si puedo definir el valor de probabilidad para cada punto, $P(\{ \omega_{i}\})$ tal que $$P(\Omega) = \sum_{\omega_{i} \in \Omega} P(\{\omega_{i}\})= 1$$
>entonces $$P(A) = \sum_{\omega_{i} \in A} P (\{\omega_{i}\})$$
>es una **distribución de probabilidad**

### Ejemplo 1
Se tiene un dado cargado tal que la probabilidad de cada número es proporcional a ese número (es decir $P(x) = kx$ con $k$ fijo). Sean los eventos A = "número par", B="número primo" (recordar que 1 no es primo ) y C = "número impar"
1. Decir como debe ser $k$ para que $P(x) = kx$ sea realmente una probabilidad y liste la probabilidad de cada punto del espacio muestral.
2. Hallar $P(A),\  P(B\cup C), \  P(A\cap B^c)$
3. Hallar la probabilidad de que salga
   - Un número par o primo
   - Un número impar pero no primo

El espacio muestral del experimento "tiramos un dado cargado" es $\Omega = \{1,2,3,4,5,6\}$. Las probabilidades de cada punto siguen la regla $P(x) = kx$, y como la suma de las probabilidades de los puntos de todo el espacio muestral debe ser 1, podemos obtener el valor de k $$1 = k1+k2+k3+k4+k5+k6=k(1+2+3+4+5+6) = k21$$
despejando $k$ resulta $k=1/21$ y $$P(1)= \frac{1}{21},\  P(2)= \frac{2}{21},\  P(3)= \frac{3}{21}, P(4)= \frac{4}{21}, \ P(5)= \frac{5}{21}, \ P(6)= \frac{6}{21}$$
Si A = "número par" y B = "número primo" y C = "número impar", entonces $$P(A) = P(\{2,4,6\}) = \frac{2}{21}+\frac{4}{21}+\frac{6}{21}=\frac{12}{21}=\frac{4}{7}$$
$$P(B\cup C)=P(\{1,2,3,5\}) = \frac{1}{21}+\frac{2}{21}+\frac{3}{21}+\frac{5}{21} = \frac{11}{21}$$$$P(A\cap B^c) = P(\{\text{un número par que no es primo}\} = P()\{4,6\})=\frac{4}{21}+\frac{6}{21} = \frac{10}{21}$$
Ahora queremos saber la probabilidad de obtener el evento "un número par o primo", esto es $$P(A\cup B)=P(\{2,3,4,5,6\})=1-\frac{1}{21} = \frac{20}{21}$$
La probabilidad del evento "un número impar pero no primo" es $$P(C\cap B^c) = P(\{1\})=\frac{1}{21}$$
## Probabilidad Condicional
****
### Ejemplo
Se quiere estudiar qué personas en un grupo de $N$ mujeres y hombres tienen conocimientos de alemán. Se sabe que $N_A$ personas (entre ellas $N_{AM}$ mujeres) saben alemán.
Representamos por A el suceso "saber alemán", y por M el suceso "ser mujer". Si se elige al azar una persona entre todas  del grupo, la probabilidad de que sepa alemán, al ser un experimento equiprobable, es: $$P(A)=\frac{N_A}{N}$$
Si **se sabe**, que la persona seleccionada es mujer, la probabilidad de que sepa alemán, **condicionada** a que es mujer, es: $$\mathcal{P}(A|M)=\frac{\text{casos favorables}}{\text{casos posibles(incorporando que es mujer)}} = \frac{N_{AM}}{N_M} = \frac{\frac{N_{AM}}{N}}{\frac{N_M}{N}}$$
$$=\frac{\mathcal{P}(A\cap M)}{\mathcal{P}(M)}$$
Una vez que se sabe que ha ocurrido M se puede considerar que M es el nuevo espacio muestral. La probabilidad condicionada es la proporción de M que representa la parte de A que está en M.

>[!info] Probabilidad de un suceso A condicionada por un suceso B
>(o conocido que ha ocurrido el suceso B): $$\mathcal{P}(A|B) = \frac{\mathcal{P}(A\cap B)}{\mathcal{P}(B)}$$ 
>
>La ocurrencia de B no dice nada nuevo acerca de la ocurrencia de A $$\mathcal{P}(A|B) = \mathcal{P}(A)$$
>**Regla de la Multiplicación:**$$\mathcal{P}(A\cap B) = \mathcal{P}(A|B). \mathcal{P}(B)$$ 
>A y B son independientes sii $\mathcal{P}(A\cap B) = \mathcal{P}(A) * \mathcal{P}(B)$


