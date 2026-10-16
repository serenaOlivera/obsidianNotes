
>[!warning] ESTA CLASE ES SUPER IMPORTANTE PARA MODELOS Y SIMULACIÓN DE REPASO
>(la cursas en primer cuatri de 2027)



## El modelo de una población
- Este modelo se basa en la noción de población y muestreo
- Imaginemos una población muy grande, cuyos individuos son entidades generales
- Nos interesan atributos medibles de esos individuos
- Sea $X$ un atributo medido sobre un individuo elegido al azar de una población. Entonces $X$ es una variable aleatoria.

>[!info] Definición
Una población queda definida por una o varias variables aleatorias y su distribución conjunta.

>[!example] Ejemplo
>Supongamos tener una población de tapitas de gaseosa. Y observamos su diámetro. Cada punto representa una tapita muestreada de la población. Un modelo paramétrico consiste en suponer la fórmula de $p(x)$ conocida, excepto por algunos parámetros. Por ejemplo, podemos suponer que es $N( \mu , \sigma ^2 )$ ![[Pasted image 20261001203646.png]]


 >[!example] Parámetros - Definición
En un modelo paramétrico, los parámetros son los valores que determinan la densidad de la población p(x) de la variable aleatoria medida en el modelo.
>- Denotaremos un parámetro general por la letra $\theta$, y la densidad correspondiente por $p(x; \theta)$.
>- Si el modelo es discreto $p(x; \theta)$ denota la función de probabilidad puntual.
>- En este estadio de nuestro estudio, los parámetros son los únicos valores desconocidos de la densidad (función de frecuencia) marginal o conjunta.

>[!info] Estimación Puntual
Como no conocemos los parámetros de la población, el problema central es como estimarlos.
**Definición**
Sea $X_1, . . . , X_n$ una muestra aleatoria con distribución que depende de un parámetro $\theta$, desconocido. Entonces se dice que la función de la muestra
$$ \hat{\theta} = h(X_1, \dots, X_n) $$ es un estimador puntual de $\theta$ si $\hat{\theta}$ es una variable aleatoria.
**Estimador**
Cualquier función continua de una muestra es una variable aleatoria, por lo cual estimadores hay muchos. ¿Que significa entonces estimar?



## Muestreo aleatorio

>[!info] Muestra
Una muestra es un subconjunto de observaciones seleccionadas de una población mediante un proceso aleatorio. En general, denotamos una muestra de tamaño $n$ por letras minúsculas: $x_1, . . . , x_n$.

>[!info] Muestra aleatoria
Una muestra aleatoria es un vector de variables aleatorias independientes e idénticamente distribuidas que modela el proceso de muestreo aleatorio de la población. En general, denotamos una muestra aleatoria de tamaño $n$ por letras mayúsculas: $X_1, . . . , X_n$.

>[!example]  Ejemplo Muestreo Aleatorio
>1. Población de tapitas en función de su diámetro. Cada punto representa una tapita de la población.
>2. En rojo una muestra de 10 tapitas de la población.
>3. Media Muestral $$ \overline{X} = \frac{1}{n} \sum_{i=1}^{n} X_i $$
>4. Media Muestral Observada $$ \overline{x} = \frac{1}{n} \sum_{i=1}^{n} x_i $$ ![[Pasted image 20261001211320.png]]

![[Pasted image 20261001211347.png]]

## Observación
- Es importante distinguir entre el valor observado de un estimador y el estimador en sí.
- Para dejar en claro la diferencia, el valor observado de un estimador lo llamaremos estimación.
- Por ejemplo, en el caso de las tapitas, una estimación de $\mu$ es $\overline{x} = 2.98$, pero el estimador es $\overline{X}_{10}$.
- Este segundo es una variable aleatoria, mientras que el primero es un número.

>[!info] Sesgo
Puede haber varios estimadores razonables para un mismo parámetro $\theta$. Supongamos que queremos saber qué hora es ahora mismo. Si disponemos de varios relojes, ¿qué reloj es mejor? 
**Criterios**
>- Exactitud: ¿está nuestro reloj en hora? ¿o está atrasado/adelantado?
>- Precisión: ¿marca nuestro reloj los segundos? ¿o se limita a marcar los minutos?C
>Cuando se trata de un estimador, la primer propiedad refiere al sesgo y la segunda a la varianza
>![[Pasted image 20261001211639.png]]


## Criterios de bondad de un estimador
----
## Sesgo

Sea $X_1, . . . , X_n$ una muestra aleatoria con distribución que depende de un parámetro $\theta$, desconocido. Entonces se dice un estimador de $\theta$, $\hat{\theta} = h(X_1, . . . , X_n)$ es un estimador insesgado para $\theta$ si
$$E(\hat{\theta}) = \theta$$Si el estimador no es insesgado, entonces la diferencia

$$ \text{Sesgo}(\theta) = E(\hat{\theta}) - \theta $$

es conocida como sesgo del estimador $\hat{\theta}$.

## Sesgo asintótico

Sea $X_1, . . . , X_n$ una muestra aleatoria con distribución que depende de un parámetro $, desconocido. Entonces se dice un estimador de θ, ˆθ = h(X1, . . . , Xn) es un estimador asintóticamente insesgado del parámetro θ si

$$ \lim_{n \to \infty} E(\hat{\theta}) = \theta $$
Es decir, si Sesgo$(\theta) \rightarrow 0$ cuando $n \rightarrow \infty$.

>[!info] Proposición
Sea $X_1, . . ., X_n$ una muestra aleatoria tal que $E(X_i) = \mu$ y $Var(X_i) = \sigma ^2$ para todo $i = 1, . . ., n$. Entonces, definimos como $$ \overline{X} = \frac{1}{n} \sum_{i=1}^{n} X_i \qquad S_{n-1}^2 = \frac{1}{n-1} \sum_{i=1}^{n} (X_i - \overline{X})^2 $$ las variables aleatorias media muestral y varianza muestral.
a) $\overline{X}$ es un estimador insesgado para $\mu$
b) $S_{n−1} ^ 2$ es un estimador insesgado para $\sigma ^2$
 **Resolución** $$ \mathbf{E}(\bar{X}_n) = \mathbf{E}\left(\frac{1}{n} \sum_{i=1}^n X_i\right) = \frac{1}{n} \sum_{i=1}^n \mathbf{E}(X_i) = \frac{\mu + \cdots + \mu}{n} = \mu $$
Luego, $\bar{X}_n$ es un estimador insesgado de $\mu$. ¿Qué pasa con la varianza? Veamos si $\Sigma_n^2$ es un estimador insesgado de $\sigma^2$. Calculamos $$ \begin{aligned} \mathbf{E}(\Sigma_n^2) &= \mathbf{E}\left(\frac{1}{n} \sum_{i=1}^n (X_i - \bar{X}_n)^2\right) = \frac{1}{n} \sum_{i=1}^n \mathbf{E}\left((X_i - \bar{X}_n)^2\right) \\ &= \frac{1}{n} \sum_{i=1}^n \mathbf{E}(X_i^2) - 2\mathbf{E}(X_i \bar{X}_n) + \mathbf{E}(\bar{X}_n^2) \end{aligned} $$
>
Calculemos cada término por separado. Por un lado $$\begin{align*}
\mathbf{E}(X_i \bar{X}_n) &= \frac{1}{n} \sum_{j=1}^n \mathbf{E}(X_i X_j) = \frac{\mathbf{E}(X_i^2)}{n} + \frac{1}{n} \sum_{i \neq j} \mathbf{E}(X_i) \mathbf{E}(X_j) \\
&= \frac{\mu^2 + \sigma^2}{n} + \frac{n-1}{n} \mu^2 = \mu^2 + \frac{\sigma^2}{n}
\end{align*}$$ Por otro $$\mathbf{E}(\bar{X}_n^2) = \frac{1}{n^2} \sum_{i,j=1}^n \mathbf{E}(X_i X_j) = \frac{\mu^2 + \sigma^2}{n} + \frac{n-1}{n} \mu^2 = \mu^2 + \frac{\sigma^2}{n}$$ Juntando ambos cálculos obtenemos que $$\mathbf{E}(\Sigma_n^2) = \mu^2 + \sigma^2 - \mu^2 - \frac{\sigma^2}{n} = \frac{n-1}{n} \sigma^2$$
Vemos así que $\sum_{n}^{2}$ es un estimador sesgado de $\sigma^{2}$. El sesgo de $\sigma_{n}^{2}$ es $$ \text{Sesgo } (\Sigma_n^2) = -\frac{\sigma^2}{n} \to 0 $$ cuando $n \to \infty$. Entonces $\sum_{n}^{2}$ es un estimador asintóticamente insesgado para $\sigma^{2}$. Es por esto que se define $$ S_{n-1}^2 = \frac{1}{n-1} \sum_{i=1}^n (X_i - \overline{X})^2 = \frac{n}{n-1} \Sigma_n^2 $$ el cual si es insesgado para $\sigma^{2}$.


>[!example] Ejemplos
Consideremos que $X_1, . . . , X_n$ es una muestra aleatoria de las diferentes distribuciones planteadas en cada uno de los siguientes ítem. Veamos si son insegados.
>1. Distribución $Bernoulli(p)$ con $p \in (0; 1)$. Estimador: $\hat{p} = \overline{X}$.
>   2. Distribución $Poisson(\lambda)$ con $\lambda > 0$. Estimador: $\hat{\lambda} = \overline{X}$.
>   3. Distribución $N (\mu, \sigma^{2})$ con $\mu \in \mathbb{R}$ y $\sigma > 0$. Estimador: $\hat{\mu} = \overline{X}, \quad \hat{sigma}^{2} = S_{n−1}^{2}$.
>   4. Distribución $U[0, \theta]$ con $\theta > 0.$ Estimador 1: $\hat{\theta}_1 = 2 \overline{X}$; Estimador 2: $\hat{theta}_{2} = max(X_1, · · · , X_n)$.
> 
> - Los primeros tres casos se resuelven aplicando la proposición anterior, pues $\overline{X}$ y $S_{n-1}^{2}$ son insesgados. 
> - En el caso de la Distribución $U[0, \theta]$ con $\theta > 0$, el estimador 1 es el doble de la media muestral $\hat{\theta}_1 = 2 \overline{X}$.
> - Como la media muestral es insesgada con respecto a la esperanza $\mu$ y el parámetro $\theta = \mu/2$, resulta insesgado.
> - El estimador 2 es el máximo de la muestra, tengo que calcular su distribución acumulada, luego su densidad y recién puedo calcular su esperanza.

La distribución del máximo de una muestra aleatoria de variables independientes e idénticamente distribuidas (iid) de una distribución uniforme en el intervalo $[0, \theta]$ se puede derivar de la siguiente manera:

1. **Variables Aleatorias**: Supongamos que tenemos n variables aleatorias $X_1, X_2, . . ., X_n$ que son iid y distribuidas uniformemente en $[0, \theta]$.

2. **Función de Distribución Acumulada (CDF)**: La CDF de cada Xᵢ es:

$$F_X(x) = \begin{cases} 0 & \text{si } x < 0 \\ \frac{x}{\theta} & \text{si } 0 \leq x \leq \theta \\ 1 & \text{si } x > \theta \end{cases}$$

3. **Máximo de la Muestra**: Definimos el máximo de la muestra como $M = \max(X_1, X_2, \dots, X_n)$.


4. **CDF del Máximo**: La CDF del máximo se puede calcular como:

$$
\begin{align*}
F_M(m) &= P(M \leq m) = P(X_1 \leq m, X_2 \leq m, \dots, X_n \leq m) \\
&= P(X_1 \leq m)^n \\
&= (F_X(m))^n
\end{align*}
$$

Para $0 \leq m \leq \theta$:

$$
F_M(m) = \left( \frac{m}{\theta} \right)^n
$$

5. **Función de Densidad (PDF)**: Para encontrar la función de densidad del máximo, derivamos la CDF:

$$
\begin{align*}
f_M(m) &= \frac{d}{dm} F_M(m) \\
&= \frac{d}{dm} \left( \frac{m}{\theta} \right)^n \\
&= \frac{n}{\theta^n} m^{n-1}
\end{align*}
$$

para $0 \leq m \leq \theta$.


La función de densidad del máximo $M$ de $n$ variables aleatorias uniformes en $[0, \theta]$ es:

$$f_M(m) = \begin{cases} \frac{n}{\theta^n} m^{n-1} & \text{si } 0 \le m \le \theta \\ 0 & \text{de otro modo} \end{cases}$$

Para determinar si el estimador del máximo $M = max(X_1, X_2, . . ., X_n)$ de una muestra de variables aleatorias $X_i$ uniformes en el intervalo $[0, \theta]$ es insesgado, debemos calcular su valor esperado $E[M]$ y compararlo con $\theta$.

1. **Cálculo de $E[M]$**: Usamos la función de densidad del máximo:

$$E[M] = \int_{0}^{\theta} m \cdot f_M(m) \, dm = \int_{0}^{\theta} m \cdot \frac{n}{\theta^n} m^{n-1} \, dm = \frac{n}{\theta^n} \int_{0}^{\theta} m^n \, dm$$

2. **Integral**: La integral $\int_{0}^{\theta} m^n \, dm$ se evalúa como:

$$ \int_0^\theta m^n \, dm = \left[ \frac{m^{n+1}}{n+1} \right]_0^\theta = \frac{\theta^{n+1}}{n+1} $$

3. **Sustituyendo**: Sustituyendo en la expresión para $E[M]$:

$$ E[M] = \frac{n}{\theta^n} \cdot \frac{\theta^{n+1}}{n+1} = \frac{n\theta}{n+1} $$

4. **Comparación**: Vemos que:

$$ E[M] = \frac{n\theta}{n+1} $$

Esto implica que $E[M]$ no es igual a $\theta$, lo que significa que el estimador $M$ es sesgado.


## Correción

1. **Corrección**: Para que sea insesgado, podemos considerar un estimador corregido, por ejemplo, $\hat{\theta} = \frac{n+1}{n} M$, que tiene un valor esperado:

$$E[\hat{\theta}] = E\left[\frac{n+1}{n} M\right] = \frac{n+1}{n} E[M] = \frac{n+1}{n} \cdot \frac{n\theta}{n+1} = \theta$$

Por lo tanto, el máximo $M$ es sesgado, pero el estimador $\hat{\theta} = \frac{n+1}{n} M$ es insesgado.


## Error cuadrático medio de un estimador

-  Supongamos que $\hat{\theta}_1$ y $\hat{\theta}_2$ son estimadores inesegados de $\theta$. Esto indica que la distribución de cada estimador está centrada en el verdadero valor $\theta$.
- Sin embargo, las varianzas de estas distribuciones pueden ser diferentes.
- Cuando se elige uno de entre varios estimadores, un principio útil es seleccionar el estimador que tenga la menor varianza.

>[!info] ECM
El error cuadrático medio de un estimador $\hat{\theta}$ del parámetro $\theta$ está definido como  $$ECM(\hat{\theta}) = E\left((\hat{\theta} - \theta)^2\right)$$
y puede reescribirse de la siguiente manera:
$$ \begin{align*} \text{ECM}(\hat{\theta}) &= \mathbf{E} \left( (\hat{\theta} - \theta)^2 \right) \\ &= \mathbf{E} \left( (\hat{\theta} - \mathbf{E}(\hat{\theta}))^2 \right) + (\theta - \mathbf{E}(\hat{\theta}))^2 \\ &= \text{Var}(\hat{\theta}) + \text{SSGO}(\hat{\theta})^2 \end{align*} $$ Esto es, el error cuadrático medio de $\hat{\theta}$ es igual a la varianza del estimador más el cuadrado del sesgo. Vamos a comparar dos estimadores usando el ECM.
>
>- Si $\hat{\theta}_1$ y $\hat{\theta}_2$ son estimadores para $\theta$, vamos a decir que aquel que posea el menor ECM es el mejor estimador. Si $\hat{\theta}$ es un estimador insesgado de $\theta$, el error cuadrático medio de $\hat{\theta}$ es igual a la varianza de $\hat{\theta}$.

>[!info] Estimadores insesgados
Si $\hat{\theta}_1$ y $\hat{\theta}_2$ son estimadores insesgados para $\theta$,vamos a elegir aquel que posea la menor varianza. Por ejemplo, si $$V(\hat{\theta}_1) \geq V(\hat{\theta}_2)$$ entonces decimos que $\hat{\theta}_2$ es mejor estimador que $\hat{\theta}_1$ para estimar $\theta$


## Error Estándar de un estimador

>[!notes] Error estándar
Sea $\hat{\theta} = h(X_1; · · · ; X_n)$ un estimador puntual para $\theta$. Llamaremos Error Estándar del Estimador a
$$ \sigma_{\hat{\theta}} = \sqrt{Var(\hat{\theta})} $$ Cuando el error estándar del estimador depende de parámetros desconocidos y son reemplazados por estimaciones, se lo llama **Error Estandar Estimado**, denotado por $$ \hat{\sigma}_{\hat{\theta}} = \sqrt{\hat{Var(\hat{\theta})}} $$


## Eficiencia relativa

El error cuadrático medio es un criterio importante para comparar dos estimadores.

## Eficiencia relativa

Sean $\hat{\theta}_1$ y $\hat{\theta}_2$ dos estimadores del parámetro $\theta$, y $ECM(\hat{\theta}_1)$ y $ECM(\hat{\theta}_2)$ los errores cuadráticos medios de $\hat{\theta}_1$ y $\hat{\theta}_2$. Entonces, la eficiencia relativa de $\hat{\theta}_1$ con respecto a $\hat{\theta}_2$ se define como

$$ \begin{align*} \frac{ECM(\hat{\theta}_1)} {ECM(\hat{\theta}_2)} \end{align*} $$

Si la eficiencia relativa es menor que uno, entonces puede concluirse que $\hat{\theta}_1$ es un estimador más eficiente de $\theta$ que $\hat{\theta}_2$, en el sentido de que tiene un error cuadrático medio más pequeño.![[Pasted image 20261002091046.png|526]]


>[!example] Ejemplo
 Supongamos que queremos estimar la media μ de una población a partir de una muestra aleatoria $X_1,⋯,X_n$.
 Se quiere comparar dos estimadores posibles de $\mu$: la media muestral $\overline{X}$ y una variable de la muestra aleatoria, por ejemplo $X_1$. 
 Ambos estimadores son insegados, por lo cual el ECM de cada uno de ellos es la varianza.
 >
>-  Para la media muestral, se tiene $$ \text{ECM}(\overline{X}) = \frac{\sum_{i=1}^{n} Var(X_i)}{n^2} = \frac{\sigma^2}{n} $$
>- Para $X_1$ la varianza es $Var(X_i) = \sigma^{2}$. Por consiguiente, la eficiencia relativa de $\overline{X}$ con respecto a $X_1$ es $$ \frac{\text{ECM}(\overline{X})}{\text{ECM}(X_1)} = \frac{\frac{\sigma^2}{n}}{\sigma^2} = \frac{1}{n} $$
>- Puesto que $\frac{1} {n} < 1$ si $n \geq 2$, podemos concluir que la media muestral es un mejor estimador de $\mu$ que una sola observación $X$.


Otra manera de medir la proximidad de un estimador $\hat{\theta}$ al parámetro $\theta$ es en términos de la consistencia. Denotemos el estimador como $\hat{\theta}_n$ para enfatizar que depende de un muestreo aleatorio de tamaño $n$.

>[!notas] Consistencia
Sea $X_1, . . . , X_n$ una muestra aleatoria con distribución que depende de un parámetro $\theta$, desconocido. Entonces se dice un estimador de $\theta$, $\hat{\theta} = h(X_1, . . . , X_n)$ es un estimador consistente para $\theta$ si $\lim_{n \to \infty} \hat{\theta} = \theta$ en probabilidad. Esto es, $$ \lim_{n \to \infty} \mathbf{P}(|\hat{\theta} - \theta| < \epsilon) = 1 $$ Y es equivalente a $$ \lim_{n \to \infty} \mathbf{P}(|\hat{\theta} - \theta| \geq \epsilon) = 0 $$ ![[Pasted image 20261002092009.png]]

Una forma de mostrar que un estimador es consistente es probar que su error cuadrático medio tiende a cero cuando $n$ tiende a infinito. Recordar que la desigualdad de Chebychev establece una cota superior para las colas de una distribución de una variable que tiene varianza finita.

>[!notes] Criterio de consistencia
Sea $\hat{\theta}$ un estimador del parámetro $\theta$ basado en un muestreo de tamaño $n$. Entonces, para todo $\epsilon > 0$ vale que $$P(|\hat{\theta} - \theta| \geq \epsilon) \leq \frac{E((\hat{\theta} - \theta)^2)}{\epsilon^2} = \frac{ECM(\hat{\theta})}{\epsilon^2}$$
Por lo cual, si el error cuadrático medio de $\hat{\theta}$ tiende a cero cuando $n$ tiende a infinito, entonces $\hat{\theta}$ es consistente para $\theta$.

## Consistencia del promedio y varianza muestral

Una consecuencia del criterio de consistencia es que el promedio $X_n$ es un estimador consistente de $\mu = E(X)$, la esperanza de la distribución de la población.

>[!info] Consistencia de la media muestral
>1. Por la ley de los grandes números, $\overline{X}$ converge a $\mu$ en probabilidad.
>2. Como $ECM(\overline{X})$ es $\sigma^{2}/n$, aplicando el criterio de consistencia resulta $\overline{X}$ consistente para $\mu$

¿Qué ocurre con $S^{2}$ o $\sum^{2}$? ¿Es un estimador consistente de $\sigma^{2}$? La respuesta es sí, pero para probarlo precisamos un argumento que nos permita aplicar una función continua a un estimador consistente

>[!info] Consistencia y continuidad
Si $\hat{\theta}$ es un estimador consistente del parámetro $\theta$, y $g : \mathbb{R} \to \mathbb{R}$ es una función continua, entonces $g(\hat{\theta})$ es un estimador consistente de $g(\hat{\theta})$.

Apliquemos este resultado a $\sum^{2}$.
1. Por un lado, un cálculo directo muestra que

$$ \Sigma^2 = \frac{1}{n} \sum_{i=1}^{n} (X_i - \overline{X})^2 = \frac{1}{n} \sum_{i=1}^{n} X_i^2 - \overline{X}^2 $$

2. El primer término del lado derecho converge, con probabilidad alta, a $E(X^{2})$ por la LGN aplicada a la sucesión i.i.d. de variables $X_{1}^{2}; . . . ; X_{n}^{2}$.
3. Para ver la convergencia del segundo miembro aplicamos el teorema anterior con $g(x) = x^{2}$. Es decir, como $\overline{X}$ es un estimador consistente de $E(X)$, entonces $\overline{X}^{2}$ es un estimador consistente de $E(X)^{2}$.
4. Entonces $\sum^{2}$ es un estimador consistente de $E(X^{2}) – E(X)^{2} = \sigma^{2}$. Lo mismo vale para $S^{2}$.


## Momentos

1. Los momentos de $X$ son $$M_1 = E(X), \dots, M_k = E(X^k)$$supondremos que existen y son finitos.
2. Sea $X_1, \dots, X_n$ un muestreo aleatorio de $X$, con distribución $$p(x, \theta_1, \dots, \theta_k) \text{ con } (\theta_1, \dots, \theta_k) \in \mathbb{R}^k$$ Aquí $p$ denota la densidad continua de $X$ o la función de probabilidad discreta
3. Entonces el vector de momentos es una función de los $\theta_{i}$: $$(M_1, \dots, M_k) = g(\theta_1, \dots, \theta_k)$$
4. Denotamos $$\overline{M}_j = \frac{1}{n} \sum_{i=1}^n X_i^j$$ los momentos muestrales.

 >[!info] Método
El método de los momentos consiste en resolver el sistema de ecuaciones $$(\overline{M}_1, \dots, \overline{M}_k) = g(\hat{\theta}_1, \dots, \hat{\theta}_k)$$ Es decir, los estimadores $\hat{\theta}_i; i = 1; \dots; k$ están dados por $$(\hat{\theta}_1, \dots, \hat{\theta}_k) = g^{-1}(\overline{M}_1, \dots, \overline{M}_k)$$
Este sistema no tiene porque tener solución, ni ser única, pero sí en todas las aplicaciones que veremos en el curso.


>[!example] Ejemplo
>1. Por ejemplo, supongamos que $X_1; \dots; X_n$ es un muestreo aleatorio de $X$ que tiene densidad $$p(x, \theta) = (\theta + 1)x^\theta \quad x \in [0, 1]$$ 
>2. La esperanza de $X$ es entonces $$E(X) = (\theta + 1) \int_{0}^{1} x^{\theta+1} dx = \frac{\theta + 1}{\theta + 2}$$
>3. Esto quiere decir que la esperanza de $X$ es una función del parámetro $g(\theta)$; en este caso $$g(\theta) = \frac{\theta + 1}{\theta + 2}$$
>4. Planteando la ecuación de estimación y resolviendo queda $$\overline{X} = \frac{\hat{\theta} + 1}{\hat{\theta} + 2} \implies \hat{\theta} = \frac{1 - 2\overline{X}}{\overline{X} - 1}$$ y este es el estimador de momentos de $\theta$.

>[!example] Ejemplo
>1. Por ejemplo, supongamos que $X_1; \dots; X_n$ es un muestreo aleatorio de $X$ que tiene densidadm$$f_X(x) = \begin{cases} \frac{1}{2} + \frac{\beta x^3}{2} & -1 \leq x \leq 1 \\ 0 & \text{en cualquier otro caso} \end{cases}$$ donde $\beta \in [-1, 1]$.
>2. La esperanza de $X$ es entonces $$\begin{align*}
E[X] &= \int_{-\infty}^{\infty} x f_X(x) \, dx = \int_{-1}^{1} x \left( \frac{1}{2} + \frac{\beta x^3}{2} \right) \, dx = \int_{-1}^{1} \frac{x}{2} dx + \int_{-1}^{1} \frac{\beta x^4}{2} dx \tag{1} \\
&= 0 + \frac{\beta x^5}{25} \bigg|_{-1}^{1} = \frac{\beta}{5} \tag{2}
\end{align*}$$
>3. Esto quiere decir que la esperanza de $X$ es una función del parámetro $g(\beta)$; en este caso $$g(\beta) = \frac{\beta}{5}$$ 
>4. Planteando la ecuación de estimación y resolviendo queda $$X = \frac{\beta}{5} \implies \hat{\beta} = 5\overline{X}$$ y este es el estimador de momentos de $\beta$.


## Verificar que el estimador es insesgado

Un estimador es insesgado si su esperanza es igual al parámetro verdadero. Calculamos $E[\hat{\beta}]$:
$$E[\hat{\beta}] = E[5\bar{X}] = 5E[\bar{X}].$$ Dado que X es la media muestral, tenemos: $$E[\bar{X}] = E[X] = \frac{\beta}{5}.$$Por lo tanto:

$$E[\hat{\beta}] = 5 \cdot \frac{\beta}{5} = \beta.$$

Esto confirma que $\hat{\beta} = 5\overline{X}$ es un estimador insesgado para $\beta$.

## Estimación de Máxima Verosimilitud

-  Sea $X_1; · · · ; X_n$ una muestra aleatoria de $X$, con distribución
$$p(x, \theta_1, \cdots, \theta_k) \text{ con } (\theta_1, \cdots, \theta_k) \in \mathbb{R}^k$$Aquí $p$ denota la densidad continua de $X$ o la función de probabilidad discreta.
- Queremos estimar el vector de parámetros desconocidos $(\theta_{1}, · · · , \theta_{k})$ de la distribución.
- Definimos la función de verosimilitud de la muestra, esto es, la densidad conjunta de la muestra aleatoria en función del vector de parámetros, dejando fijo el conjunto de valores observados de la muestra. $$L(\theta_1, \cdots, \theta_k) = p(x_1, \cdots, x_n | \theta_1, \cdots, \theta_k) = \prod_{i=1}^{n} p(x_i | \theta_1, \cdots, \theta_k) \quad (1)$$
- La estimación de máxima verosimilitud (MV) es un método para encontrar los parámetros que mejor ajusten la función de (no esta completo en la filmina)???

- Suponga que se quiere estimar un sólo parámetro $\theta$, el estimador $\hat{\theta}$ de máxima verosimilitud es el valor de $\theta$ que maximiza la verosimilitud $L(\theta)$, esto es $$ \hat{\theta} = \arg \max_{\theta} \prod_{i=1}^{n} p(x_i|\theta) $$
- Ese estadístico también realiza el máximo de la función de log-verosimilitud $\ell(\theta) \equiv \ln p(x_1, \dots, x_n|\theta)$, esto es

$$ \hat{\theta} = \arg \max_{\theta} \sum_{i=1}^{n} \ln p(x_i|\theta) $$

![[Pasted image 20261002223540.png|585]]
(a) Puntos en una dimensión tomados de una distribución Gaussiana con varianza específica y media desconocida. Se muestran cuatro de un número infinito de distribuciones fuente candidatas.
(b) Verosimilitud (curva negra) y log-verosimilitud (curva roja) en función de la media. El valor que maximiza la verosimilitud es señalado con θ .

-  Generalizando la verosimilitud como una función de los $k$ parámetros desconocidos $\theta = (\theta_{1}, . . . , \theta_{k})$; el estimador vectorial de máxima verosimilitud es el vector $\hat{\theta} = (\hat{\theta}_{1}, . . . , \hat{\theta}_{k})$ que maximiza la $\ell(\theta) \equiv \ln p(x|\theta)$ $$\hat{\theta} = \arg \max_{\theta} \sum_{i=1}^{n} \ln p(x_i | \theta)$$
- En la mayoría de los casos, esto se reduce a resolver la ecuación$$ \nabla_{\theta} \mathcal{L}(\theta) = \sum_{i=1}^{n} \nabla_{\theta} \ln p(x_i | \theta) = 0 $$donde el operador gradiente es

$$ \nabla_{\theta} \equiv \left[ \frac{\partial}{\partial \theta_1}, \dots, \frac{\partial}{\partial \theta_k} \right]^T $$

>[!info] Principio de Invarianza
Si $\theta$ es el estimador de máxima verosimilitud de $\theta$, entonces $h(\hat{\theta})$ es el estimador de máxima verosimilitud de $h(\theta)$

**Observación**
En general, cuando la función de verosimilitud es diferenciable en el parámetro $\theta$, para calcular $\hat{\theta}$ derivamos $\ell_{n}(\theta)$ respecto de $\theta$ e igualamos a cero.
En general se trata siempre de un máximo, aunque para verificarlo deberíamos calcular el signo  de la derivada segunda $\ell_{n}´´(\theta)$ y ver que es negativo.
Cuando $L_n(\theta)$ no es diferenciable, cosa que sucede típicamente cuando el dominio de $L_n(\theta)$ depende de $\theta$, hallar en dónde se da el máximo es más difícil y no se puede hacer derivando.

>[!example] Ejemplo: Caso Bernoulli
Supongamos que $X_1, . . ., X_n \sim Ber(p)$. El logaritmo de la función de verosimilitud es $$ \ell_n(p) = \sum_{i=1}^{n} X_i \ln(p) + (1 - X_i) \ln(1 - p)$$ de donde vemos que $$\begin{cases} \ell_n'(p) = n \left[ \frac{\bar{X}_n}{p} - \frac{1 - \bar{X}_n}{1 - p} \right] \\ \ell_n''(p) = -n \left[ \frac{\bar{X}_n}{p^2} + \frac{1 - \bar{X}_n}{(1 - p)^2} \right] \end{cases}$$ Notar que $\ell_n''(p) < 0$ para todo $p \in (0, 1)$, por lo que el punto crítico es un máximo. Se puede deducir entonces que $T_n = \bar{X}_n$. Es decir, el estimador de máxima verosimilitud es el promedio.

>[!example] Ejemplo: Caso Uniforme
>-  Supongamos que $X_1, . . . , X_n \sim U (0, \theta)$. La función de verosimilitud no es continua, y está dada por $$L_n(\theta) = \begin{cases} \frac{1}{\theta^n} & \text{si } X_i < \theta \forall i \\ 0 & \text{si no.} \end{cases}$$
>- Decir que $X_{i} < \theta$ para todo $i$ es equivalente a decir que $\max_i X_i < \theta$. Entonces podemos reescribir la función de verosimilitud como $$L_n(\theta) = \begin{cases} \frac{1}{\theta^n} & \text{si } \max_i X_i < \theta \\ 0 & \text{si no.} \end{cases}$$
>- Es claro que el máximo se da en $T_n = \max_{i} X_{i}$, que es por lo tanto el estimador de máxima verosimilitud de $\theta$.
>  ![[Pasted image 20261002224902.png]]

