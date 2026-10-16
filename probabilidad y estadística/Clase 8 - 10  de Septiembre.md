### Variable aleatoria $N(\mu, \sigma^2)$
La distribución normal es especialmente relevante en el análisis de datos debido a varias razones:
1. Modelo ampliamente utilizado: Muchos métodos y técnicas estadísticas se basan en la suposición de que los datos siguen una distribución normal
2. Facilita la inferencia estadística: Al asumir una distribución normal, podemos aplicar herramientas estadísticas estándar para realizar inferencias sobre los datos. Esto incluye realizar pruebas de hipótesis, construir intervalos de confianza y realizar análisis de regresión, entre otros.
3. Simplifica los cálculos: La distribución normal tiene propiedades matemáticas bien conocidas y establecidas. Esto facilita los cálculos y permite realizar estimaciones y predicciones más precisas.
4. El Teorema Central del Límite: Establece que la suma o promedio de un gran número de variables aleatorias independientes tiende a seguir una distribución normal, incluso si las variables individuales no son normalmente distribuidas. Esto es fundamental en el análisis de muestras grandes y permite utilizar la distribución normal como una aproximación útil en muchos escenarios.

>[!Info] Variable aleatoria $N(0, 1)$
Se dice que una variable aleatoria continua $Z$ tiene distribución Normal Patrón si su densidad de probabilidad $\varphi$ está definida como
$$ \varphi(z) = \frac{1}{\sqrt{2\pi}} e^{-z^2/2} \quad -\infty < z < \infty $$
en donde aparecen tres de los números más famosos de la historia de la matemática, $\sqrt{2}$, $\pi$ y $e$.

>[!info] Distribución Normal Patrón
La distribución acumulada correspondiente a $\varphi$, denotada por $\Phi$ no tiene fórmula cerrada,
$$ \Phi(z) = \int_{-\infty}^{z} \varphi(y) \, dy = \int_{-\infty}^{z} \frac{1}{\sqrt{2\pi}} e^{-y^2/2} \, dy $$
por lo cual no es posible calcular probabilidades integrando la curva. Sin embargo, existen aproximaciones tabuladas de diferentes maneras.


Densidad y Distribución 
![[Pasted image 20260918102529.png|324]]
Si Z tiene distribución normal estándar....
1. $$z > 0 \quad P(Z \geq z) = 1 - P(Z \leq z) = 1 - \Phi(z)$$![[Pasted image 20260918102646.png|471]]

2. $$z > 0 \quad P(Z \leq -z) = P(Z \geq z) = 1 - P(Z \leq z) = 1 - \Phi(z)$$
![[Pasted image 20260918102748.png|478]]

3. $$
\begin{align*}
z_1, z_2 > 0 \quad P(-z_1 \leq Z \leq z_2) &= P(Z \leq z_2) - P(Z \leq -z_1) \\
&= P(Z \leq z_2) - P(Z \geq z_1) \\
&= P(Z \leq z_2) - [1 - P(Z \leq z_1)] \\
&= \Phi(z_2) + \Phi(z_1) - 1
\end{align*}
$$

![[Pasted image 20260918102912.png]]
y si $z_1 = z_2 = z$
$$z > 0 \quad P(-z \leq Z \leq z) = 2\Phi(z) - 1$$
### Manejo de la tabla - Distribución Normal
1. Para el calculo de probabilidades de una normal estandar hay tablas generadas por metodos de integracion numerica.
2. La tabla de acumulación a cola a izquierda tabula los valores de
$$ \alpha = \Phi(z_\alpha) = P(Z \leq z_\alpha) $$
$$ z_\alpha > 0 \text{ y } Z \sim N(0, 1). $$
![[Pasted image 20260918103140.png]]

- Supongamos tener una tabla acumulada de cola a izquierda. En el centro de la tabla están las columnas con probabilidades $\alpha$ y en los márgenes de la tabla los valores de los cuantiles $z_{\alpha} > 0$. El margen izquierdo tiene los valores enteros y primer decimal de $z_{\alpha}$ y el margen superior el segundo decimal de $z_{\alpha}$.
-  Para encontrar $$ \alpha = P(Z < z_\alpha) = P(Z < 0.34) $$ se busca la fila del $z_{\alpha} = 0.3$ y luego se sigue esa fila hasta la columna del segundo decimal 0.04. La intersección de fila y columna da el valor $\alpha = 0.6331.
![[Pasted image 20260918105908.png|505]]
![[Pasted image 20260918105842.png|427]]

>[!example] Ejemplo: Manejo de la tabla
>1. Calcular las siguientes probabilidades:
1.1 $P(Z ≤ 1.45)$
1.2 $P(Z ≥ −0.37)$
1.3 $P(−1.56 ≤ Z ≤ 2.58)$
>2. Determinar el valor de la constante q tal que:
2.1 $\Phi(q) = 0.95$
>3. Determinar los percentiles $25, 50 y 75$
>
>La probabilidad de que $Z$ sea menor o igual que 1.45.
>$$P(Z \leq 1.45) = 0.9265$$
 La probabilidad de que Z sea mayor o igual que -0.37. $$\begin{align*}
P(Z \ge -0.37) &= 1 - P(Z \le -0.37) \\
&= 1 - [1 - P(Z \le 0.37)] \\
&= P(Z \le 0.37) = 0.6443
\end{align*}$$
La probabilidad de que X sea mayor que -1.56 y menor que 2.58 es $$ \begin{align*}
P(-1.56 \le Z \le 2.58) &= P(Z \le 2.58) + P(Z \le 1.56) - 1 \\
&= 0.9951 + 0.9406 - 1 = 0.9357
\end{align*}$$
> El valor de q tal que $\Phi(q) = 0.95$ es $1.645$
 Los percentiles 25, 50 y 75 son
$$0.675 = \eta(0.75) \quad 0 = \eta(0.5) \quad -0.675 = \eta(0.25)$$

>[!info] Variable aleatoria $N(\mu, \sigma^2)$
Sea Y una variable aleatoria con densidad dada por
$$f_Y(y) = \frac{1}{\sigma\sqrt{2\pi}}e^{-(y-\mu)^2/2\sigma^2} = \frac{1}{\sigma}\varphi\left(\frac{y-\mu}{\sigma}\right) \quad -\infty < y < \infty$$
La distribución de Y se llama normal con parámetros $\mu$ y $\sigma^2$ y se denota $Y \sim N(\mu, \sigma^2)$.
>![[Pasted image 20260918111137.png]]
La distribución acumulada correspondiente a $f_Y$, no tiene formula cerrada,
$$F_Y(y) = \int_{-\infty}^y f_Y(t)dt = \int_{-\infty}^y \frac{1}{\sigma\sqrt{2\pi}} e^{-(t-\mu)^2/2\sigma^2}dt$$
por lo cual no es posible calcular probabilidades integrando la curva
>![[Pasted image 20260918111241.png]]
>![[Pasted image 20260918111252.png]]

>[!notes] Propiedades N(μ, σ2)
Sea Y variable aleatoria con densidad $N(\mu, \sigma^2)$
>1. $f_Y(x) \ge 0 \forall x \in \mathbb{R}$ y $\int_{-\infty}^{\infty} f_Y(x) dx = 1$
>2. $f_Y$ es simétrica con respecto a $\mu$, o sea $f_Y(\mu - x) = f_Y(\mu + x)$
>3. $\lim_{x \to -\infty} f_Y(t) = \lim_{x \to \infty} f_Y(t) = 0$
>4. La gráfica tiene forma de campana.
>   ![[Pasted image 20260918111439.png]]
>5.  Si $Y$ tiene distribución normal con parámetro $\mu$ y $\sigma ^2$ entonces $Z = \frac{Y-\mu}{\sigma}$ tiene distribución normal estándar.
>6. si $Z$ es una variable normal estándar $Y = \mu + \sigma Z$ tiene distribución normal con parámetros $\mu$ y $\sigma^2$


Si $X$ es una variable con distribución normal $N(\mu, \sigma^2)$ entonces para calcular $P(a < X \leq b)$ primero se debe estandarizar la variable aleatoria $X$ creando $Z = \frac{X-\mu}{\sigma}$ y después usar la tabla de la $(0, 1)$. Por ejemplo
$$P(a \le X < b) = P\left(\frac{a - \mu}{\sigma} < Z < \frac{b - \mu}{\sigma}\right) = \Phi\left(\frac{b - \mu}{\sigma}\right) - \Phi\left(\frac{a - \mu}{\sigma}\right)$$
si $a < b$ son números reales, y $\Psi$ es la función de distribución acumulada de una variable aleatoria $N(0, 1)$.



>[!example] Ejemplo 
>Si X es una variable normal con media $\mu= 50$ y varianza $\sigma^2 = 100$ , calcule las siguientes probabilidades utilizando la distribución normal estándar.
>- La probabilidad de que X sea menor o igual que 40.
>- La probabilidad de que |X| (o sea, el valor absoluto de X ) sea menor o igual que 60.
>- La probabilidad de que |X| (o sea, el valor absoluto de X ) sea mayor o igual que 60
>  
>1.  La probabilidad de que X sea menor o igual que 40.
$$P(X \leq 40) = P(Z \leq \frac{40 - 50}{10}) = P(Z \leq -1) = 0.1587$$
>2.  La probabilidad de que |X| (o sea, el valor absoluto de X ) sea menor o igual que 60. $$\begin{align*}
P(|X| \le 60) &= P(-60 \le X \le 60) = P(X \le 60) - P(X \le -60) \\
&= P(Z \le \frac{60 - 50}{10}) - P(Z \le \frac{-60 - 50}{10}) \\
&= P(Z \le 1) - P(Z \le -11) = 0.8413 - 0 = 0.8413
\end{align*}$$ 
>3. La probabilidad de que |X| (o sea, el valor absoluto de X ) sea mayor o igual que 60.
$$P(|X| \ge 60) = 1 - P(|X| \le 60) = 1 - 0.8413 = 0.1587$$


>[!example] Ejemplo
>En una empresa hay dos maquinas disponibles A y B que cortan corchos, para ser usados en botellas de vino, tal que el 40 % son cortados con la maquina A y el resto con la B. 
>Se sabe que la maquina A corta corchos con diámetro que están normalmente distribuido con una media de 3 cm y una desviación estándar de 0,1 cm y la maquina B corta corchos con diámetro que están normalmente distribuido con una media de 3,04 cm y una desviación estándar de 0,02 cm.
> Para que un corcho sea aceptable para su uso debe cumplir que su diámetro este comprendido entre 2,9 y 3,1 cm.
>1. Cual de las dos maquinas producen mayor porcentaje de corchos aceptables?
>2. Se selecciona al azar un corcho de la producción, cual es la probabilidad de que el corcho sea aceptable?
>
>Datos del Problema
 Máquina A:
>1. Media $(\mu_A) = 3 cm$
>2. Desviación estándar $(\sigma_A) = 0.1 cm$
Máquina B:
>1. Media $(\mu_B) = 3.04 cm$
> 2. Desviación estándar $(\sigma_B) = 0.02 cm$
>-  Rango aceptable de diámetro: entre 2.9 cm y 3.1 cm
>- Proporción de corchos cortados por cada máquina:
>  1. Máquina A: 40%
>  2. Máquina B: 60% 
>    
>    a) Porcentaje de corchos aceptables por cada máquina
>- Para la Máquina A, la probabilidad de que un corcho sea aceptable es $$\begin{align*}
>  P(2.9 \le X \le 3.1) &= P \left( Z \le \frac{3.1 - 3}{0.1} \right) - P \left( Z \le \frac{2.9 - 3}{0.1} \right) \\
>  &= P(Z < 1) - P(Z < -1) \\ &= 0.8413 - 0.1587 = 0.6826 \end{align*}$$
Por lo tanto, el porcentaje de corchos aceptables producidos por la máquina A es 68.26%.
>
>- Para la Máquina B, la probabilidad de que un corcho sea aceptable con la máquina B es:
$$P(2.9 \le X \le 3.1) = P \left( \frac{2.9 - 3.04}{0.02} \le Z \le \frac{3.1 - 3.04}{0.02} \right)$$ $$ = P(Z < 3) - P(Z < -7) \approx 0.9987 - 0 = 0.9987$$
Por lo tanto, el porcentaje de corchos aceptables producidos por la máquina B es 99.87%.
 Conclusión: La máquina B produce un mayor porcentaje de corchos aceptables.
 >
 >b) Probabilidad de que un corcho seleccionado al azar sea aceptable
 Usamos el teorema de la probabilidad total considerando las proporciones de corchos producidos por cada máquina. $$P(\text{aceptable}) = P(\text{aceptable} \mid A) \cdot P(A) + P(\text{aceptable} \mid B) \cdot P(B)$$
Donde:
>1. P(aceptable | A) = 0.6826
> 2. P(aceptable | B) = 0.9987
> 3. P(A) = 0.40
> 4. P(B) = 0.60
> 
> Entonces:  $$\begin{aligned}
P(\text{aceptable}) &= (0.6826 \times 0.40) + (0.9987 \times 0.60) \\
&= 0.27304 + 0.59922 = 0.87226
\end{aligned}$$  La probabilidad de que un corcho seleccionado al azar sea aceptable es aproximadamente 0.872 o 87.2%
>  
>  Para la maquina que produce mayor porcentaje de corchos aceptables:
>  1. cual es la probabilidad de que el diámetro este comprendido entre 2,99 y 3,05 cm?
>  2. Si se seleccionan al azar 10 corchos de la producción, ¿cuál es la probabilidad de que el diámetro este comprendido entre 2,99 y 3,05 cm en por lo menos dos de los 10?
>  3. Hallar los percentiles 30 y 70 para la variable diámetro del corcho cortado con la máquina elegida.
>    
>  Para la máquina que produce mayor porcentaje de corchos aceptables (Máquina B):
>  1. La probabilidad de que el diámetro esté entre 2.99 y 3.05 cm es: $$\begin{align*}
P(2.99 \le X \le 3.05) &= P\left(\frac{2.99 - 3.04}{0.02} \le X \le \frac{3.05 - 3.04}{0.02}\right) \\
&= P(Z < 0.5) - P(Z < -2.5) \\
&= 0.6915 - 0.0062 = 0.6853
\end{align*}$$ esto es, 68.53%
>2. Observemos que la probabilidad de que un corcho tenga un diámetro en ese intervalo es p = 0.685. Si tenemos una muestra de tamaño 10, X el número de corchos con diámetro en el intervalo tiene distribución binomial B(n = 10, p = 0.685).
$$ P(X \ge 2) = 1 - P(X < 2) = 1 - [P(X = 0) + P(X = 1)] $$  
>
>$$P(X = 0) = \begin{pmatrix} 10 \\ 0 \end{pmatrix} \cdot 0.685^0 \cdot (1 - 0.685)^{10} = (0.315)^{10} \approx 0.0007$$
$$P(X = 1) = \begin{pmatrix} 10 \\ 1 \end{pmatrix} \cdot 0.685^1 \cdot (1 - 0.685)^9 \approx 10 \cdot 0.685 \cdot 0.0007 = 0.0048$$
Entonces:
$$P(X \geq 2) = 1 - (0.0007 + 0.0048) = 1 - 0.0055 = 0.9945$$
La probabilidad de que el diámetro esté entre 2.99 y 3.05 cm en por lo menos dos de los 10 corchos es aproximadamente 0.9945 o 99.45%.
> 
>3. Hallar los percentiles 30 y 70 para el diámetro de los corchos Para la máquina B, usamos la distribución normal con media 3.04 y desviación estándar 0.02.
>- El valor Z correspondiente al percentil 30 es aproximadamente -0.524.
$$X_{30} = \mu + Z \cdot \sigma = 3.04 + (-0.524) \cdot 0.02 = 3.04 - 0.01048 = 3.02952$$ El percentil 30 es aproximadamente 3.0295 cm.
>- El valor Z correspondiente al percentil 70 es aproximadamente 0.525.
$$X_{70} = \mu + Z \cdot \sigma = 3.04 + 0.525 \cdot 0.02 = 3.04 + 0.0105 = 3.0505$$
El percentil 70 es aproximadamente 3.0505 cm.



## Distribución Chi Cuadrado 

>[!info] Variable aleatoria $X \sim \chi^2 (k)$ 
>Se dice que una variable aleatoria $X$ tiene distribución Chi cuadrado con $k$ grados de libertad, $X \sim \chi ^2 (k)$, si función densidad de probabilidad de X es
$$f_X(x, k) = \begin{cases} \frac{1}{2^{k/2}\Gamma(k/2)} x^{\frac{k}{2}-1}e^{-\frac{x}{2}} & \text{si } x \ge 0 \\ 0 & \text{en otro caso} \end{cases}$$
Notación: $X \sim \chi ^2 (k) = \Gamma (k/2, \lambda= 1/2) = \Gamma(k/2, \beta = 2)$.
> ![[Pasted image 20260923215437.png]]


>[!notes] Propiedades
> 1. Si $X \sim \chi ^2 (k)$ entonces  $$E(X) = k \quad Var(X) = 2k$$
>2. Si $Z_1, · · · , Z_n$ son variables normales estándar independientes, entonces la variable definida como $$X = Z_1^2 + \cdots + X_n^2$$
tiene distribución Chi cuadrado con n grados de libertad.
> 3. Una variable Chi cuadrado con 2 grados de libertad es una variable con distribución exponencial con tasa λ = 1/2
$$X \sim \chi^2(2) = \Gamma(2/2, \lambda = 1/2) = \Gamma(1, \lambda = 1/2) = \mathcal{E}(1/2)$$

### Distribución Chi cuadrado con k grados de libertad
### Cuantiles
Si X es una variable chi cuadrado con $n$ grados de libertad, entonces para todo $\alpha \in (0, 1)$ la cantidad  ${\chi ^2}_{\alpha,n}$esta definida tal que
$$P(X \geq \chi_{\alpha,n}^2) = \alpha$$
![[Pasted image 20260923220741.png]]![[Pasted image 20260923220801.png]]

>[!example] Ejemplo 
>Si X es una variable Chi cuadrado con 26 grados de libertad, determine P( X < 30.435)
$$P(X \leq 30.435) = 1 - P(X \geq 30.435) \sim 1 - 0.25 = 0.75$$
>Hallar los puntos críticos para una $X \sim \chi ^2 (10)$ tales que
>1. el área de la cola superior sea igual a 0.025
$$P(X \geq \chi_{10}^2) = 0.025 \text{ entonces } \chi_{10}^2 = 20.483$$
>2. el área de la cola inferior sea igual a 0.025
$$P(X \leq \chi_{10}^2) = 0.025 \text{ entonces } P(X \geq \chi_{10}^2) = 1 - 0.025 = 0.975$$
$$\chi_{10}^2 = 3.247$$

>[!example] Ejemplo
>Supongamos que estamos intentando localizar un objetivo en un espacio tridimensional, y que los errores de las coordenadas (en metros) del punto elegido son variables aleatorias normales independientes con media 0 y desviación estándar 2. Encuentre la probabilidad de que la distancia entre el punto elegido y el objetivo supere los 3 metros.
>Si D es la distancia entonces
$$D^2 = X_1^2 + X_2^2 + X_3^2$$
donde $X_i$ es el error en la i-esima coordenada y por hipótesis tienen distribución normal con media cero y desviación estándar 2. Defino $Z_i = X_i / 2, \ \  ,i=1,2,3$ entonces $Z_i$ son todas variables aleatorias normales estándar y $$ \begin{align*}
P(D^2 > 9) &= P(X_1^2 + X_2^2 + X_3^2 > 9) \\
&= P(Z_1^2 + Z_2^2 + Z_3^2 > 9/4) \\
&= P(\chi_3^2 > 2.25) \sim 0.525
\end{align*}$$
pues 2.55 está entre 2.109 (p= 0.55) y 2.366(p=0.5)

## Distribución log normal 

>[!notes] Definición
>Se dice que una variable aleatoria X tiene distribución Log-normal con parámetros $\mu$ y $\sigma ^ 2$ si la variable aleatoria $Y = \ln X \sim N (\mu, \sigma ^2)$ 
>
$$f_X(x) = \begin{cases} \frac{1}{x\sqrt{2\pi\sigma^2}}e^{\frac{(\ln(x)-\mu)^2}{2\sigma^2}} & \text{si } x > 0 \\ 0 & \text{en otro caso} \end{cases}$$
con $\mu \in \mathbb{R}$ . Notación $X \sim  \text{log normal}(\mu,  \sigma ^ 2)$


$$Y=\log(X) \sim N(\mu, \sigma^2)$$

Entonces $f(\ln x) = \frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{1}{2}(\frac{\ln x-\mu}{\sigma})^2}$ para $-\infty < \ln x < +\infty$.

$$y = h(\ln x) = e^{\ln x} = x \quad \text{con} \quad y > 0, \quad \text{luego } h^{-1}(y) = \ln x$$

$$Entonces \quad f_Y(y) = f_X(h^{-1}(y)) \left| \frac{dh^{-1}(y)}{dy} \right| = f_{\ln x}(\ln x) \frac{d\ln x}{dx}$$

$$f_X(x) = \frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{1}{2}(\frac{\ln x-\mu}{\sigma})^2} \left(\frac{1}{x}\right) = \frac{1}{x\sigma\sqrt{2\pi}} e^{-\frac{1}{2}(\frac{\ln x-\mu}{\sigma})^2} \quad \text{para } x > 0.$$

**Proposición**

Sea X una variable aleatoria con distribución Log-normal con parámetros \mu y \sigma entonces

1. La función de distribución acumulada es

$$F(x) = \begin{cases} \Phi\left(\frac{\ln(x)-\mu}{\sigma}\right) & \text{si } x > 0 \\ 0 & \text{en otro caso} \end{cases}$$

donde $\Phi$ es la función de distribución acumulada de la normal estándar.

$$2. E(X) = e^{\mu + \sigma^2/2} y Var(X) = e^{2\mu + \sigma^2}[e^{\sigma^2} - 1]$$
>[!notes]  $Y=log(X) \sim N(\mu, \sigma ^2)$
$$F(x, \mu, \sigma) = P(X \le x) = $$ $$P(\ln(X) \le \ln(x)) = P(Z \le (\ln(x)-\mu)/\sigma) = \Phi((\ln(x)-\mu)/\sigma)$$
>![[Pasted image 20260923222500.png]]


 >[!info] Teorema. Si $X \sim$ $\text{Lognormal}(\mu, \sigma$) entonces,
$$E(X^n) = \exp\left(\frac{n^2\sigma^2}{2} + n\mu\right)$$
 >
 >$$E(X^n) = \int_0^\infty \frac{x^n}{x\sigma\sqrt{2\pi}} e^{-\frac{1}{2}\left(\frac{\ln x - \mu}{\sigma}\right)^2} dx = \frac{1}{\sigma\sqrt{2\pi}} \int_0^\infty x^{n-1} e^{-\frac{1}{2}\left(\frac{\ln x - \mu}{\sigma}\right)^2} dx$$
>
$$Haciendo, \quad t = \frac{\ln x - \mu}{\sigma} \quad luego \quad x = e^{\sigma t + \mu} \quad y - \infty < t < +\infty.$$
>
$$dt = \frac{dx}{x\sigma} \quad \Rightarrow \quad \sigma x^n dt = x^{n-1} dx \quad \Rightarrow \quad \sigma e^{n\sigma t + n\mu} dt = x^{n-1} dx \quad \Rightarrow$$
>
$$E(X^n) = \frac{1}{\sigma\sqrt{2\pi}} \int_{-\infty}^{+\infty} e^{-t^2/2}(\sigma e^{n\sigma t + n\mu}) dt$$
>
$$E(X^n) = \frac{1}{\sqrt{2\pi}}\int_{-\infty}^{+\infty} exp\left[-\frac{1}{2}(t^2 - 2n\sigma t + n^2\sigma^2)\right] exp\left(\frac{n^2\sigma^2}{2} + n\mu\right) dt$$
>
$$E(X^n) = exp\left(\frac{n^2\sigma^2}{2} + n\mu\right) \int_{-\infty}^{+\infty} \frac{1}{\sqrt{2\pi}} exp\left[-\frac{1}{2}(t - n\sigma)^2\right] dt$$
$$ Finalmente, \quad E(X^n) = exp\left(\frac{n^2\sigma^2}{2} + n\mu\right). \quad \text{LQQD.} $$



>[!example] Ejemplo
 Sea X la medida de elasticidad MDE estándar de piso de vigueta de madera de pino grado 2, modelado con una distribución lognormal de parámetros $\mu=0.375$ y $\sigma=0.25$.  ¿Cual es el valor de c tal que solo el 1% de todos los sistemas tienen MDE que excede c?
$$0.99 = P(X≤c) = P(\ln(X)≤\ln(c)) = P(Z≤(\ln(x)-μ)/σ) = \Phi((\ln(c)-μ)/σ)$$
$$2.326= (\ln(c)-μ)/σ por lo cual c= 2.605$$
>![[Pasted image 20260923223129.png]]



