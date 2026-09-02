## Parámetros de tendencia central: Esperanza 
**** 
>[!example] Ejemplo 1
>En el ejemplo de Y el número de aciertos al corresponder el nombre de un animal con su dibujo al azar $$p_Y(0) = \frac{2}{6}$$
>$$p_Y(1)=\frac{3}{6}$$  $$p_Y(3) = \frac{1}{6}$$
>La esperanza de $Y$ es $$E(Y) = 0p_Y(0) + 1p_Y(1)+3p_Y(3) = 0\frac{2}{6}+1\frac{3}{6}+3\frac{1}{6}=1$$

>[!example] Ejemplo 2
>¿Cuál es el tamaño promedio de una familia argentina? Aquí presentamos una tabla de la distribución de las familias argentinas de acuerdo a uno de los institutos de estadística provinciales
>![[Pasted image 20260831092706.png]]
>
>Si imaginamos seleccionar una sola familia al azar, el tamaño de la familia seleccionada es la variable aleatoria X con distribución de probabilidad dad por la tabla. La esperanza $E(X)$ es el tamaño medio de las familias de la población. Esta media es $$E(X)=2*0,231 + 3*0,397 + 4*0,212 +$$
>$$ 5*0,097 + 6*0,038 + 7*0,017 + 8*0,008$$  $E(X)=3,396$
>En este ejemplo hemos ignorado las familias con 9 miembros o más, en realidad el tamaño real de la sfamilias argentinas es más cercao a cuatro de lo que muestra este ejemplo.


>[!example] Ejemplo 3
>Consideremos los siguientes 3 juegos:
>1. Tiro una moneda Gano 1$ si sale cara y pierdo 1$ si sale número.
>2. Apuesto al rojo en la ruleta. Gano 1$ si sale rojo y pierdo 1$ si no sale rojo.
>3. Gano 1$ si saco un abolilla roja de una caja con 5 bolas, solo una roja, las demás negras. Pierdo 0.1$ si no saco la bola roja.
>¿A cual juego conviene jugar? Al juego con esperanza de ganar más alta
>
>Sea $X$ la ganancia neta (toma en cuenta lo que me paga la banca. lo que cuesta jugar y lo que apuesto).
>1. En el primer juego, la moneda tiene dos posiciones solamente y la esperanza de $X$ es $$E(X)= 1 . \frac{1}{2} + (-1).\frac{1}{2} =0$$
>2. En el segundo juego, hay 37 posiciones en la ruleta, de las cuales 18 son rojas y 18 negras y el cero. $$E(X)=1.\frac{18}{37} + (-1).\frac{19}{37} = -\frac{1}{37}$$
>3. En el tercer juego, hay una bola roja y cuatro negras, un 20% de posibilidades de sacar roja en una extracción al azar, por lo tanto $$E(X)=1.0,2 + (-0,1).0,8 = 0,2 - 0,008 = 0,12$$

### Propiedades
Si $X$ e $Y$ son varables aleatorias con esperanza finita y $a,\ b,\ c \in \mathbb{R}$ son constantes entonces:
1. $E[c] = c$
2. $E[cX] = c E[X]$
3. Si $X\geq 0$ entonces $E[X]\geq 0$
4. Si $X\leq Y$ entonces $E[X] \leq E[Y]$
5. Si $X$ está delimitada por dos números reales, $a \ y\ b$, esto es $a < X < b$ entonces también lo está su media, es decir, $a < E[X] < b$
6. Si $Y=a+bX$, entonces $E[Y]=E[a+bX]=a+bE[X]$
   
**La esperanza es una cantidad asociada, no tiene porque tomar valores de las variables**

>[!example] Ejemplo 4 
>1. Supongamos que medimos el error al predecir el valor de una variable $X$ por un número $c$ usando la función $g = (x-c)²$. Sea $\mu = E(X)$
>   $$E[(X-c)²] = E[(X-\mu+\mu-c)²]$$
>   $$= E[(X-\mu)² + 2(\mu-c)(X-\mu) + (\mu-c)²]$$
>   $$= E[(X-\mu)²] + 2(\mu-c)E[(X-\mu)] + E[(\mu-c)²]$$
>   $$=E[(X-\mu)²]+ 2(\mu-c)(E[X]-\mu) + E[(\mu-c)²]$$
>   $$E[(X_\mu)²+ (\mu-c)²]$$
>   $$\geq E[(X-\mu)²]$$
>2. El mejor predictor de una variable aleatoria, minimizando el error cuadrático media es la esperanza de la variable.

## Parámetros de tendencia central: Moda y Mediana
****
La tendencia central de ls distribuciones (o valor entral alrededor del cual se encuentran repartidas de forma equilibrada las probabilidades)
![[Pasted image 20260831095432.png]]

>[!info] Mediana de una v.a. X
>Es el valor $Me$ tal que $$P(X<Me) \leq \frac{1}{2}\text{, y } F(Me)=P(X\leq Me) \geq \frac{1}{2}$$
>es una medida de tendencia central en el sentido de que es el valor para el cual la distribución de probabilidad queda dividida en dos partes iguales.
>Es el primero valor (o rango de valores) que acumula (por la izquierda) una probabilidad mayor o igual a $\frac{1}{2}$

moda: valor de la variable que es más frecuente
media: le da mucho peso a los valores de la variable (uno cambia y se va)
mediana: No le empuja su valor un dato. Resuelve el problema de la media, pero a cambio es más complejo de calcular.

Que tengan la misma moda, media y mediana no implican que sean la misma, tenemos que ver la dispersión (es decir, la varianza): cuán diferentes son los valores con respecto a un centro/referencia. Usamos de referencia la esperanza.

## Medidas de variabilidad
****
### Varianza
1. Dada una variable aleatoria X, sería muy útil poder resumir las propiedades escenciales de una función de masa con medidas diseñadas cuidadosamente. Una de esas medidas es la esperanza $E(X)$.
2. Observemos las variables, $X,\ Y\ y \ Z$ con funciones de masa determinada por $$W=0 \text{  con probabilidad 1}$$$$ Y =
\left\{
\begin{array}{ll}
-1 & \text{ con probabilidad } \frac{1}{2} \\\
1 & \text{ con probabilidad } \frac{1}{2}
\end{array}
\right.$$
$$ W =
\left\{
\begin{array}{ll}
-100 & \text{ con probabilidad } \frac{1}{2} \\\
100 & \text{ con probabilidad } \frac{1}{2}
\end{array}
\right.$$
Las tres tienen la misma esperanza, están centradas en cero. Pero su dispersión alrededor de la media es muy diferente.
3. Podemos calcular la $E(|X-\mu|)$, pero es matemáticamente inconveniente, por lo cual se considera más apropiada $E((X-\mu)²).$
![287](data:image/png;base64,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)

>[!info] Varianza de una v.a. discreta
> $\sigma_{X}² = V(X)=E[(X-\mu_X)²] = \sum_i (x_i-\mu_X)²p_X(x_i)$
> o alternativamente:
> $\sigma_X² = E[X²] - \mu_X² = \sum_i x_i^2p_X(x_i) - \mu_X²$
> 
> - momento centrla de orden 2: $\mu_2 = E[(X-\mu_X)²]$
> - se denota por $V(X) \ o\  \sigma_X²$
> - representa la distancia cuadrática promedio a la media $\implies$ dispersión de una v.a. en torno a su media.
> - Su raíz cuadrada, $\sigma$, se denomina **desviación típica**
> - $E[(X-\mu_X)²] = E[X²] - \mu_X²$
>   (el momento central de orden 2 es igual al momento ordinario de orden 2 menos el cuadrado del momento ordinario de orden 1)

### Propiedades
Dada una variable aleatoria $X$ y dos números reales $a, \ b \in \mathbb{R}$, se verifica:
- $V(X)=E[X²]-(E[X])²$
- $V(aX) = a²V(X)$
- $V(b)=0$
- $V(aX+b)=a²V(X)$ --> doble chequear este  
- **Desigualdad de Chebichev:** $$P(|X-\mu_X| > k\ \sigma_X) \leq \frac{1}{k²}$$
### Coeficiente de variación 
$$CV_X = \frac{\sigma_X}{\mu_X}$$
- Expresa la magnitud de la dispersión de una variable aleatoria con respecto a su valor esperado 
- Permite comparar la dispersión relativa de dos distribuciones de probabilidad.
- Especialmente útil cuando la escala de medida de las variables que queremos comparar difiere notablemente.

>[!example] Ejemplo 5
>Sea la vriable aleatoria discreta $X$ correspondiente al número de cruces obtenidas al lanzar 4 veces una moneda. $$\text{Función de masa: }P(x_i) = \left\{\begin{array}{l} \frac{1}{16} \ x_i = 0\\\ \frac{4}{16}\ x_i = 1 \\\ \frac{6}{16} \ x_i = 2 \\\ \frac{4}{16} \ x_i = 3 \\\  \frac{1}{16} \ x_i= 4 \end{array} \right.$$
> $\text{Media: } \mu_X = 0. \frac{1}{16}+1.\frac{4}{16} + 2.\frac{6}{16}+3.\frac{4}{16}+ 4. \frac{1}{16}=2$
> La función de distriución a la izquierda de 2 es $\frac{5}{16}$ u em 2 es $\frac{11}{16} \implies Me=2.$
> $\text{Varianza: } \sigma_X² = 0².\frac{1}{16} + 1².\frac{4}{16} + 2².\frac{6}{16}+3².\frac{4}{16} + 4².\frac{1}{16} - 2²=\frac{16}{16} = 1$ 
> $\text{Coeficiente de variación: } CV_X=\frac{\sqrt{1}}{2} = \frac{1}{2}$

## Momentos 
****
Valores esperados de ciertas funciones de X
Se pueden definir alredeor de cualquier punto de referencia:
- alrededor del cero $\implies$ momentos **ordinarios** o respecto al origen.
- Alrededor de la esperanza de $X \implies$ momentos **centrales** o respecto a la media.

>[!info] Momento ordinario de orden k: $\alpha_k = E[X^k]$
>$\alpha_1 = \mu_X$ (el momento ordinaro de orden 1 es la media de X)

>[!info] Momento central de orden k: $\mu_k = E[(X-\mu_X)^k]$
$\mu_1 = E[X-\mu_X] = E[X]- \mu_X = \mu_X -\mu_X =0$ (el momento central de orden 1 de cualquier v.a. es cero)
> Dos v.a. con los mismos momentos tienen la misma distribución de probabilidad (los momentos caracterizan la distribución de probabilidad)

## Distribuciones conocidas 
****

### Distribución Degenerada $X\equiv \delta_c$
Una variable aleatoria $X$ tiene distribución degenarada en el punto c si tene toda la probabilidad concentrada en dicho punto 
>[!info] Función de masa:
>$$P(X=c)=1, \ \ \ \  P(X \neq c)=0$$
>**Esperanza y varianza:**
>$$E[X]=c, \ \ \ \ V(X)=c²-c²=0$$

### Distribución Uniforme Discreta $X \equiv \text{Unif}\{x_1,...,x_n\}$
Una variable aleatoria $X$ tiene una distribución uniforme discreta sobre el conjunto de números $\{x_1,...,x_n\}$ si la probabilidad de que tome cualquiera de estos valores es la misma.
>[!info] Función de masa
>$$P(X=x_i)=
>\left\{
>\begin{array}{ll}
>\frac{1}{n}, \text{ si  } i=1,..,n \\\ 
>0, \text{ en otro caso} 
>\end{array}
>\right.
>$$
>**Esperanza y Varianza:**
>$$E[X]=\frac{1}{n} \sum_{i=1}^n x_i, \ \ \ \ V(X) = \frac{1}{n}\sum_{i=1}^n x_i^2 - (\frac{1}{n} \sum_{i=1}^n x_i)²$$

### Distribución Bernoulli $X \equiv Bern(p)$
Las pruebas de Bernoulli son experimentos aleatorios con 2 resultados posibles, "éxito", E y "fracaso" F, con probabilidades $P(E)= p$ y $P(F)=1-p=q$
- "Observar un chip al azar d elos producidos en una fábrica" $\rightarrow E=\text{"el chip no es defectuoso"}$ y $F=\text{"el chip es defectuoso"}$
- "Lanzar una moneda dos veces" $\rightarrow$ nos puede interesar sacar el mismo resultado las dos veces $\rightarrow E=\{CC,++\} \ y\ F=\{C+,+C\}$
- "Elegir al azar un número entre 0 y 1" $\rightarrow$ podemos considerar $\rightarrow E=[0, 0.3]\ y \ F=(0.3, 1]$
  
  La variable aleatoria $X$ obtenida al realizar una prueba de Bernoulli con $P(E)=p$ tiene distribución $Bern(p)$ 
$$X=
\left\{
\begin{array}{ll}
1, \text{ si obtenemos E} \\
0, \text{ si obtenemos F}
\end{array}
\right.$$
>[!info] Función de masa, Esperanza y Varianza
>$$P(X=x)=p^x (1-p)^{1-x} = p^x q^{1-x}, \ x=0,1$$
>$$E[X]=p \ \ \ \ V(X)=p(1-p)=pq$$
>Suma: la suma de v.a.'s independientes Bern(p) da lugar a otro tipo de v.a. denominada Binomal, de la que la Bernoulli es un caso particular.

### Distribución Binomial $X \equiv B(n,p)$
- Se genera por la repetición de n pruebas Bernouilli independientes.
- X="número de éxitos obtenidos en las n pruebas de Bernouilli"
- puede escrbirse como la suma de n v.a. Bern(p), independientes $$X=X_1,...,X_n,$$ con $$X_i =
  \left\{
  \begin{array}{ll}
1, \text{ si obtenemos E en la i-ésima prueba} \\ 
0, \text{ si obtenemos F en la i-ésima prueba}  
  \end{array}
  \right.$$
$X_i \equiv Bern(p),\ \  i=1,...,n$
>[!info] Función de masa, Esperanza y Varianza
>$$P(X=x) = \binom{n}{x}p^x(1-p)^{n-x} = \binom{n}{x}p^xq^{n-x},\ \ x=0,1...,n$$
>$$E[X]=np, \ \ \ \ V(X)=npq$$

![[Pasted image 20260831115138.png|419]]

>[!example] Ejemplo Binomial
>En 1963, Samuel Pepys (a quien hoy se recuerda mejor por su diario) escribió una carta a Isaac Newton preguntándole acerca de una apuesta que Pepys planeaba hacer. Pepys quería saber cuál de los dos siguientes eventos tenía la mayor probabilidad de ocurrir.
>1.  $A=\{\text{Se lanzan 6 dados y al menos 1 es un seis}\}$
>2.  $B=\{\text{Se lanzan 12 dados y al menos 2 son seis}\}$
>3.  $C=\{\text{Se lanzan 18 dados y al menos 3 son seis}\}$
>Pepys pensó que el tecero tenía la mayor probabilidad, pero Newton no estaba de acuerdo.
>
>La probabilidad del evento A es sencilla de calcular $$P(\text{al menos un seis en seis tiradas}) = 1- P(\text{0 seis en seis tiradas})$$
>$$= 1- \frac{5^6}{6^6}$$
>$$\approx .665$$
>Sin embargo, las probabilidades de los otros dos eventos son más complicadas de calcular. Por ejemplo, no es obvio cómo contar el número de formas de obtener exactamente 2 seis en 18 tiradas de dados.
>
>1. Definamos como éxito E obtener un seis en una tirada de dados y fracaso F no observar un seis en la misma tirada. La porbabilidad de éxito es $p=1/6$ y la de fracaso $q=5/6$.
>2. Este es un experimento Bernoulli
>3. Si lo repetimos 12 veces en forma independiente (tiramos 12 dados o tiramos un dado 12 veces en forma consecutiva), y definimos a $X$ como el número de éxitos en los 12 experimentos, esta variable tiene distribución binomial de parámetros $n=12$ y $p= 1/6$
>4. $P(B) = P(X\geq 2)$
>   
>   $$P(X \geq 2) = 1- P(X \leq 1)$$
>   $$=1- [P(X=0) + P(X=1)]$$ 
>   $$=1 -\binom{12}{0} (\frac{1}{6})^0 (\frac{5}{6})^{12} - \binom{12}{1} (\frac{1}{6})^1 (\frac{5}{6})^{11}$$
>   $$= 1- (\frac{5}{6})^{12} - 12 (\frac{1}{6}) (\frac{5}{6})^{11}$$
>   $$\approx .6187$$
>   
>   Sea $Y$ el número de seis en 18 tiradas de un dado. Y es una variable binomial con parámetros $p = \frac{1}{6}$ y $n= 18$
>    $$P(Y \geq 3) = 1- P(Y \leq 2)$$
>   $$=1- [P(Y=0) + P(Y=1) + P(Y=2)]$$ 
>   $$=1 -\binom{18}{0} (\frac{1}{6})^0 (\frac{5}{6})^{18} - \binom{18}{1} (\frac{1}{6})^1 (\frac{5}{6})^{17} - \binom{18}{2} (\frac{1}{6})^{2} (\frac{5}{6})^{16}$$
>   $$\approx .5973$$


### Distribución Poisson $X \equiv \mathbb{P}(\lambda)$
Expresa la probabilidad de que ocurran un número x de sucesos en un tiempo fijo, si ocurren con una tasa media conocida, $\lambda$, y son independientes del tiempo transcurrido desde el último suceso.
Se aplica a sucesos con probabiildad muy baja de ocurrir (sucesos "raros")
>[!info] Función de masa, Esperanza y Varianza
>$$P(X=x) = \frac{e^{-\lambda} \lambda^{x}}{x!}, \ \ \ \ x=0,1,...$$
>$$E[X]=V[X]=\lambda$$
>Suma: si $X_i \equiv \mathbb{P}(\lambda_i)$ son independientes $\implies \text{la v.a.} \sum_{i} X_i \equiv \mathbb{P}(\sum_{i} \lambda_i)$

>[!example] Ejemplo Poisson
>1. Estás en una habitación con $n$ personas.
>2. Cada persona en la sala ha contribuido con $1000 a una colecta .
>3. El dinero recolectado se redistribuirá de vuelta a las personas en la sala, de la siguiente manera: cada billete de mil pesos tiene la misma probabilidad de ir a cualquiera de los $n$ personas, independientemente de los otros billetes recolectados.
>4. Esto significa que algunas personas podrían recibir más de $1000 mientras que otras se quedan con nada.
>   
> 
> A medida que $n$ tiende a infinito ¿Cuál es la probabilidad de que termines sin dinero?
> Hay dos corrientes de pensamiento comunes:
> -  A medida que $n$ tiende a infinito el número de billetes en la colecta aumenta hasta el infinito, así que parece que la probabilidad de que termines con al menos uno de esos billetes debería acerarse a 1, es decir, la probabilidad de que termines sin dinero se aproxima a cero.
> - La probabilidad de que ganes un billete de 1000 es $\frac{1}{n}$ y a medida que $n$ tiende a infinito, esa probabilidad disminuye a 0, por lo que parece que la probabilidad de que termines sin dinero se aproxima a 1.
> ¿Cuál escuela de pensamiento es la correcta? Resulta que ambos argumentos están equivocados. Veamos por qué:
> 
> Vamos a definir la variable X como el número de billetes que recibes de la colecta de $n$ billetes. La variable $X$ tiene distribución binomial de parámetros $(m, 1/n)$, por lo cual la probabilidad de no recibir ningún billete es $$P(X=0)= \binom{n}{0} (\frac{1}{n})^{0} (1- \frac{1}{n})^{n}$$
>$$=(1-\frac{1}{n})^{n}$$ 
>¿Cuál es el límite cuando $n$ tiende a infinito? Es un límite famoso en matemática, un límite notable.
>Para calcularlo, se toma el logaritmo (natural) para bajar la $n$ del exponente y aplica la regla de L'Hopital: $$\lim_{n\rightarrow \infty} log(1-\frac{1}{n})^{n} = \lim_{n \rightarrow \infty} n log(1-\frac{1}{n})$$
>$$= \lim_{x \rightarrow 0} \frac{log(1-x)}{x}$$
>$$=\lim_{x \rightarrow 0} \frac{\frac{d}{dx} log (1-x)}{\frac{d}{dx}x}$$
>$$=\lim_{x\rightarrow 0}\frac{-\frac{1}{1-x}}{1}$$
>$$= -1$$
>$$lim_{n \rightarrow \infty} (1-\frac{1}{n})^{n} = e^{-1}$$
>La probabilidad de no recibir ninún diner es $1/e \approx 0.368$ cuando $n \rightarrow \infty$

Si $X$ es una variable Binomial de parámetros $(n, p=\lambda)$, la función de masa $X$ converge a la función de asa de una variable Poisson con parámetro $\lambda$ cuando $n$  tiende a infinito.
$$\lim_{n \rightarrow \infty} \binom{n}{k}p_{n}^{k} (1-p_n)^{n-k} = \lim_{n \rightarrow \infty}\frac{n(n-1)...(n-k+q)}{k!} (\frac{\lambda}{n})^k (1- \frac{\lambda}{n})^{n-k}$$
$$= \lim_{n \rightarrow \infty} \frac{\lambda^k}{k!}(1-\frac{\lambda}{n})^n \frac{n(n-1)...(n-k+1)}{n^k} (1-\frac{\lambda}{n})^{-k}$$
$$= \frac{\lambda^k}{k!} \lim_{n \rightarrow \infty} (1-\frac{\lambda}{n})^n (1-\frac{\lambda}{n})^{-k} (1-\frac{1}{n}) (1-\frac{2}{n})..(1-\frac{k-1}{n})$$
$$p_Y(k)=\frac{\lambda^k}{k!}e^{-\lambda}$$

Ejemplo
El número de errores en un artículo de investigación cuando llega al editor final es una variable con distribución Poisson con \mu=4.6 ¿Cuál es la probabilidad de que haya 2 o más erores en un artículo seleccionado al azar?
$$P(X \geq 2) = 1- P(X<2)$$
$$= 1- f(0)-f(1)$$
te quedaste en filmina 57

