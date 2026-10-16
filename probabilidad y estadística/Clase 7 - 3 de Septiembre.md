>[!example] Ejemplo 
>Es usual modelar el número de autos que entra al estacionamiento de un aeropuerto con una distribución de Poisson. ¿Qué distribución tendría el tiempo hasta el primer arribo?
>![[Pasted image 20260906201842.png]]
>Esta es una variable aleatoria, pero de diferente tipo. Puede valer 10 minutos, 3 minutos 8 segundos, 1 minuto 20s segundos, $\sqrt{2}$ minuto o $\pi$ minutos.
 En realidad, cualquier número mayor que cero puede ser un valor posible de una variable relacionada con el TIEMPO.
 >
 >Para ser concretos, si el número de autos es Poisson con media λ = 0.8 autos POR MINUTO, representemos el tiempo hasta el primer arribo con la variable T. Podemos calcular la probabilidad de que el primer auto llegue después de dos minutos reescribiendo esta probabilidad en términos del número de arribos
$$P(T > 2) = P(0 \text{ autos entre } 0 \text{ y } 2 \text{ minutos})$$
>
>Sabemos que Y el número de autos entre 0 y 2 minutos tiene distribución Poisson (μ = 0.8 × 2) por lo cual podemos evaluar la función de masa de Y en x = 0
>$$\begin{align*}
P(T > 2) &= P(0 \text{ autos entre } 0 \text{ y } 2 \text{ minutos}) \\
&= e^{-0.8 \cdot 2} \frac{(0.8 \cdot 2)^0}{0!} \\
&= e^{-1.6} \approx .202.
\end{align*}$$
>
Tambien podemos calcular la probabilidad que el primer auto en llegar este entre 2 y 3 minutos, como $$P(2 < T < 3) = P(T > 2) - P(T > 3)$$
  Calculamos $P(T > 3)$ en la misma forma que calculamos $P(T > 2)$ arriba
$$P(T > 3) = e^{-0.8 \cdot 3} \frac{(0.8 \cdot 3)^0}{0!} = e^{-2.4} \approx .091.$$
Por lo cual
$$P(2 < T < 3) = e^{-1.6} - e^{-2.4} \approx .111.$$

**Observación:** Si bien calculamos probabilidades específicas acerca de T ,¿Cómo podemos describir su distribución? En particular:
1. ¿Cuál es su función de distribución acumulada?
2. Cual es su función de densidad?

Recordemos que la función de distribución acumulada se define como
$$F(t) = P(T \leq t) = 1 - P(T > t).$$
Supongamos ahora que el número de arribos en $[0, t]$ tiene distribución Poisson con media $\mu = 0.8t$. Como vimos antes, la probabilidad de que no arribe ningún auto en ese intervalo es $$ \begin{aligned} P(T > t) &= P(\text{Ningun auto llega hasta el tiempo } t) \\ &= e^{-0.8 \cdot t} \frac{(0.8 \cdot t)^0}{0!} \\ &= e^{-0.8t}. \end{aligned} $$
$\text{con } t \geq 0$
Por otra parte, el tiempo es siempre positivo, por lo cual si $(t < 0)$,
$$P(T > t) = 1$$Poniendo todo junto queda
$$F(t) = 1 - P(T > t) = \begin{cases} 1 - e^{-0.8t} & t \geq 0 \\ 0 & t < 0 \end{cases}$$![[Pasted image 20260906204621.png|500]]

>[!tip] Distribuciones acumuladas
>![[Pasted image 20260906204745.png]]


## Definición de variable contínua
****

Una variable aleatoria se llama continua si su función de distribución acumulada es una función continua.

>[!example] Ejemplo: ¿Cuál es la probabilidad de $P(T = 2)$?
>Consideremos la probabilidad de que el primer arribo sea en el intervalo $(2-\epsilon,2+\epsilon)$. Esta probabilidad va a ser siempre mayor que $P(T=2)$ porque el intervalo contiene mas puntos.
Poisson con parámetro $\mu = 0.8 \times 2\epsilon$ por lo cual$$
\begin{align*}
P(\text{al menos un arribo en el intervalo}) &= 1 - P(\text{ningún arribo en el intervalo}) \\
&= 1 - e^{-0.8 \cdot 2\epsilon} \frac{(0.8 \cdot 2\epsilon)^0}{0!} \\
&= 1 - e^{-1.6\epsilon}.
\end{align*}$$
>
Si hacemos a $\epsilon$ arbitrariamente chico, $e^{-1.6\epsilon}$ es cada vez mas cercana a uno y la probabilidad de que el primer arribo sea exactamente en 2 minutos es cero.

## Densidad de probabilidad 
**** 

Se dice que f es una **densidad de probabilidad** de la variable X con distribución F si se cumple que $f \geq 0$ y $$F(t) = \int_{-\infty}^{t} f(x)dx$$
### Propiedades
-  La densidad f no es única.
- En los puntos donde F es derivable, $f(t) = F'(t)$ es una densidad.
- Si f es una función no negativa tal que $$1 = \int_{-\infty}^{\infty} f(x) dx$$
  entonces f es una densidad para la distribución F $$F(t) = \int_{-\infty}^{t} f(x) dx$$

>[!example] Ejemplo: función de densidad y función de distriubución
>En el ejemplo del tiempo de arribo del primer auto, vimos que
$$F(t) = \begin{cases} 1 - e^{-0.8t} & t \geq 0 \\ 0 & t < 0 \end{cases}.$$
Entonces, derivando para $t > 0$ y $t < 0$, podemos definir una densidad como
$$f(t) = F'(t) = \begin{cases} 0.8e^{-0.8t} & t \ge 0 \\ 0 & t < 0 \end{cases}$$
>![[Pasted image 20260906205816.png]]


### Propiedades
Si X es una variable continua con distribución $F$ y densidad $f$, entonces
$$P(a \leq X \leq b) = \int_a^b f(x)dx$$
pues
$$P(a < X \leq b) = P(X \leq b) - P(X \leq a) = F(b) - F(a) = \int_a^b f(x)dx$$
$$P(a \leq X \leq b) = P(a < X < b) = P(a \leq X < b) = P(a < X \leq b)$$![[Pasted image 20260906210118.png]]

$$P(2<T<3)=\int_{2}^{3}f(t)\,dt=\int_{2}^{3}0.8e^{-0.8t}\,dt=.111,$$
$$P(T>2)=\int_{2}^{\infty}f(t)\,dt=\int_{2}^{\infty}0.8e^{-0.8t}\,dt=.202.$$

>[!example] Ejemplo
>Sea $g$ la siguiente función.
$$g(x) = \begin{cases} x(1-x) & 0 \le x \le 1 \\ 0 & \text{en otro caso} \end{cases}$$
Encuentre una función densidad $f_X$ que coincida con g salvo una constante.
>
>**Resolución:**
>La función densidad debe ser no negativa y tener integral igual a 1, por lo cual una candidata es $$f(x) = \frac{1}{c}g(x) \quad c = \int_{-\infty}^{\infty} g(x)dx$$
>Entonces
$$c = \int_{-\infty}^{\infty} g(x)dx = \int_{0}^{1} x(1-x)dx = \left(\frac{x^2}{2} - \frac{x^3}{3}\right)\bigg|_{0}^{1} = \frac{1}{6}$$
y la densidad $f_X$ resulta $$f_X(x) = \begin{cases} 6x(1-x) & 0 \le x \le 1 \\ 0 & \text{en otro caso} \end{cases}$$

>[!example] Otro ejemplo :)
> Calcular la función de distribución de la variable aleatoria $X$ con función de densidad
$$f_X(x) = \begin{cases} \frac{x}{2} & x \in (0, 1] \\ \frac{3}{4} & x \in (1, 2) \\ 0 & x \notin (0, 2). \end{cases}$$
>A partir de la expresión $F_X(x) = \int_{-\infty}^{x} f_X(t)dt$, calculamos la función de distribución por trozos:
>- Si $x < 0$, $f_X(t) = 0$, $\forall t \in (-\infty, x]$ y, por tanto, $F_X(x) = 0$.
>- Si  $x \ge 0$, puesto que $f_X(t) = 0$, $\forall t \in (-\infty, 0]$, se tiene $F_X(x) = \int_0^x f_X(t)dt$; así:
$$ \cdot \text{ Si } 0 \le x < 1, \quad F_X(x) = \int_0^x \frac{t}{2} dt = \frac{x^2}{4}.$$
$$ \cdot \text{ Si } 1 \le x < 2, \quad F_X(x) = \int_0^1 \frac{t}{2} dt + \int_1^x \frac{3}{4} dt = \frac{1}{4} + \frac{3(x-1)}{4}.$$
$$\cdot \text{ Si } x \ge 2, \quad F_X(x) = \int_0^1 \frac{t}{2} dt + \int_1^2 \frac{3}{4} dt + \int_2^x 0 dt = \frac{1}{4} + \frac{3}{4} = 1.$$
>$$ F_X(x)=
\left\{
>\begin{array}{ll}
>0 \ \ \ x \in(-\infty, 0) \\\ 
>\frac{x²}{4} \ \ \ x \in [0, 1) \\\
>\frac{3x-2}{4} \ \ \ x \in [1,2) \\\
>1 \ \ \ \ x \in [2, +\infty)
>\end{array}
>\right.
>$$
>![[Pasted image 20260906211737.png]]


>[!example] Un ejemplo más...
>Calcular la función de densidad de una variable aleatoria con función de distribución
>$$F_X(x) =
\begin{cases}
0 & x \in (-\infty, 0) \\
\frac{x^2}{4} & x \in [0, 1) \\
\frac{1}{4} & x \in [1, 2) \\
\frac{3x^2 - 7}{20} & x \in [2, 3) \\
1 & x \in [3, +\infty).
\end{cases}$$
>![[Pasted image 20260906211933.png]]
>Observamos que esta función es continua y, además, derivable en $\mathbb{R} - \{0, 1, 2, 3\}$.
>Por lo tanto, $F_X$ puede expresarse como $F_X(x) = \int_{-\infty}^x f_X(t)dt$, $\forall x \in \mathbb{R}$, sin más que definir
$$f_X(x) = \frac{dF_X(x)}{dx}, \quad \forall x \in \mathbb{R} - \{0, 1, 2, 3\}$$
y con valores arbitrarios en el conjunto $\{0, 1, 2, 3\}$.
Entonces, la variable $X$ es de tipo continuo, y su función de densidad es
$$f_X(x) = \begin{cases} \frac{x}{2} & x \in (0, 1) \\ \frac{3x}{10} & x \in (2, 3) \\ 0 & x \notin (0, 1) \cup (2, 3). \end{cases}$$
La función de densidad de una variable continua tiene un papel similar al de la función masa de probabilidad de una variable discreta. De hecho, al determinar la función de distribución, determina también la distribución de probabilidad de la variable.

At this point, de tantos ejemplos que hay si no entendés, ya es kind of your fault reina.... just saying

>[!example] Ejemplo!!
Sea X una variable aleatoria continua con densidad $f$ y sean $a$ y $b \neq 0$ números reales, entonces la variable $Y = a + bX$ tiene densidad
$$f_Y(y) = \frac{1}{|b|} f\left(\frac{y-a}{b}\right)$$y $f_Y(y) = 0$ en otro lado.
Supongamos que $b > 0$, entonces $g(y) = \frac{y−a}{b}$ es una función creciente y $$P(Y \leq y) = P(X \leq \frac{y − a}{b} ) = F_X ( \frac{y − a}{b} )$$ por lo cual $$f_Y ( y ) = \frac{1}{b} f ( \frac{y − a}{b} )$$
>Si $b < 0$, entonces $g(y) = \frac{y−a} {b}$ es una función decreciente y
$$P(Y \leq y) = P(X \geq \frac{y-a}{b}) = 1 - F_X(\frac{y-a}{b})$$ por lo cual
$$f_Y(y) = -\frac{1}{b}f\left(\frac{y-a}{b}\right)$$
>Resumiendo, si $b \neq 0$
$$f_Y(y) = \frac{1}{|b|} f\left(\frac{y-a}{b}\right)$$


## Dsitribución condicional
***
Si A y B son subconjuntos de R x entonces
$$P(X \in A / X \in B) = \frac{P(X \in A \cap B)}{P(X \in B)} = \frac{\int_{A \cap B} f(y) dy}{\int_B f(y) dy}$$
## Esperanza y Varianza
***
**Observación:** Recordemos que si $X$ era una variable aleatoria discreta, tal que $\sum_x |x|p_X(x) <\infty$ entonces $X$ tenía esperanza y$$E(X) = \sum_{x} x p_X(x)$$
En forma análoga, definimos esperanza de variables aleatorias continuas de la siguiente forma.

>[!info] Definición de esperanza, varianza y desviación estandar
>Sea $X$ un variable aleatoria continua con densidad $f$. Decimos que $X$ tiene esperanza finita si $$ \int_{-\infty}^{\infty} |x| f(x) dx < \infty$$y en ese caso se define la **esperanza** como
$$ E(X) = \int_{-\infty}^{\infty} x f(x) dx < \infty $$
y la **varianza** como
$$ V(X) = E[(X - E(X))^2] = E(X^2) - E(X)^2 $$
La **desviación estándar** es la raíz cuadrada positiva de la varianza, $\sigma = \sqrt{V(X)}$.

### Propiedades: 
Sea X un variable aleatoria continua sobre $(\Omega, A, P)$ con densidad de probabilidad $f$ y $E(X^2) < \infty$, entonces
1. $0 \leq V(X) = E(X^2) − \mu^2$ donde $\mu = E(X)$.
2. $E(aX + b) = aE(X) + b$ y $V(aX + b) = a^2V(X)$ , para todo $a, b \in \mathbb{R}$
3. Si $h(X)$ es una variable aleatoria continua, entonces
$$E(h(X)) = \int_{-\infty}^{\infty} h(x)f(x)dx$$
siempre que$$\int_{-\infty}^{\infty} |h(x)| f(x) dx < \infty$$

>[!info] Cuantiles 
> 1. Sea $p \in (0, 1)$ y sea $X$ una variable aleatoria continua sobre $(\Omega, A, P)$ con función de distribución acumulada $F$ entonces se llama cuantil $p$ de $X$ al valor $\eta(p)$ tal que $$p = F(\eta(p))$$
> 2. Si $f$ es una función de densidad de $X$, entonces $$p = F(\eta(p)) = \int_{-\infty}^{\eta(p)} f(t)dt$$
> ![[Pasted image 20260906213951.png]]


### Propiedades
Los cuantiles suelen usarse por grupos que dividen la distribución en partes iguales; entendidas estas como intervalos que comprenden la misma proporción de valores. Los más usados son:
1. Los cuartiles, que dividen a la distribución en cuatro partes (corresponden a los cuantiles 0,25; 0,50 y 0,75);
2. Los quintiles, que dividen a la distribución en cinco partes (corresponden a los cuantiles 0,20; 0,40; 0,60 y 0,80);
3. Los deciles, que dividen a la distribución en diez partes;
4. Los percentiles, que dividen a la distribución en cien partes.

>[!example] Ejemplo: ¿Cuál es el cuantil de p=0.15866? ¿Y de p=0.84134?
>![[Pasted image 20260906214141.png]]

**Propiedad**
Sea $X$ una variable aleatoria continua con función de distribución acumulada $F$, y sea $\eta_X(p)$ el cuantil $p$ de $X$, con $p \in [0; 1]$. Si $Y = aX + b$ con $a  \neq 0$ y $b \in \mathbb{R}$, entonces $$ \eta_Y(p) = \begin{cases} a\eta_X(p) + b & \text{si } a > 0 \\ a\eta_X(1-p) + b & \text{si } a < 0 \end{cases}$$
