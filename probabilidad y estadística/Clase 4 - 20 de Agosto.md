## Variable aleatoria. Densidad discreta y distribución 
**** 

>[!example] Ejemplo 1
>En un ítem de una prueba de una prueba aplicada a niños pequeños, se les pide que hagan corresponder cada uno de los tres dibujo sde animales con la palabra que identifica a ese animal.
>Si un niño asigna aleatoriamente las tres palabras a los tres dibujos,
>1. Encuentre la función densidad discreta
>2. La función de distribución acumulada de Y, el número de aciertos
>3. Encuentre $P(1 \leq X \leq 6)$.
>
>Resolución
>Si la posición en el vector $(x,y,z)$ denota el dibujo $d_1, d_2, d_3$ denotan los nombres de los animales, el espacio muestral del experimento es $$\Omega = \{(d_1, d_2, d_3), (d_2,d_1, d_3), (d_3, d_2, d_1), (d_1, d_3, d_1), (d_3, d_1, d_2), (d_1,d_3,d_2), (d_3, d_1, d_2), (d_2, d_3. d_1)\}$$
> y es equiprobable, con $P(\{\omega\})= \frac{1}{6}$
>
>La variable $Y$ toma 3 valores con probabilidad diferente de cero por lo cual $R_Y = \{0,1,3\}$. La función $p_Y$ toma los valores $$p_Y(0) = P(Y = 0) = P({\text{ningún acierto}})$$ 
>$= P(\{(d_2, d_3, d_1), (d_3, d_1, d_2)\}) = \frac{2}{6}$
>$$p_Y(1)= P(Y=1) = P(\{\text{exactamente un acierto}\})$$
>$P(\{(d_1,d_3,d_2), (d_3,d_2,d_1), (d_2, d_1, d_3)\}) = \frac{3}{6}$
>$$p_Y(2) = P(Y=2) = P(\{\text{exactamente dos aciertos}\}) = 0$$
>(porque si acierto dos, acierto 3)
>$$p_Y(3) = P(Y=3) = P(\{exactamente tres aciertos\})$$
>$= P(\{(d_1, d_2, d_3)\}) = \frac{1}{6}$
>
>y F_Y resulta 
>$$F_Y(t) = P(Y \leq t) = 0 \ \ \ \ t < 0$$
>$$F_Y(t) = P(Y \leq t) = p_Y(0) = \frac{2}{6} \ \ \ \ 0 \leq t < 1$$
>$$F_Y(t) = P(Y \leq t) = p_Y(0) + p_Y(1) = \frac{2}{6} +\frac{3}{6} \ \ \ \ 1\leq t < 2$$
>$$F_Y(t) = P(Y \leq t) = p_Y(0) + p_Y(1) + p_Y(2) = \frac{2}{6} +\frac{3}{6} + 0 \ \ \ \ 2\leq t < 3$$
>$$F_Y(t) = P(Y \leq t) = p_Y(0) + p_Y(1) + p_Y(2) + p_Y(3) = \frac{2}{6} +\frac{3}{6} + 0 + \frac{1}{6} = 1\ \ \ \ 3\leq t$$
>$$P(1 < X \leq 6) = F_X (6) - F_X(1) = 1- \frac{5}{6} = \frac{1}{6}$$
>![[Pasted image 20260825225301.png]]



>[!example] Ejemplo 2
>Experimento aleatorio: lanzar cuatro veces una moneda equilibrada.
>Espacio muestral: $$\Omega = \{CCCC, CCC+, CC+C, C+CC, +CCC,$$
>$$ CC++, C+C+, C++C, +CC+, +C+C, ++CC,$$
>$$ +++C, ++C+, +C++, C+++, ++++\}$$
>
>- Ningún punto del espacio tiene mayor probabilidad de ocurrir
>- Probabildad de Laplace asociada al espacio $\Omega$
>- $P(\Omega) = 1/ \#\Omega = 1/16$
>
>Variable aleatoria X: Recolecta el número de cruces obtenidas en una realización del experimento. ¿Qué valores puede tomar la variable? ¿Con qué probabilidad?
>
>X v.a. que expresa el número de cruces obtenidas; toma el valor 0 cuando el resultado es $\{CCCC\}$, el valor 1 si ocurre el suceso $\{CCC+, CC+C, C+CC, +CCC\}$, el valor 2 si aparece $\{CC++, C+C+, C++C, +CC+, +C+C, ++CC\}$, el valor 3 para los resultados $\{+++C, ++C+, +C++, C+++\}$, y el valor 4 si sale $\{++++\}$
$P(x_i) = \left\{\begin{array}{l} \frac{1}{16} x_i = 0\\\ \frac{4}{16}\ x_i = 1 \\\ \frac{6}{16} \ x_i = 2 \\\ \frac{4}{16} \ x_i = 3 \\\  \frac{1}{16} \ x_i= 4 \end{array} \right.$
$F(x) = \left\{\begin{array}{l} 0 \ x < 0 \\\ \frac{1}{16}\ 0 \leq x < 1 \\\ \frac{5}{16} \ 1 \leq x < 2 \\\ \frac{11}{16} \ 2 \leq x < 3 \\\  \frac{15}{16} \ 3 \leq x< 4 \\\ \frac{16}{16}=1 \ x \geq 4 \end{array} \right.$
Se quiere hallar la probabilidad de que aparezcan más de dos cruces:
$P(X > 2) = P(X=3) + P(X=4) = \frac{4}{16} + \frac{1}{6} = \frac{5}{16}$
o también $P(X>2) = 1 - P(X \leq 2) = 1-F(2) = \frac{5}{16}$
Se quiere calcular la probabilidad de que el número de cruces sea más de 1 y menos de 4:
$P\{1 < X <4\} = P(X=2) +P(X=3) = \frac{4}{16} + \frac{6}{16} = \frac{10}{16}$


>[!example] Ejemplo 3
>Una moneda honesta se tira una vez. Si sale cara se tira una segunda vez y si sale cruz se tira 2 veces. 
>Hallar la función densidad discreta de X el número total de caras obtenidas.
>![[Pasted image 20260826220843.png]]
>
>Resolución
>La variable X toma los calores 0,1,2. No puede tomar el valor 3 pues nunca se tira tres veces si salió cara la primera vez. 
>Definamos $Y$ la variable que vale 1 si salió cara la primera vez, y 0 si no.
>Entonces, si $Y=0$ tenemos el experimento condicional con espacio muestral equiprobable  $$\Omega_0 = \{(s,s,s), (s,c,s), (s,s,c), (s,c,c)\}$$
>y si $Y=1$, tenemos el experimento condicional con espacio muestral equiprobable $$\Omega_1 = \{(c,s), (c,c)\}$$
>por lo tanto,
>$p_X (0) = P(X=0/Y=0) P(Y=0) + P(X=0 /Y=1) P(Y=1)$
>$= P(\{(s,s,s)\}) P(cruz en la primera) + P(\emptyset) P(cara en la primera)$
>$=\frac{1}{4}.\frac{1}{2} + 0 . \frac{1}{2} = \frac{1}{8}$
>
>$p_x(1) = P(X=1/Y=0)P(Y=0) + P(X=1/Y=1)P(Y=1)$
>$=P(\{(s,c,s),(s,s,c)\})P(\text{cruz en la primera}) + P(\{(c,s)\}) P(\text{cara en la primera})$
>$=\frac{2}{4}. \frac{1}{2} + \frac{1}{2}.\frac{1}{2} = \frac{1}{2}$
>
>$p_x(2) = P(X=2/Y=0)P(Y=0) + P(X=2/Y=1)P(Y=1)$
>$=P(\{(s,c,c)\})P(\text{cruz en la primera}) + P(\{(c,c)\}) P(\text{cara en la primera})$
>$=\frac{1}{4}. \frac{1}{2} + \frac{1}{2}.\frac{1}{2} = \frac{3}{8}$


## Transformación de variables aleatorias 
Dadas una variable aleatoria X y una función real de variable real $g: \mathbb{R} \rightarrow \mathbb{R}$ queremos estudiar la distribución de la variable aleatoria transformada por g de $X$, $Y = g(X)$

Basta con calcular la función de distribución de $Y (P \text{ está caracterizada por F})$
$$F_Y (y) = P_Y(Y \leq y) = P_Y(g(X) \leq y) = P_X(X \in A_y),$$
donde $A_y = \{x : g(x) \leq y\} \ \ \ \text{en muchos casos es sencillo de calcular}$

>[!tip] Transformación de una v.a. discreta
>- Función de distribución $$F_Y(y) = P_X(X \in A_y) = \sum_{x_i \in A_y} p_X(x_i) = \sum_{g(x_i)\leq y} p_X(x_i)$$
>- Función de masa: $$p_Y(y) = P_Y(Y=y)= P_Y(g(X) = y) = \sum_{g(x_i) = y} p_X(x_i)$$


![[Pasted image 20260830212939.png|470]]

>[!example] Ejemplos, relacionados con los de antes (4)
>1. En el ejemplo de $Y$  el número de aciertos al corresponder el nombre de un animal con su dibujo al azar, se define la variable $Z = Y²$. Entonces $Z$ toma valores $0² \  \  1² \ \ y 3²$, con probabilidades $$p_Z(0) = P(Y² = 0) = P(Y=0) = \frac{2}{6}$$ $$p_Z(1) = P(Y² = 1) = P(Y=1) = \frac{3}{6}$$ $$p_Z(9) = P(Y²=9) = P(Y=3) = \frac{1}{6}$$
>
>2. En el ejemplo de $Y$  el número de aciertos al corresponder el nombre de un animal con su dibujo al azar, se define la variable $Z = (Y-1)²$. Entonces $Z$ toma valores $0 \  \  1 \ \ y 4$, con probabilidades $$p_Z(0) = P((Y-1)² = 0) = P(Y=1) = \frac{3}{6}$$ $$p_Z(1) = P((Y-1)² = 1) = P(Y=0) = \frac{2}{6}$$ $$p_Z(4) = P(Y-1)²=4) = P(Y=3) = \frac{1}{6}$$
>3. En el ejemplo de $Y$  el número de aciertos al corresponder el nombre de un animal con su dibujo al azar,suponga que se define la variable $Z$ que otorga un caramelo si acierta uno o más veces y no da ninún caramelo si no le acierta a ninguno. Entonces $Z$ toma valores $0 \  \ y\ \   1$, con probabilidades $$P(Z=0) = P(Y=0) = \frac{1}{3}$$ $$p(Z=1) = P(Y = 1) + P(Y=2) + P(Y=3) = \frac{2}{3}$$

## Medidas características de una variable
El estudio y comparación de la distribucion de probabilidadd de distintas variables aleatorias es más sencillo mediante el uso de constantes (**medidas características** de la variable) que caracterizan:
- La tendencia central de las distribuciones (o valor central alrededor del cual se encuentran repartidas de forma equilibrada las porbabilidades),
- la dispersión (mayor o menor densidad en torno al valor central)
- etc-

## Parámetros de tendencia central: esperanza
**** 

El principio es que el valor de una ganancia futura debe ser directamente proporcional a la posibilidad de obtenerla.

>[!example] Ejemplo 5
>1. Sea $X$ a la variable que representa nuestra ganancia en un juego.
>2. Esto es, con probabilidad $p_(x_i)$ ganamos $x_i$ monedas, con $i = 1,..,n$
>3. La interpretación frecuentista dice que si jugamos este juego infinitas veces, la proporción de veces que ganamos $x_i$ monedas es $p(x_i)$
>
>Proporción muestral = $\frac{n_i}{N}$
>$N$ número de experimentos
>$n_i$ número de veces que observamos $x_i$
>1. Supongamos que jugamos N veces el mismo juego, con N muy grande. Aproximadamente $Np(x_i)$ veces de esos juegos, ganaremos x_i monedas y el total de nuestra ganancia en $N$ juegos será  

$$\sum_{i=1}^n x_iNp(x_i)$$$\frac{1}{N} \sum_{i=1}^n x_iNp(x_i) = \sum_{i=1}^n x_ip(x_i) = \text{ganancia esperada}$$

### Definición 
Esperanza de una v.a. discreta $$\mu_X = E[X] = \sum_{i} x_ip_X(x_i)$$
- medida característica de tendencia central más importante
- también se denomina "esperanza matemática", "media" o "valor esperado" de la v.a.
- se denota como $E[X]$ o $\mu_X$
- representa el valor promedio o centro de gravedad de los valores que toma la variable, ponderando éstos mediante la correspondiente probabilidad.
![](data:image/png;base64,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)

>[!example] Ejemplo 6
>1. Vamos a llamar $E(X)$ esperanza de la variable $X$ o valor esperado de la variable $X$, pero no debemos interpretarlo como el valor que debiéramos esperar que X nos dé sino el valor promedio de $X$ es una gran cantidad de repeticiones del experimento, y no necesariamente este valor es un resultado posible del experimento. 
>2. Como ejemplo pensemos en la variable indicadora de un evento particular. 
>   $$ I =
>   \left\{
>   \begin{array}{ll} 
>   1 & \text{si } A \text{ ocurre} \\\
>   0 & \text{si } A \text{ no ocurre} 
>   \end{array}
>   \right.
>   $$
>   entonces $$E(I) = 1P(A) + =(1-P(A)) = P(A)$$

Dada $g:\mathbb{R} \rightarrow \mathbb{R}$, la esperanza de $Y=g(X)$, viene dada por $$\mu_Y = E[Y] = \sum_{i} g(x_i)p_X(x_i)$$

