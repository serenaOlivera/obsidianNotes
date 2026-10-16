# Método de los momentos
---- 

1. Los momentos de X son $$M_1 = E(X), \dots, M_k = E(X^k)$$ supondremos que existen y son finitos.

2. Sea $X_1, \dots, X_n$ un muestreo aleatorio de $X$, con distribución $$p(x, \theta_1, \dots, \theta_k) \text{ con } (\theta_1, \dots, \theta_k) \in \mathbb{R}^k$$ Aquí p denota la densidad continua de X o la función de probabilidad discreta

3. Entonces el vector de momentos es una función de los $\theta_i$: $$(M_1, \dots, M_k) = g(\theta_1, \dots, \theta_k)$$
4. Denotamos $$\overline{M}_j = \frac{1}{n} \sum_{i=1}^n X_i^j$$los momentos muestrales.

>[!info] Método
El método de los momentos consiste en resolver el sistema de ecuaciones $$(\overline{M}_1, \dots, \overline{M}_k) = g(\hat{\theta}_1, \dots, \hat{\theta}_k)$$
Es decir, los estimadores $\hat{\theta}_i; i = 1; \dots; k$ están dados por $$(\hat{\theta}_1, \dots, \hat{\theta}_k) = g^{-1}(\overline{M}_1, \dots, \overline{M}_k)$$ 
>
Este sistema no tiene porque tener solución, ni ser única, pero sí en todas las aplicaciones que veremos en el curso.


>[!example] Ejemplo
>1. Por ejemplo, supongamos que $X_1; \dots; X_n$ es un muestreo aleatorio de $X$ que tiene densidad $$p(x, \theta) = (\theta + 1)x^\theta \quad x \in [0, 1]$$
>2. La esperanza de $X$ es entonces $$E(X) = (\theta + 1) \int_{0}^{1} x^{\theta+1} dx = \frac{\theta + 1}{\theta + 2}$$
>3. Esto quiere decir que la esperanza de $X$ es una función del parámetro $g(\theta)$; en este caso $$g(\theta) = \frac{\theta + 1}{\theta + 2}$$ 
>4. Planteando la ecuación de estimación y resolviendo queda $$\overline{X} = \frac{\hat{\theta} + 1}{\hat{\theta} + 2} \implies \hat{\theta} = \frac{1 - 2\overline{X}}{\overline{X} - 1}$$ y este es el estimador de momentos de $\theta$.


>[!example] Ejemplo
>1. Por ejemplo, supongamos que $X_1; \dots; X_n$ es un muestreo aleatorio de $X$ que tiene densidad $$f_X(x) = \begin{cases} \frac{1}{2} + \frac{\beta x^3}{2} & -1 \leq x \leq 1 \\ 0 & \text{en cualquier otro caso} \end{cases}$$ donde $\beta \in [-1, 1]$.
>2. La esperanza de $X$ es entonces $$E[X] = \int_{-\infty}^{\infty} x f_X(x) \, dx = \int_{-1}^{1} x \left( \frac{1}{2} + \frac{\beta x^3}{2} \right) \, dx =$$  $$\int_{-1}^{1} \frac{x}{2} dx + \int_{-1}^{1} \frac{\beta x^4}{2} dx \tag{1}$$  $$= 0 + \frac{\beta x^5}{25} \bigg|_{-1}^{1} = \frac{\beta}{5} \tag{2}$$
>3. Esto quiere decir que la esperanza de X es una función del parámetro $g(\beta)$; en este caso $$g(\beta) = \frac{\beta}{5}$$
>4. Planteando la ecuación de estimación y resolviendo queda $$X = \frac{\beta}{5} \implies \hat{\beta} = 5\overline{X}$$ y este es el estimador de momentos de $\beta$


>[!info] Verificar que el estimador es insesgado
>Un estimador es insesgado si su esperanza es igual al parámetro verdadero. Calculamos $E[\hat{\beta}]$: $$E[\hat{\beta}] = E[5\bar{X}] = 5E[\bar{X}].$$ Dado que $\overline{X}$ es la media muestral, tenemos: $$E[\bar{X}] = E[X] = \frac{\beta}{5}.$$ Por lo tanto: $$E[\hat{\beta}] = 5 \cdot \frac{\beta}{5} = \beta.$$Esto confirma que $\hat{\beta} = 5\overline{X}$ es un estimador insesgado para $\beta$.


# Estimación de máxima verosimilitud
---

- Sea $X_1; · · · ; X_n$ una muestra aleatoria de $X$, con distribución $$p(x, \theta_1, \cdots, \theta_k) \text{ con } (\theta_1, \cdots, \theta_k) \in \mathbb{R}^k$$ Aquí p denota la densidad continua de X o la función de probabilidad discreta.
  
- Queremos estimar el vector de parámetros desconocidos $(\theta_1, · · · , \theta_k)$ de la distribución.
- Definimos la función de verosimilitud de la muestra, esto es, la densidad conjunta de la muestra aleatoria en función del vector de parámetros, dejando fijo el conjunto de valores observados de la muestra. $$L(\theta_1, \cdots, \theta_k) = p(x_1, \cdots, x_n|\theta_1, \cdots, \theta_k) = \prod_{i=1}^{n} p(x_i|\theta_1, \cdots, \theta_k) \quad (1)$$
- La estimación de máxima verosimilitud (MV) es un método para encontrar los parámetros que mejor ajusten la función de densidad
  
- Suponga que se quiere estimar un sólo parámetro $\theta$, el estimador $\hat{\theta}$ de máxima verosimilitud es el valor de $\theta$ que maximiza la verosimilitud $L(\theta)$, esto es $$ \hat{\theta} = \arg \max_{\theta} \prod_{i=1}^{n} p(x_i|\theta)$$
- Ese estadístico también realiza el máximo de la función de log-verosimilitud $\ell(\theta) \equiv \ln p(x_1, \dots, x_n|\theta)$, esto es $$\hat{\theta} = \arg \max_{\theta} \sum_{i=1}^{n} \ln p(x_i|\theta)$$

![[Pasted image 20261013204251.png]]
a)  Puntos en una dimensión tomados de una distribución Gaussiana con varianza  específica y media desconocida. Se muestran cuatro de un número infinito de distribuciones fuente candidatas. 
b) Verosimilitud (curva negra) y log-verosimilitud (curva roja) en función de la media. El valor que maximiza la verosimilitud es señalado con $\theta$ .

- Generalizando la verosimilitud como una función de los $k$ parámetros desconocidos $\theta  = (\theta_1, . . . , \theta_k)$; el estimador vectorial de máxima verosimilitud es el vector $\hat{\theta} = (\hat{\theta_1}, . . . , \hat{\theta_k})$ que maximiza la $\ell(\theta) ≡ \ln p(x|\theta)$  $$\hat{\theta} = \arg \max_{\theta} \sum_{i=1}^{n} \ln p(x_i | \theta)$$
- En la mayoría de los casos, esto se reduce a resolver la ecuación $$\nabla_{\theta} \mathcal{L}(\theta) = \sum_{i=1}^{n} \nabla_{\theta} \ln p(x_i | \theta) = 0$$donde el operador gradiente es

$$ \nabla_{\theta} \equiv \left[ \frac{\partial}{\partial \theta_1}, \dots, \frac{\partial}{\partial \theta_k} \right]^T $$
>[!info] Principio de Invarianza
Si $\hat{\theta}$ es el estimador de máxima verosimilitud de $\theta$, entonces $h(\hat{\theta})$ es el estimador de máxima verosimilitud de $h(\theta)$.

**Observación**
- En general, cuando la función de verosimilitud es diferenciable en el parámetro $\theta$, para calcular $\hat{\theta}$ derivamos $\ell_{n}(\theta)$ respecto de $\theta$ e igualamos a cero.
- En general se trata siempre de un máximo, aunque para verificarlo deberíamos calcular el signo de la derivada segunda $\ell_{n}''(\theta)$ y ver que es negativo.
- Cuando $L_n(\theta)$ no es diferenciable, cosa que sucede típicamente cuando el dominio de $L_n(\theta)$ depende de $\theta$, hallar en dónde se da el máximo es más difícil y no se puede hacer derivando.

>[!example] Ejemplo: Caso Bernoulli
Supongamos que $X_1, . . ., X_n \sim Ber(p)$. El logaritmo de la función de verosimilitud es $$\ell_n(p) = \sum_{i=1}^{n} X_i \ln(p) + (1 - X_i) \ln(1 - p)$$ de donde vemos que $$\begin{cases} \ell_n'(p) = n \left[ \frac{\bar{X}_n}{p} - \frac{1 - \bar{X}_n}{1 - p} \right] \\ \ell_n''(p) = -n \left[ \frac{\bar{X}_n}{p^2} + \frac{1 - \bar{X}_n}{(1 - p)^2} \right] \end{cases}$$
Notar que $\ell_n''(p) < 0$ para todo $p \in (0, 1)$, por lo que el punto crítico es un máximo. Se puede deducir entonces que $T_n = \bar{X}_n$. Es decir, el estimador de máxima verosimilitud es el promedio.


>[!example] Ejemplo: Caso Uniforme
  >- Supongamos que $X_1, . . . , X_n \sim U (0, \theta)$. La función de verosimilitud no es continua, y está dada por $$L_n(\theta) = \begin{cases} \frac{1}{\theta^n} & \text{si } X_i < \theta \forall i \\ 0 & \text{si no.} \end{cases}$$
  >- Decir que $X_i < \theta$ para todo $i$ es equivalente a decir que $\max_{i} X_i < \theta$. Entonces podemos reescribir la función de verosimilitud como $$L_n(\theta) = \begin{cases} \frac{1}{\theta^n} & \text{si } \max_i X_i < \theta \\ 0 & \text{si no.} \end{cases}$$
  >- Es claro que el máximo se da en $T_n = \max_i X_i$, que es por lo tanto el estimador de máxima verosimilitud de $\theta$.

![[Pasted image 20261013211214.png|423]]

>[!info] $U [0, \theta]$
El estimador de máxima verosimilitud de $\theta$ es sesgado.
>- Supongamos que tenemos $n$ variables aleatorias $X_1, X_2, . . ., X_n$ que son iid y distribuidas uniformemente en $[0, \theta]$.
>- La CDF de cada $X_i$ es: $$F_X(x) = \begin{cases} 0 & \text{si } x < 0 \\ \frac{x}{\theta} & \text{si } 0 \leq x \leq \theta \\ 1 & \text{si } x > \theta \end{cases}$$
>- Definimos el máximo de la muestra como $M = max(X_1, X_2, . . ., X_n)$.
>- La CDF del máximo se puede calcular como: $$\begin{align*} F_M(m) &= P(M \le m) = P(X_1 \le m, X_2 \le m, \dots, X_n \le m) \\ &= P(X_1 \le m)^n \\
&= (F_X(m))^n \end{align*}$$ Para $0 \le m \le \theta$: $$F_M(m) = \left(\frac{m}{\theta}\right)^n$$
>- Para encontrar la función de densidad del máximo, derivamos la CDF: $$\begin{align*} f_M(m) &= \frac{d}{dm} F_M(m) \\ &= \frac{d}{dm} \left(\frac{m}{\theta}\right)^n \\ &= \frac{n}{\theta^n} m^{n-1} \end{align*}$$ para $0 \le m \le \theta$.
>  
>- Para determinar si el estimador del máximo $M = max(X_1, X_2, . . ., X_n)$ de una muestra de variables aleatorias $X_i$ uniformes en el intervalo $[0, \theta]$ es insesgado, debemos calcular su valor esperado $E[M]$ y compararlo con $\theta$.
>- Usamos la función de densidad del máximo: $$E[M] = \int_{0}^{\theta} m \cdot f_M(m) \, dm = \int_{0}^{\theta} m \cdot \frac{n}{\theta^n} m^{n-1} \, dm = \frac{n}{\theta^n} \int_{0}^{\theta} m^n \, dm$$
>- La integral $\int_{0}^{\theta} m^{n} dm$ se evalúa como: $$\int_{0}^{\theta} m^{n} dm = \left[ \frac{m^{n+1}}{n+1} \right]_{0}^{\theta} = \frac{\theta^{n+1}}{n+1}$$
>- Sustituyendo en la expresión para $E[M]$: $$E[M] = \frac{n}{\theta^n} \cdot \frac{\theta^{n+1}}{n+1} = \frac{n\theta}{n+1}$$
>- Vemos que: $$E[M] = \frac{n\theta}{n+1}$$ Esto implica que $E[M]$ no es igual a $\theta$, lo que significa que el estimador $M$ es sesgado.
>
>- Para que sea insesgado, podemos considerar un estimador corregido, por ejemplo,  $\hat{\theta}= \frac{n + 1} {n} M$ , que tiene un valor esperado: $$E[\hat{\theta}] = E\left[\frac{n+1}{n}M\right] = \frac{n+1}{n}E[M] = \frac{n+1}{n} \cdot \frac{n\theta}{n+1} = \theta$$ Por lo tanto, el máximo $M$ es sesgado, pero el estimador$\hat{\theta} = \frac{n+1} {n} M$ es insesgado.



>[!example] Ejemplo: Caso uniforme  $U [θ, 1]$
Sea $X_1, . . . , X_n$ una muestra aleatoria de una distribución uniforme en el intervalo $[\theta, 1]$ con $\theta > 0$. Veamos que el estimador de máxima verosimilitud de $\theta$ es $\hat{\theta} = \min(X_i)$.
>- Dada una muestra aleatoria $X_1, . . . , X_n \sim Unif[\theta, 1]$ con $\theta > 0$, la función de densidad para cada $X_i$ es: $$f_X(x; \theta) = \frac{1}{1-\theta} \cdot \mathbb{I}_{[\theta,1]}(x)$$
>- La función de verosimilitud de la muestra es el producto de las densidades individuales:
$$L(\theta) = \prod_{i=1}^{n} \frac{1}{1-\theta} \mathbb{I}_{[\theta,1]}(x_i) = \frac{1}{(1-\theta)^n} \mathbb{I}_{\{\theta \leq \min(x_i), \max(x_i) \leq 1\}}$$
>- Para que $L(\theta) > 0$, se debe cumplir que $\theta ≤ \min(X_i)$.
>- Como la función $L(\theta) = \frac{1}{(1-\theta)^n}$ es estrictamente creciente con respecto a $\theta$ en el intervalo $(0, \min(X_i)]$, alcanza su valor máximo en el límite superior del dominio permitido para $\theta$: $$\hat{\theta} = \min(X_i)$$


¿Cual es la distribución acumulada de $\hat{\theta}$? ¿ y la densidad de $\hat{\theta}$?.
- Para cada $X_i \sim Unif[\theta, 1]$, la densidad y la distribución acumulada son: $$\begin{align*} f_X(x) &= \frac{1}{1-\theta} \text{ para } \theta \le x \le 1 \\ F_X(x) &= \frac{x-\theta}{1-\theta} \text{ para } \theta \le x \le 1 \end{align*}$$
- Sea $Y = \hat{\theta} = \min(X_i)$. Calculamos primero $P(Y > y)$: $$P(Y > y) = P(\min(X_1, \ldots, X_n) > y) = \prod_{i=1}^{n} P(X_i > y) = (1 - F_X(y))^n$$
- Sustituyendo $$1-F_X(y)=1-\frac{y-\theta}{1-\theta}=\frac{1-y}{1-\theta}$$ resulta $$P(Y>y)=(1-F_X(y))^n=(\frac{1-y}{1-\theta})^n$$  si $\theta \leq y \leq 1$.
- Función de distribución acumulada $(F_{\hat{\theta}}(y)=1-P(Y>y))$:
$$F_{\hat{\theta}}(y) = \begin{cases} 0 & \text{si } y < \theta \\ 1 - \left(\frac{1-y}{1-\theta}\right)^n & \text{si } \theta \leq y \leq 1 \\ 1 & \text{si } y > 1 \end{cases}$$
- Función de densidad de probabilidad $(f_{\hat{\theta}}(y)=\frac{d}{dy} F_{\hat{\theta}}(y))$:

$$f_{\hat{\theta}}(y) = \frac{n(1-y)^{n-1}}{(1-\theta)^n} \quad \text{para } \theta \leq y \leq 1$$
>[!info] El estimador de máxima verosimilitud de $\theta$ es sesgado, pero que $(n + 1) \hat{\theta}/n$ es insesgado.
>- Calculamos el valor esperado de $\hat{\theta}$: $$E[\hat{\theta}] = \int_{\theta}^{1} y \cdot \frac{n(1-y)^{n-1}}{(1-\theta)^n} \, dy$$
>- Haciendo la sustitución $u=1-y$. Entonces, $dy=-du$; si $y=\theta \implies u=1-\theta$, si $y=1 \implies u=0$: $$E[\hat{\theta}] = \int_{0}^{1-\theta} (1-u) \cdot \frac{nu^{n-1}}{(1-\theta)^n} \, du = \frac{n}{(1-\theta)^n} \left[ \int_{0}^{1-\theta} u^{n-1} \, du - \int_{0}^{1-\theta} u^n \, du \right]$$
>- Entonces $$\begin{align*}
E[\hat{\theta}] &= \frac{n}{(1-\theta)^n} \left[ \frac{(1-\theta)^n}{n} - \frac{(1-\theta)^{n+1}}{n+1} \right] \\
&= 1 - \frac{n}{n+1}(1-\theta) \\
&= \frac{n\theta+1}{n+1}
\end{align*}$$
>- Sesgo de $\hat{\theta}$: $$\text{Sesgo}(\hat{\theta}) = E[\hat{\theta}] - \theta = \frac{n\theta + 1}{n + 1} - \theta = \frac{1 - \theta}{n + 1} \neq 0$$
>- Dado que $\theta < 1$, el sesgo es positivo, por lo que el estimador de máxima verosimilitud es sesgado.


>[!info] El estimador $\tilde{\theta} = \frac{(n+1)\hat{\theta}-1}{n}$ es insesgado 
>$$\begin{align*} E\left[\frac{(n+1)\hat{\theta}-1}{n}\right] &= \frac{(n+1)E[\hat{\theta}]-1}{n} \\
&= \frac{(n+1)\left(\frac{n\theta+1}{n+1}\right)-1}{n} \\
&= \frac{n\theta+1-1}{n} = \theta
\end{align*}$$

>[!info] El estimador $2 \overline{X}-1$ es un estimador insesgado para $\theta$.
>-  Para una variable $X_i \sim U[\theta, 1]$, la esperanza teórica es el punto medio del intervalo: $$E[X_i] = \frac{\theta + 1}{2}$$
>- Por lo tanto, la combinación lineal insesgada basada en la media es $$E[\bar{X}] = \frac{\theta + 1}{2}$$ 
>- Por lo tanto, la combinación lineal insesgada basada en la media es $\hat{\theta}_2 = 2\bar{X} - 1$: $$E[2\bar{X} - 1] = 2E[\bar{X}] - 1 = 2\left(\frac{\theta + 1}{2}\right) - 1 = \theta$$


**¿Cual es el mejor Estimador?**

- Para elegir entre los dos estimadores inesegados, comparamos sus varianzas:
- Varianza de $\hat{\theta_2}  = 2 \overline{X} − 1$:

$$ \text{Var}(X_i) = \frac{(1-\theta)^2}{12} \implies \text{Var}(\bar{X}) = \frac{(1-\theta)^2}{12n} $$

$$ \text{Var}(\hat{\theta}_2) = 4\text{Var}(\bar{X}) = \frac{(1-\theta)^2}{3n} = O\left(\frac{1}{n}\right) $$

- Varianza del estimador basado en el mínimo $\tilde{\theta}$ : Calculando $E[\hat{\theta}^2]$ se obtiene que $Var(\tilde{\theta})$ disminuye a una tasa de $O (\frac{1}{n^2})$.

>[!tip] Conclusión:
Se elige el estimador corregido basado en el mínimo $\tilde{\theta} = \frac {(n+1) \min(X_i)−1}{n}$  porque su varianza es significativamente menor para cualquier tamaño  muestral $n > 1$, lo que lo convierte en un estimador más eficiente (menor  Error Cuadrático Medio).

