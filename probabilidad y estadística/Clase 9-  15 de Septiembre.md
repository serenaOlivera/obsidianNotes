## Distribución Uniforme 
****
Sean a y b constantes con a < b. La densidad uniforme sobre el intervalo (a, b) es la densidad f definida por
$$f(x) = \begin{cases} \frac{1}{b-a} & a < x < b \\ 0 & \text{en otro caso} \end{cases}$$
La distribución correspondiente a f está dada por
$$F(x) = \begin{cases} 0 & x < a \\ \frac{x-a}{b-a} & a \leq x \leq b \\ 1 & x > b \end{cases}$$
La esperanza y varianza de X con distribución uniforme es
$$E(X) = \frac{a+b}{2} \quad Var(X) = \frac{(b-a)^2}{12}$$

**Densidad $\mathcal{U}[a,b]$** 
![[Pasted image 20260908204135.png|482]]

>[!example] Ejemplo 1
>Supongamos que Mario usualmente va a visitar a María entre las 8 y 8:30 de la noche. Si el horario de llegada es aleatorio, ¿cuál es la probabilidad de que Mario llegue después de las 8:25?.
>Datos: 
>- El horario de llegada es aleatorio
>- El rango del horario de llegada es [8,8:30] 
>- La variable X, tiempo de llegada, es continua
>
>  En este caso, queremos calcular la probabilidad de que X, la variable que modela el tiempo de llegada de Mario, tome valores entre las 8:25 y las 8:30 hs. Si X tiene distribución uniforme entre las 8 y las 8:30 hs, su densidad puede escribirse como
$$f(x) = \begin{cases} \frac{1}{30} & 0 < x < 30 \\ 0 & \text{en otro caso} \end{cases}$$
donde x son los minutos despues de las 8 en los que Mario llega.
>$$P(25 \leq X \leq 30) = \int_{25}^{30} \frac{1}{30} dx = \frac{30 - 25}{30} = \frac{5}{30} = \frac{1}{6} = 0.166$$



>[!example] Ejemplo 2
>Sea $X$ con distribución uniforme en el $(0, 1)$. Encuentre la densidad de $Y = - \frac{1}{\lambda} \log(1-X)$para todo $\lambda > 0$
>
>Observemos primero que Y es una variable positiva y por lo tanto $F_Y(y) = 0$ para todo $y \leq 0$. Para $y > 0$ se tiene
>$$ \begin{align*}
F_Y(y) &= P(Y \le y) = P\left(-\frac{1}{\lambda} \log(1-X) \le y\right) \\
&= P(\log(1-X) \ge -\lambda y) \\
&= P(1-X \ge e^{-\lambda y}) = P(X \le 1-\exp(-\lambda y)) \\
&= F(1-e^{-\lambda y}) = 1-\exp(-\lambda y)
\end{align*}$$
por lo cual $f_Y(y) = F'_Y (y) = \lambda e^{−\lambda y}$ para $y > 0$. La densidad de $Y$ está dada por
>$$ f_Y(y) = \begin{cases} \lambda e^{-\lambda y} & y > 0 \\ 0 & y \leq 0 \end{cases}$$

**Propiedad**
Sea X un a variable aleatoria continua con función densidad $f_X$ y función de distribución acumulada $F_X$, tal que $F_X$ es estrictamente creciente en un intervalo $I$ (que puede ser no acotado), nula a la izquierda de $I$ y vale 1 a la derecha de $I$. Entonces $F^{ −1} ( x )$ está bien definido para cada valor $x \in I$.
1. Sea $Z = F(X)$, entonces $Z$ tiene distribución uniforme en $[0, 1]$.
2. Si $U$ tiene distribución uniforme en el $[0, 1]$, entonces $Y = F ^{−1}(U)$ tiene como distribución acumulada a la función $F$ .

*Resolución de la propiedad* 
Observemos que si $z \in [0, 1]$
$$P(Z \le z) = P(F(X) \le z) = P(X \le F^{-1}(z)) = F(F^{-1}(z)) = z$$
y como ésta es la función de distribución acumulada de una variable uniforme, sale el resultado. Observemos ahora que
$$P(Y \le y) = P(F^{-1}(U) \le y) = P(U \le F(y)) = F(y)$$
por lo cual $X$ e $Y$ tienen la misma función de distribución acumulada.

>[!info] Otra propiedad
>Si $X$ ~ $[0, 1]$ entonces
>1.  $\eta(p) = p$ con $p \in (0, 1)$
>2. $E(X) = \frac{1}{2}$ y $V(X) = \frac{1}{12}$
>3. Para cualquier $z < b$ números reales sea una variable aleatoria $Y = (b − a)X + a$. Entonces
>   -  $Y$ ~ $U[a, b]$
>    - $\eta_Y (p) = (b − a)p + a$ para cualquier $p \in (0, 1)$
>    - $E(Y) = \frac{a+b}{2}$ y $Var(Y) = \frac{(b−a)^2}{12}$

>[!example] Ejemplo 3
> El tiempo (en minutos) que tarda un camión en realizar un viaje (ida y vuelta), para transportar concreto hacia una obra en construcción, tiene distribución uniforme en el intervalo [50; 70].
>1. ¿Cual es la probabilidad de que la duración del viaje de un camión sea menor de 65 minutos?
>2. ¿Cual es la probabilidad de que la duración del viaje de un camión sea mayor de 65 minutos dado que se sabe que fue mayor a 55 minutos?
>3. Dar el valor medio y desviación estándar del tiempo que tarda un camión en realizar un viaje (ida y vuelta) para transportar concreto hacia la obra en construcción.
>4. Suponga que los tiempos que tardan cada uno de tres camiones en realizar un viaje (ida y vuelta) para transportar concreto hacia la obra en construcción son independientes entre si. ¿Cual es la probabilidad de que por lo menos uno de ellos tarde mas de 65 minutos?
>
>**Resolución:**
>Vamos a resolver cada una de las preguntas paso a paso. Sabemos que el tiempo de viaje tiene una distribución uniforme en el intervalo $[50, 70]$.
> 1. **Probabilidad de que la duración del viaje sea menor de 65 minutos**
> - Para una distribución uniforme en el intervalo $[a, b]$, la probabilidad de que una variable $X$ sea menor que un valor $x$ dentro del intervalo se calcula como:
$$P(X < x) = \frac{x - a}{b - a}$$
>- Aquí, $a = 50$, $b = 70$, y queremos la probabilidad de que $X < 65$:
$$P(X < 65) = \frac{65 - 50}{70 - 50} = \frac{15}{20} = 0.75$$
>- Así que la probabilidad de que la duración del viaje sea menor de 65 minutos es $0.75$ o 75%
> 2. **Probabilidad de que la duración del viaje sea mayor de 65 minutos dado que se sabe que fue mayor a 55 minutos**
 >- Queremos encontrar $P(X > 65 | X > 55)$ . Usamos la fórmula de la probabilidad condicional:
$$P(X > 65 \mid X > 55) = \frac{P(X > 65 \cap X > 55)}{P(X > 55)}$$
>-  Sabemos que $P(X > 65 \cap X > 55) = P(X > 65)$. Primero, calculemos $P(X > 65)$:
$$P(X > 65) = \frac{70 - 65}{70 - 50} = \frac{5}{20} = 0.25$$
>-  Ahora calculemos $P(X > 55)$:
$$P(X > 55) = \frac{70 - 55}{70 - 50} = \frac{15}{20} = 0.75$$
>- Entonces:
$$P(X > 65 \mid X > 55) = \frac{0.25}{0.75} = \frac{1}{3} \approx 0.3333$$
La probabilidad de que la duración del viaje sea mayor de 65 minutos dado que se sabe que fue mayor a 55 minutos es 1/3 o aproximadamente 33.33%.
>
>3. **Valor medio y desviación estándar del tiempo de viaje**
>- Para una distribución uniforme en el intervalo $[a, b]$, el valor medio $\mu$ y la desviación estándar $\sigma$ se calculan como:
>- Valor medio (esperanza):$$ \mu = \frac{a + b}{2} $$
>- Desviación estándar:
$$ \sigma = \sqrt{\frac{(b-a)^2}{12}} $$
>-  Para $a = 50$ y $b = 70$:
$$ \mu = \frac{50 + 70}{2} = \frac{120}{2} = 60 $$
$$ \sigma = \sqrt{\frac{(70 - 50)^2}{12}} = \sqrt{\frac{400}{12}} = \sqrt{33.3} \approx 5.77 $$
>- El valor medio del tiempo de viaje es 60 minutos y la desviación estándar es aproximadamente 5.77 minutos.
>
>4. **Probabilidad de que al menos uno de los tres camiones tarde más de 65 minutos**
>-  Primero, calculamos la probabilidad de que un camión tarde 65 minutos o menos. Sabemos que $P(X ≤ 65) = 0.75$.
>- Entonces, la probabilidad de que un camión tarde más de 65 minutos es $1 – 0.75 = 0.25$.
>-  Para tres camiones independientes, la probabilidad de que ninguno tarde más de 65 minutos es:
$$P(\text{ninguno tarda más de } 65) = (0.75)^3 = 0.421875$$
> - La probabilidad de que al menos uno de los tres camiones tarde más de 65 minutos es:
$$P(\text{al menos uno tarda más de } 65) = 1 - P(\text{ninguno tarda más de } 65)$$  $$= 1 - 0.421875 = 0.578125$$
>-  La probabilidad de que al menos uno de los tres camiones tarde más de 65 minutos es aproximadamente 0.578 o 57.8%

## Distribución Gamma 
**** 
- La distribución Gamma es una familia bi-paramétrica de distribuciones de probabilidad continua muy versatil.
- Las distribuciones Exponencial, Erlang y Chi-cuadrado son casos especiales de esta familia de distribuciones.
- Las densidades correspondientes a distribuciones de esta familia son sesgadas a derecha.
 ![[Pasted image 20260908212103.png|348]]

- Hay dos parametrizaciones equivalentes en uso
  -  Con parámetro de forma $\alpha$ y parámetro de escala $\beta$ 
  - Con parámetro de forma $\alpha$ y parámetro de escala inverso $\alpha = \frac{1}{\beta}$, llamado el parámetro de tasa.
- En ambos casos, los parámetros son números reales positivos.
- Esta familia de distribuciones tiene importantes aplicaciones en muchos campos, como econometría, estadística Bayesiana, testeo de longevidad y confiabilidad (o fiabilidad) de procesos instrumentales.
  -  En econometría la parametrización con forma α y escala β es común para modelar tiempos de espera,
  - Estimación Bayesiana favorece la parametrización en forma α y tasa λ para uso como distribución a priori conjugada.
- En ambos casos, los parámetros son números reales positivos.


La función gamma, muy importante en muchas ramas de la matemática, es parte de la definición de la función de densidad de probabilidad de la familia Gamma

>[!info] Función Gamma de Euler $\Gamma$
Para $\alpha > 0$ , la función Gamma evaluada en α esta definida como
$$ \Gamma(\alpha) = \int_{0}^{\infty} x^{\alpha-1} e^{-x} dx $$
**Propiedades de la función Gamma de Euler**
>1. $\Gamma (\alpha) =(\alpha-1)\Gamma(\alpha-1)$ para cualquier $\alpha > 1$
>2. $\Gamma (n) = (n-1)! \ \  \forall n  \in N$.
>3.  $\Gamma (1/2)= \sqrt{\pi}$

### Caracterización usando forma $\alpha$ y tasa $\lambda$
Variable aleatoria $X$ ~ $\Gamma(\alpha, \lambda)$
Para $\alpha ,\lambda > 0$ , Se dice que una variable aleatoria $X$ tiene distribución Gamma con parámetros de forma $\alpha$ y tasa $\lambda, X$ ~ $\Gamma(\alpha, \lambda)$ , si función densidad de probabilidad es
$$f_X(x, \alpha, \lambda) = \frac{\lambda^\alpha x^{\alpha-1} e^{-\lambda x}}{\Gamma(\alpha)}$$
Se dice que una variable aleatoria X tiene distribución Gamma con parámetros forma $\alpha$ y escala $\beta$ si la función de densidad de probabilidad es
$$f_X(x, \alpha, \beta) = \begin{cases} \frac{1}{\beta^\alpha \Gamma(\alpha)} x^{\alpha-1} e^{-\frac{x}{\beta}} & \text{si } x \ge 0 \\ 0 & \text{en otro caso} \end{cases}$$

>[!info] Esperanza y varianza de una distribución Gamma
>1. La media de una distribución Gamma esta dada por el producto de sus parámetros
$$ \mu = \alpha\beta = \alpha/\lambda $$
>2. La varianza es
$$ \sigma^2 = \alpha\beta^2 = \alpha/\lambda^2 $$
>3. La raíz cuadrada del parámetro de forma es el coeficiente de variación
$$ \sigma / \mu = 1 / \sqrt{\alpha} $$
> **Propiedad**
Si $X$ ~ $\Gamma (\alpha, \lambda)$ y $a > 0$ entonces $aX$ ~ $\Gamma(\alpha, \lambda/a)$

## Distribución Chi Cuadrado ✧(ꈍᴗꈍ)✧

Variable aleatoria $X$ ~ $\chi ^ 2(k)$
Se dice que una variable aleatoria $X$ tiene distribución Chi cuadrado con k grados de libertad, $X$ ~ $\chi²(k)$, si función densidad de probabilidad de X es
$$f_X(x, k) = \begin{cases} \frac{1}{2^{k/2}\Gamma(k/2)} x^{\frac{k}{2}-1}e^{-\frac{x}{2}} & \text{si } x \ge 0 \\ 0 & \text{en otro caso} \end{cases}$$
Notación: $X$ ~ $\chi²(k) = \Gamma (k/2 , \lambda = 1/2) = \Gamma (k/2, \beta =2)$
![[Pasted image 20260908214516.png|362]]

## Distribución Exponencial 
***
Sea $\lambda$ un valor real positivo. La densidad exponencial es la densidad f definida por
$$f(x) = \begin{cases} \lambda e^{-\lambda x} & x \geq 0 \\ 0 & x < 0 \end{cases}$$
La esperanza y varianza de $X$ con distribución exponencial de parámetro $\lambda$es
$$E(X) = \frac{1}{\lambda} \quad Var(X) = \frac{1}{\lambda^2}$$

### Densidades
![[Pasted image 20260908214718.png|398]]

>[!example] Ejemplo 4
>Como vimos en el ejemplo anterior, es la densidad de la variable $Y = - \frac{1}{\lambda} \log (1-X)$, cuando $X$ es uniforme en $(0, 1)$. La función de distribución acumulada correspondiente a $f$ es
$$ F(x) = \begin{cases} 1 - e^{-\lambda x} & x \geq 0 \\ 0 & x < 0 \end{cases}$$
Sea $X$ la duración en horas de las lámparas almacenadas en un depósito, y supongamos que pueden modelarse con la distribución exponencial con parámetro 0.01.
>1. Hallar la función de distribución acumulada de $X$, la duración de una lámpara elegida al azar del lote.
>2. ¿Cuál es la probabilidad de que una lámpara dure más de 120 horas? ¿Cuántas horas se espera que dure una lámpara?
>3. Si se tiene un lote de 10000 lámparas ¿Cuál es la probabilidad de que 10 lámparas elegidas al azar del lote duren menos de 70 horas?
>-  La distribución acumulada de X es la distribución de una exponencial, y se calcula aplicando directamente la definición:
$$P(X \le x) = \int_{0}^{x} \lambda \exp(-\lambda t) dt = \lambda \frac{\exp(-\lambda t)}{-\lambda} \bigg|_{0}^{x} = 1 - \exp(-\lambda x) \quad x > 0$$
>-  En el caso de $\lambda = 0.01$ resulta
$$P(X \le x) = 1 - \exp(-0.01x)$$
>- Usando esta fórmula podemos calcular la probabilidad de que una lámpara elegida al azar del depósito dure más de 120 hs. $$\begin{align*}
P(X > 120) &= 1 - P(X \le 120) = 1 - (1 - \exp(-0.01120)) \\
&= \exp(-0.01120) = \exp(-1.2) = 0.3011
\end{align*}$$
>
>Duración esperada de las lámparas
>-  Para una distribución exponencial de parámetro $\lambda$ , el valor medio $\mu$ se calculan como:
>- **Valor medio (esperanza):**
$$ \mu = \frac{1}{\lambda} $$
 Entonces se espera que dure 100 horas.
 >Si se tiene un lote de 10000 lámparas ¿Cuál es la probabilidad de que 10 lámparas elegidas al azar del lote duren menos de 70 horas?
>- Lote es realmente grande, comparado con la muestra
>- Suponer que extraemos con reposición, (pues la probabilidad de elegir dos veces la misma lámpara es casi nula).
>- Entonces podemos suponer que tenemos un experimento binomial, donde en cada extracción tenemos éxito si la lámpara dura menos de 70 horas.
>- La variable Y , número de lámparas que duran menos de 70 horas, es una variable binomial de parámetros $n = 10$ y $p = P(X < 70)$.
>- Calculemos esta probabilidad, $$P(X < 70) = 1 - \exp(-0.0170) = 1 - \exp(-0.7) = 0.5034$$
>- Entonces, la probabilidad de que las 10 lámparas elegidas al azar del lote duren menos de 70 horas es $$P(Y = 10) = \begin{pmatrix} 10 \\ 10 \end{pmatrix} 0.5034^{10}(1 - 0.5034)^{10-10} = 0.5034^{10} = 0.00104$$

>[!example] Ejemplo 5
>Sea $X$ una variable que tiene densidad exponencial con parámetro $\lambda$. Encuentre la densidad de $Y = X^{1/\beta}$, con $\beta \neq 0$
>-  Si $X$ tiene distribución exponencial de parámetro $\lambda$ entonces su densidad es $f_X ( x ) = \lambda e ^{− λ x}$ , si $x > 0$ , y cero si no.
>- Supongamos $\beta > 0$, entonces $g(x) = x^{\beta}$ es una función creciente y si $y > 0$
$$P(Y \leq y) = P(X^{1/\beta} \leq y) = P(X \leq y^\beta) = F_X(y^\beta) = 1 - e^{-\lambda y^\beta}$$
>- entonces
$$f_Y(y) = F_X'(y) = \beta \lambda y^{\beta-1} e^{-\lambda y^\beta}$$

### Distribución exponencial de tasa $\lambda$
Variable Aleatoria $X$ ~ $\mathcal{E}(\lambda)$
Recordemos que se dice que una variable aleatoria $X$ tiene distribución Exponencial con tasa $\lambda$, $X$ ~ $\mathcal{E}(\lambda)$, si función densidad de probabilidad es
$$f_X(x, \lambda) = \lambda \exp^{-\lambda x} = \frac{\lambda^1 x^{1-1} e^{-\lambda x}}{\Gamma(1)} \quad x > 0$$
por lo cual si $X$ tiene distribución exponencial de tasa $\lambda$, entonces también tiene distribución Gamma con parámetro de forma $\alpha = 1$ y tasa $\lambda$. Notación: $X$ ~ $\mathcal{E}(\lambda) = \Gamma(1,\lambda)$

**Propiedades**
1. Si $X$ ~ $\mathcal{E}(\lambda)$ entonces
$$ \mu = 1/\lambda \quad \sigma^2 = 1/\lambda^2 $$
2. 
$$ F_X(x) = \begin{cases} 1 - e^{-\lambda x} & \text{si } x \ge 0 \\ 0 & \text{si } x < 0 \end{cases} $$
3. Si $t ≥ 0$ entonces $P(X \geq t + t_0|X ≥ t)$ para todo $t > 0$
4.  Si tenemos varias variables exponenciales $X_i$ ~ $\mathcal{E}(\lambda_i)$ para las cuales los eventos $(X_i > x)$ son independientes entre si, entonces
$$P[\min(X_1, \dots, X_n) > x] = e^{-\sum_{i=1}^n \lambda_i x}$$
Por lo cual, la variable $X = min(X_1, · · · , X_n)$ tiene distribución exponencial con tasa$\sum_{i=1}^{n} \lambda_i$.
5. Si $X$ ~ $\mathcal{E}(\lambda)$ entonces para todo $c > 0$, la variable $cX$ ~ $\mathcal{E}(\frac{\lambda}{c})$

-  Esta distribución es muy utilizada para modelar, por ejemplo, el tiempo de vida o duración de determinados componentes.
- La propiedad enunciada en el item (3)  es conocida como carencia de memoria y puede entenderse como que no tiene en cuenta el efecto desgaste producido por el paso del tiempo.
- Existen otras distribuciones alternativas como la distribución Weilbull y la lognormal para modelar paso del tiempo que modelan otro tipo de decaimiento.
## Distribución Weibull
***
Se dice que una variable aleatoria $X$ tiene distribución Weibull con parámetros $\alpha$ y $\beta$ si su función densidad de probabilidad es
$$f_X(x, \alpha, \beta) = \begin{cases} \frac{\alpha}{\beta^\alpha} x^{\alpha-1} e^{-(\frac{x}{\beta})^\alpha} & \text{si } x \ge 0 \\ 0 & \text{en otro caso} \end{cases}$$
con $\alpha$ y $β$ números positivos. Notación $X$ ~ $W(α, β)$
-  Salvo cuando ambas coinciden con la exponencial (o en casos límite muy específicos), Weibull y Gamma son modelos diferentes.
- La distribución Weibull se usa mucho para la tasa de fallos o desgaste en ingeniería, y la distribución Gamma para tiempos de espera acumulados de varios eventos o variables asimétricas.

### Variable aleatoria Weibull
![[Pasted image 20260908221122.png|529]]

>[!info] Proposición
>Sea X una variable aleatoria con distribución Weibull con parámetros $α$ y $β$ entonces
>1. Si $α = 1$ entonces $W(1, β) = \mathcal{E}(1/β)$
>2. La función de distribución acumulada es
$$F(x) = \begin{cases} 1 - e^{-(\frac{x}{\beta})^\alpha} & \text{si } x > 0 \\ 0 & \text{en otro caso} \end{cases}$$
>3. $E(X) = βΓ(1 + \frac{1} {α}) y Var(X) = β^2[Γ(1 + \frac{2}{α}) − Γ(1 + \frac{1}{α})^{2}]$ con $α$ y $β$ números positivos.


## Distribución Weibull vs Gamma

- Las distribuciones Gamma y Weibull pueden verse como generalizaciones de la distribución exponencial.  Si miramos a la distribución exponencial como el tiempo de espera de un proceso de Poisson (tiempo de espera hasta que un evento ocurra si ese evento tiene igual probabilidad de ocurrir en cualquier intervalo) entonces la distribución $Γ(k,θ)$ describe el tiempo de espera hasta que k eventos independientes ocurran. 
- Por otro lado, la distribución Weibull describe efectivamente el tiempo de espera para que el evento ocurra si ese evento cambia su probabilidad de ocurrir con el tiempo. En este caso k describe cuán rápido es ese cambio. ■ Si descartamos las constantes de normalización vemos que la Weibull decae más rápidamente si k>1 o más lentamente si k<1
$$f_{\Gamma}(x) \propto x^{k-1} \exp\left(-\frac{x}{\theta}\right)$$ $$f_W(x) \propto x^{k-1} \exp\left(-\left(\frac{x}{\lambda}\right)^k\right)$$
