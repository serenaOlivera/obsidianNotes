## Covarianza
----
>[!info] Definición 
>Sea $(X, Y)$ un vector aleatorio con densidad conjunta $f_{XY}$ y esperanzas finitas entonces $$\begin{align*} Cov(X, Y) &= \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} (X - E(X))(y - E(Y)) f_{X,Y}(x, y) dx dy \\
&= E(XY) - E(X)E(Y) \end{align*}$$

**Propiedades**
Sea $(X, Y)$ un vector aleatorio con densidad conjunta $f_{XY}$, entonces 
1. $Cov(X, X) = V(X)$
2. $Cov(X, Y) = E(XY) −E(X)E(Y)$ 
3. Si $X$ e $Y$ son independientes, entonces $Cov(X, Y) = 0$.
4. $Cov(aX + b, cY + d) = acCov(X, Y) \quad \forall a, b, c, d \in \mathbb{R}$
5. $Var(aX + bY) = a^2Var(X) + b^2Var(Y) + 2abCov(X, Y) \quad \forall a, b \in \mathbb{R}$ 
6. Si $X$ e $Y$ son independientes entonces $Var(aX + bV) = a^2Var(X) + b^2Var(Y)$

Proposición:
Si $X_1, . . ., X_n$ son variables aleatorias con varianzas finitas y $a_i \in \mathbb{R}  \quad \forall i = 1, . . ., n$, entonces
1.
$$E\left(\sum_{i=1}^{n} a_i X_i\right) = \sum_{i=1}^{n} a_i E(X_i)$$
2. Si $Y_1, . . ., Y_m$ son variables aleatorias con varianzas finitas, $b_j \in  \mathbb{R} \quad \forall j, \  j = 1, . . ., m$ entonces:
$$Cov\left(\sum_{i=1}^{n} a_i X_i, \sum_{j=1}^{m} b_j Y_j\right) = \sum_{i=1}^{n} \sum_{j=1}^{m} a_i b_j Cov(X_i, Y_j)$$

Proposición:
1.
$$V\left(\sum_{i=1}^{n} a_i X_i\right) = \sum_{i=1}^{n} a_i^2 V(X_i) + 2 \sum_{1 \le i < j \le n} a_i a_j \operatorname{Cov}(X_i, X_j)$$
2. Si $X_1, . . . , X_n$ son variables aleatorias independientes entonces
$$V\left(\sum_{i=1}^{n} a_i X_i\right) = \sum_{i=1}^{n} a_i^2 V(X_i)$$
## Correlación
--- 
>[!info] Definición
>Sean $X$ e $Y$ variables aleatorias continuas con $0 < Var(X) < \infty$, $0 < Var(Y) < \infty$. Definimos el coeficiente de correlación lineal como $$\rho(X, Y) = \frac{Cov(X, Y)}{\sqrt{(Var(X))} \sqrt{Var(Y)}}$$ 

Propiedades
1. El coeficiente de correlación lineal es independiente de posición y escala, pues
$$ \rho(X + a, Y + a) = \rho(X, Y) \qquad \rho(aX, aY) = \rho(X, Y), a > 0 $$
2. $-1 \le \rho(X, Y) \le 1$
3. $\rho(X, Y) = 1$ si y solamente si $P(Y = aX + b) = 1$, con $a > 0$.
$\rho(X, Y) = -1$ si y solamente si $P(Y = aX + b) = 1$, con $a < 0$.


# Sumas
--- 
 Proposición:
1. Si $X_1, . . ., X_n$ son variables aleatorias independientes e idénticamente distribuidas (i.i.d.) con $E(X) = \mu$ y $V (X) = \sigma ^2$ entonces:
$$E(\bar{X}_n) = \mu \quad \mathbf{y} \quad V(\bar{X}_n) = \frac{\sigma^2}{n}$$
Definición:
Diremos que $X_1, . . . , X_n$ es una **muestra aleatoria** si son variables aleatorias independientes e idénticamente distribuidas.

- Proposición:
Si $X_1, . . . , X_n$ es una muestra aleatoria de la distribución normal, o sea $X_i \sim N (\mu, \sigma ^2),\quad  \forall i, \ i = 1, . . . , n$. Entonces
$$ \sum_{i=1}^{n} X_i \sim N \left( n\mu, n\sigma^2 \right) \quad \frac{1}{n} \sum_{i=1}^{n} X_i \sim N \left( \mu, \frac{1}{n}\sigma^2 \right) \quad \sqrt{n} \left( \frac{\overline{X} - \mu}{\sigma} \right) \sim N(0, 1) $$
- Proposición:
Si $X_1, . . ., X_n$ son v.a. independientes y con distribución normal, o sea que $X_i \sim N (\mu_i, \sigma_{i}^{2}), \quad \forall i = 1, . . ., n$. Entonces
$$ \sum_{i=1}^{n} a_i X_i \sim N \left( E \left( \sum_{i=1}^{n} a_i X_i \right), V \left( \sum_{i=1}^{n} a_i X_i \right) \right) $$
donde
$$ \begin{aligned} E\left(\sum_{i=1}^{n} a_i X_i\right) &= \sum_{i=1}^{n} a_i E\left(X_i\right) = \sum_{i=1}^{n} a_i \mu_i \\ V\left(\sum_{i=1}^{n} a_i X_i\right) &= \sum_{i=1}^{n} a_i^2 V\left(X_i\right) = \sum_{i=1}^{n} a_i^2 \sigma_i^2 \end{aligned} $$

- Proposición:
Si $X$ e $Y$ son discretas con función de masa conjunta $p(x, y)$, y sea $Z = X + Y$. Notemos que $Z = z$ cuando $X = x$ y $Y = z – x$, por lo cual
$$p_Z(z) = \sum_{x=-\infty}^{\infty} p(x, z-x)$$
Si $X$ e $Y$ son independientes, entonces $p(x, y) = p_X(x)p_Y(y)$ y
$$p_Z(z) = \sum_{x=-\infty}^{\infty} p_X(x)p_Y(z-x)$$
Esta suma se llama convolución de las funciones $p_X$ y $p_Y$

-  Proposición:
  Sean $X_1, . . . , X_r$ variables aleatorias independientes geométricamente distribuidas con parámetro $p$. Entonces $X_1 + · · · + X_r$ tiene distribución binomial negativa de parámetros $r, p$.
- Proposición:
  Sean $X_1, . . . , X_r$ variables aleatorias independientes con distribución binomial con parámetro $n_i, p$. Entonces $X_1 + · · · + X_r$ tiene distribución binomial de parámetros $n_1 + · · · + n_r, p$.
- Proposición:
  Sean $X_1, . . ., Xr$ variables aleatorias independientes con distribución binomial negativa con parámetro $n_i, p$. Entonces $X_1 + · · · + X_r$ tiene distribución binomial negativa de parámetros $n_1 + · · · + n_r, p$.
- Proposición:
  Sean $X_1, . . ., X_r$ variables aleatorias independientes con distribución Poisson con parámetro $\lambda_i$. Entonces $X_1 + · · · + X_r$ tiene distribución Poisson con parámetro$\lambda_1 + · · · + \lambda_r$.

>[!example] Ejemplo 
> El número de imperfecciones que tiene una placa fotográfica sigue la distribución de Poisson de parámetro 0,1 imperfecciones por $cm^2$.
> 1. Si de tal placa se toma una muestra de $30 cm^2$, ¿cuál es la probabilidad de que esa muestra contenga exactamente tres irregularidades?
> 2. Si ahora se toma en forma independiente 5 muestras de $30 cm^2$, ¿cuál es la probabilidad de que exactamente dos de ellas contengan a lo sumo una irregularidad?
>
>Si Y es el número imperfecciones que tiene una placa fotográfica sigue la distribución de Poisson de parámetro 0,1 imperfecciones por cm².
> Si tenemos $30cm^2$, entonces el número de imperfecciones $X$ en toda la placa es la suma de las imperfecciones en cada centímetro cuadrado, $X = Y_1 + · · · + Y_{30}$, una suma de variables aleatorias independientes Poisson con el mismo parámetro 0.1.
>  Por lo cual $X$ también es Poisson, con parámetro $\lambda = 0.1+···+0.1= 30×0.1= 3$. Esto quiere decir que podemos esperar una media de 3 imperfecciones por placa de $30 cm^2$.
>   Ahora la probabilidad de que la placa contenga exactamente 3 irregularidades es $$P(X = 3) = \frac{\lambda^3}{3!} e^{-\lambda} = \frac{27}{6} e^{-3} = 0.2240$$
>  
>- Si ahora tomamos 5 muestras independientes de $30 cm^2$ cada una, la variable $Z$ que mide el número de placas con a lo sumo una irregularidad es una variable binomial, con parámetro $n = 5$ y probabilidad $p = P(X \leq 1)$, donde $X$ es la variable Poisson que mide las irregularidades por placa. $$p = P(X \leq 1) = e^{-\lambda} + \frac{\lambda^2}{2!} e^{-\lambda} = e^{-3}(1 + \frac{9}{2}) = 0.2738$$
>   Por lo cual la probabilidad de que exactamente dos tengan a lo sumo una irregularidad es $$P(Z = 2) = \binom{5}{2} 0.2738^2 (1 - 0.2738)^{5-2}$$

Proposición:
Si X e Y son variables aleatorias continuas con densidad conjunta f(x, y) y sea Z = X + Y
$$f_{X+Y}(z) = \int_{-\infty}^{\infty} f(x, z-x)dx \quad -\infty < z < \infty$$
Si X e Y son variables independientes entonces X + Y tiene densidad
$$f_{X+Y}(z) = \int_{-\infty}^{z} f_X(x)f_Y(z-x)dx \quad -\infty < z < \infty$$
Si X e Y son independientes y no negativas entonces X + Y tiene densidad
$$f_{X+Y}(z) = \int_{0}^{z} f_X(x)f_Y(z-x)dx \quad -\infty < z < \infty$$

Notemos que $Z \leq z$ cuando $X = x$ y $Y \leq z - x$, por lo cual
$$F_Z(z) = \int_{-\infty}^{\infty} \int_{-\infty}^{z-x} f(x, y) dy dx$$
Haciendo el cambio de variable en la integral interior $y = v - x$ se obtiene
$$F_Z(z) = \int_{-\infty}^{\infty} \int_{-\infty}^{z} f(x, v - x) dv dx = \int_{-\infty}^{z} \int_{-\infty}^{\infty} f(x, v - x) dx dv$$
Diferenciando con respecto a $z$ queda
$$f_Z(z) = \int_{-\infty}^{\infty} f(x, z - x) dx$$
Si X e Y son independientes, entonces $f(x,y) = f_X(x)f_Y(y)$ y
$$f_Z(z) = \int_{-\infty}^{\infty} f_X(x) f_Y(z - x) dx$$
Esta integral se llama convolución de las funciones $f_X$ y $f_Y$


>[!example] Ejemplo
>La vida útil de un cierto tipo de fusibles puede suponerse con distribución exponencial con $\lambda = 1/3$, donde las mediciones son en cientos de horas.
Si un sistema tiene dos fusibles con vida útil independiente ensamblados de tal forma que uno se activa cuando el otro falla, por lo cual el sistema falla cuando ambos lo hacen, encuentra la probabilidad de que el sistema dure menos de 1 (ciento de hora)
>
>Sea $V$ la vida útil del sistema, $X$ e $Y$ la vida útil de cada fusible, entonces $V = X + Y$, la suma de dos variables continuas no negativas independientes con distribución exponencial. Por lo tanto $$ f_V(z) = \int_0^z \lambda e^{-\lambda x} \lambda e^{-\lambda(z-x)} dx \\ = \lambda^2 e^{-\lambda z} \int_0^z dx \\ = \lambda^2 ze^{-\lambda z} \quad 0 < z$$  $$\begin{align*} P(V < 1) &= \int_0^1 \lambda^2 ze^{-\lambda z} dz = uv - \int vu' \\
&= \lambda^2 \left[ z \frac{1}{-\lambda} e^{-\lambda z} \right]_0^1 - \frac{1}{-\lambda} \int_0^1 e^{-\lambda z} dz \\
&= \lambda^2 \left[ -\frac{1}{\lambda} e^{-\lambda} - \frac{1}{-\lambda} \left[ -\frac{1}{\lambda} e^{-\lambda z} \right]_0^1 \right] \\
&= \lambda^2 \left[ -\frac{1}{\lambda} e^{-\lambda} - \frac{1}{\lambda^2} e^{-\lambda} + \frac{1}{\lambda^2} \right] \\
&= 1 - e^{-\lambda} (\lambda + 1) \\
&= 1 - \frac{4}{3} e^{\frac{1}{3}}
\end{align*}$$

>[!example] Ejemplo
> Se diseña un ascensor de carga cuyo límite es $1000 kg$. El peso de cada caja sigue una distribución normal con un peso medio de $32 kg$ y un desvío estándar de $10 kg$.
> 1. ¿Cuál es la probabilidad de que un grupo de 30 cajas exceda el límite de carga?
> 2. Se toma una muestra aleatoria simple de 5 cajas ¿cuál es la probabilidad de que el mínimo de la muestra sea superior a $30kg$ e inferior a $33kg?$
>    
>- Para que el grupo exceda el límite de carga la suma de los pesos de las cajas debe exceder $1000kg$.
>   Como el peso de cada caja es una variable normal independiente con los mismos parámetros $\mu$ y $\sigma^2$, la variable $X = \sum_{i=1}^{30} X_i$ también es normal con parámetros $\mu_X = 30 \times \mu = 960$ y $\sigma_X^2 = 30 \times \sigma^2 = 3000$.
>    Entonces estandarizando calculamos la probabilidad $$\begin{align*}
P(X > 1000) &= P((X - \mu_X) / \sigma_X > (1000 - \mu_X) / \sigma_X) \\
&= P(Z > (1000 - 960) / 54.7723) \\
&= P(Z > 0.7303) \\
&= 0.2326
\end{align*}$$
>Si las variables $X_1, X_2, X_3, X_4, X_5$ representan el peso de las cinco cajas elegidas al azar, y $K = min(X_1, X_2, X_3, X_4, X_5)$ con distribución
$$F_K(k) = P(K \le k) = 1 - P(K \ge k) = 1 - P(X_1 \ge k)^5 = 1 - [F(\sqrt[k]{k}(k))]^5$$

## Ejemplos
---
![[Pasted image 20260925001232.png]]![[Pasted image 20260925001246.png]]![[Pasted image 20260925001256.png]]![[Pasted image 20260925001310.png]]![[Pasted image 20260925001322.png]]![[Pasted image 20260925001337.png]]![[Pasted image 20260925001350.png]]![[Pasted image 20260925001358.png]]

# Teorema Central del Límite (TCL)
---

>[!tip] Teorema de Moivre-Laplace
>Si $X$ tiene distribución binomial de parámetros $n$ y $p$ entonces
$$Y = \frac{X - np}{\sqrt{np(1-p)}}$$
tiene distribución normal estándar, si $n$ es suficientemente grande. Para esta aproximación se recomienda $np \geq 10$ y $n(1 − p) ≥ 10$

**Muestra aleatoria**
Una muestra aleatoria de tamaño n es un vector de variables $X_1, . . ., X_n$ independientes e idénticamente distribuidas

>[!tip] Teorema central del límite
Sea $X_1, . . . X_n$ una muestra aleatoria de una distribución con media $\mu$ y varianza $\sigma^2$. Entonces si $Sn = X_1 + · · · + X_n$, la función de distribución de la variable $$\frac{S_n - E(S_n)}{\sqrt{Var(S_n)}} = \frac{S_n - n\mu}{\sqrt{n\sigma}}$$ converge a la la función de distribución de una variable normal standard. Esto es $$P\left(\frac{S_n - n\mu}{\sqrt{n\sigma}} \le t\right) \longrightarrow \Phi(t) \quad \forall t$$
Por lo cual, si n es suficientemente grande, puede considerarse a Sn con distribución normal con media $n\mu$ y varianza $n\sigma ^2$.

>[!info] Corolario Teorema central del límite
Sea $X_1, . . . X_n$ una muestra aleatoria de una distribución con media $\mu$ y varianza $\sigma ^2$. Entonces si $\overline{X}_n =\frac{X_1+···+Xn}{n}$ , la función de distribución de la variable
$$ \frac{\overline{X}_n - E(\overline{X}_n)}{\sqrt{Var(\overline{X}_n)}} = \sqrt{n} \frac{\overline{X}_n - \mu}{\sigma} $$
converge a la la función de distribución de una variable normal estándar. Esto es
$$ P \left( \sqrt{n} \frac{\overline{X}_n - \mu}{\sigma} \leq t \right) \longrightarrow \Phi(t) \quad \forall t $$
Por lo cual, si $n$ es suficientemente grande, puede considerarse a $\overline{X}_n$ con distribución normal con media $\mu$ y varianza $\frac{\sigma^2}{n}$ .

Observación
- Toda variable que puede escribirse como una suma de variables independientes idénticamente distribuidas puede ser aproximada por una distribución Normal. 
- El teorema de De Moivre -Laplace muestra esto para la variable Binomial, pero la Poisson y la Binomial Negativa tambien pueden ser aproximadas por una Normal 
- Y la distribución Gamma de tasa $\lambda$, cuando su parámetro de forma es un número natural, pues puede considerarse una suma de exponenciales independientes con tasa $\lambda$.

>[!info] Lema
a) Sea $X$ con distribución Poisson de parámetro $\lambda$. Si pensemos a $X$ como suma de variables Poisson independientes $X_1, . . ., X_n$ todas con el mismo parámetro $\lambda/n$, cuando $n$ es suficientemente grande $$P(X \le x) \sim \Phi(x - E(X)) / \sqrt{Var(X))} = \Phi(x - \lambda / \sqrt{\lambda})$$
b) Sea $X$ una variable con distribución binomial negativa de parámetros $n$ y $p$, entonces $X$ puede ser vista como una suma de $n$ variables geométricas independientes de parámetro $p$. Por lo tanto, cuando $n$ es suficientemente grande
$$P(X \le x) \sim \Phi(x - E(X)) / \sqrt{Var(X))} = \Phi(x - (n/p) / \sqrt{n(1-p)/p})$$

>[!example] Ejemplo
>Supongamos que un programa suma números aproximando cada sumando al entero más próximo. Si todos los errores cometidos son independientes entre sí y están distribuidos uniformemente entre -0.5 y 0.5 y se suman 1500 números,
>1. ¿cuál es la probabilidad de que la magnitud del error total exceda 15?
>2. ¿A lo sumo cuántos números pueden sumarse juntos para que la magnitud del error total se mantenga menor que 10 con probabilidad 0.9?
>
> Cada error cometido es una variable aleatoria $\varepsilon_k$ con distribución $U[-0.5, 0.5]$, media $E(\varepsilon_k) = [0.5 + (-0.5)]/2 = 0$ y varianza $Var(\varepsilon_k) = (0.5 - (0.5))^2/12 = 1/12$.
  Definamos $S_n = \sum_{k=1}^n \varepsilon_k$, con $n = 1500$. Entonces por el teorema central del límite, $[S_{1500} - nE(\varepsilon)]/\sqrt{nVar(\varepsilon)} \sim N(0, 1)$ y
$$P(|S_{1500}| > 15) = 1 - P(|S_{1500}| \leq 15) = 1 - P(-15 \geq S_{1500} \leq 15)$$
$$= 1 - P\left(\frac{-15 - nE(\varepsilon)}{\sqrt{nVar(\varepsilon)}} \leq \frac{S_{1500} - nE(\varepsilon)}{\sqrt{nVar(\varepsilon)}} \leq \frac{15 - nE(\varepsilon)}{\sqrt{nVar(\varepsilon)}}\right)$$
$$= 1 - P(-1.34 \leq Z \leq 1.34)$$
$$= 2\Phi(-1.34) = 0.1802$$
>
>Ahora, deseamos encontrar el $n$ más grande para el cual
$$0.9 = P(|S_n| < 10)$$
Usando el teorema central del límite $[S_{1500} - nE(\varepsilon)] / \sqrt{nVar(\varepsilon)} \sim N(0, 1)$ y $$\begin{align*}
P(|S_n| < 10) &= P(-10 < S_n < 10) \\
&= P \left( \frac{-10 - nE(\varepsilon)}{\sqrt{nVar(\varepsilon)}} \leq \frac{S_n - nE(\varepsilon)}{\sqrt{nVar(\varepsilon)}} \leq \frac{10 - nE(\varepsilon)}{\sqrt{nVar(\varepsilon)}} \right) \\
&= P \left( \frac{-10}{\sqrt{\frac{n}{12}}} \leq Z \leq \frac{10}{\sqrt{\frac{n}{12}}} \right) \\
&= 1 - 2P \left( Z \leq \frac{-10}{\sqrt{\frac{n}{12}}} \right)
\end{align*}$$
>por lo cual $$0.9 = 1 - 2P( Z \leq \frac{-10}{\sqrt{\frac{n}{12}}}) \implies P( Z \leq \frac{-10}{\sqrt{\frac{n}{12}}}= 0.05$$
$$y \frac{-10}{\sqrt{\frac{n}{12}}} = -1.65. \text{ Entonces, despejando resulta}$$
$$n = \frac{10^2 12}{1.65^2} = 440.7$$

>[!example] Ejemplo 
>Suponga que se tienen 100 lámparas de un cierto tipo, cuya duración puede modelarse como una variable exponencial de parámetro $\lambda = 0.002$. Si la duración de cada lámpara es independiente de la duración de las otras, encuentre la probabilidad de que el promedio muestral $\overline{T} = (1/100)(T_1 + · · · + T_{100})$ se encuentre entre $400$ y $550$ horas
>
>Como $n$ es 100, podemos suponerlo suficientemente grande y aproximar la distribución del promedio por una normal. Entonces la esperanza y varianza de $S_n = T_1 + · · · + T_n$ son $$\begin{align*} E(S_n) &= E(T_1 + \cdots + T_{100}) = 100. E(T_1) = \frac{100}{0.002} = 50000 \\
Var(S_n) &= Var(T_1 + \cdots + T_{100}) = 100. Var(T_1) = \frac{100}{0.002^2} \\
P(400 \le \frac{T_1 + \cdots + T_{100}}{100}) &\le 550) = P(40000 \le T_1 + \cdots + T_{100} \le 55000) \\
&\sim \Phi\left(\frac{55000 - E(S_n)}{\sqrt{Var(S_n)}}\right) - \Phi\left(\frac{40000 - E(S_n)}{\sqrt{Var(S_n)}}\right) \\
&= \Phi\left(\frac{55000 - 50000}{5000}\right) - \Phi\left(\frac{40000 - 50000}{5000}\right) \\
&= \Phi(1) - \Phi(-2) \\
&= 0.8413 - 0.0228 = 0.8185
\end{align*}$$
