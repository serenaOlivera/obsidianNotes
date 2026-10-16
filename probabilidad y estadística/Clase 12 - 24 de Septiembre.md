
Segunda parte de la materia!!!

# Confianza y Probabilidad

---
![[Pasted image 20261001081810.png|510]]
![[Pasted image 20261001081823.png|516]]
![[Pasted image 20261001081843.png|482]]
![[Pasted image 20261001081910.png|502]]


>[!info] Regla empírica
Establece que si una variable aleatoria está normalmente distribuida, entonces:
>1. Aproximadamente 68% de las observaciones caerán entre más y menos una desviación estándar de la media.
>2. Aproximadamente 95% de las observaciones caerán entre más y menos dos desviaciones estándar de la media.
>3. Prácticamente todas, o 99.7% de las observaciones caerán entre más y menos tres desviaciones estándar de la media.(Lind, Marchal, and Wathen 2015).

¿Como se calcula esto?

- Una desviación estándar de la media es igual al valor z=1.

- Al hablar de la tabla de probabilidad normal estándar, el valor z=1 corresponde a una probabilidad de 0.8413. Por lo tanto, ¿qué porcentaje de las observaciones caerá entre más y menos una desviación estándar de la media? Es dos veces el área que excede a 0.5, esto es 2x(0.8413-0.5), lo que da 0.6826, o aproximadamente

- El 68% de las observaciones están entre más y menos una desviación estándar de la media
![[Pasted image 20261001082218.png|564]]

![[Pasted image 20261001082255.png|566]]

![[Pasted image 20261001082318.png]]

>[!question] ¿Si la distribución no es normal?
>- Cuando charlamos sobre exactitud y precisión, sobre la regla empírica, dibujamos una distribución normal.
>  - ¿Qué podemos hacer cuando la distribución no es normal?
> - ¿Hay alguna forma de dar confianza?
>    $$P(|X-\mu|<\sigma) = 0.68$$



# Desigualdad de Chebyshev

---

## Desigualdad de Chebyshev

>[!info] Lema
>Sea X una variable aleatoria positiva con media $\mu$, y sea $t$ un número real positivo. Entonces $$P(X \ge t) \le \frac{E(X)}{t}$$

>[!info] Desigualdad de Chebyshev
>Sea $X$ una variable aleatoria con media $\mu$ y varianza $\sigma^2$. Entonces, para cada $t > 0$ $$P(|X - \mu| \ge t) \le \frac{\sigma^2}{t^2}$$


1. La proposición anterior dice que si $\sigma^2$ es muy pequeño, existe una probabilidad muy alta de que $X$ no se desvíe mucho de $\mu$.
2. Podemos realizar una cota en función de la varianza.

>[!info] Lema
Sea X una variable aleatoria con media $\mu$ y varianza $\sigma^2$. Entonces,$$
\begin{align*}
P(|X - \mu| \ge k\sigma) &\le \frac{1}{k^2} \\
P(|X - \mu| < k\sigma) &\ge 1 - \frac{1}{k^2}
\end{align*}$$

![[Pasted image 20261001082828.png|587]]


>[!example] Ejemplo
Un fabricante de tornillos sabe que el 5% de su producción es defectuosa. Por ello garantiza que si una entrega de 10000 piezas tiene más de $a$ defectuosos se reembolsará el dinero pagado por el cargamento. ¿Cuán chico puede el fabricante escoger el valor $a$ para que no deba devolver el dinero del cargamento más del 1% de las veces?
>1. Supongamos que el lote de 10000 tornillos es una muestra aleatoria de la población (infinita) de tornillos que produce la fábrica.
>2. Sea p = 0.05 la probabilidad de elegir un tonillo defectuoso de la población. Entonces X, el número de defectuosos del lote de 10000 tornillos, tiene distribución Binomial con media $np$ y varianza $np(1 − p)$, y el evento A= devolver el cargamento puede ser pensado como $$A = (X > a) = (X - np > a - np)$$
>  3. Queremos escoger a tal que $$P(\text{ devolver el cargamento }) = P(X > a) \leq 0.01$$
>  4. Sabemos por Chebyshev que $$P(|(X - np| > t) \leq \frac{np(1-p)}{t^2} < 0.01 \text{ si } t \geq \sqrt{\frac{10000 * 0.0475}{0.01}}$$
>  5. Entonces $t \geq 218$ garantiza que $$P(A) = P(X - np > a - np) \leq P(|X - np| > t) \leq 0.01$$ por lo cual $a - np = t \geq 218$ implica que
$a = 218 + np = 218 + 500 = 718$ es un valor conservativo para $a$.


## Observaciones

- Solo uso la distribución binomial para calcular la media y la varianza
- Puedo usar el TCL para sacar un valor mucho más preciso de a. 
- Entonces, para qué sirve la desigualdad de Chebyshev?

Si tengo valores históricos de media y varianza y no puedo asegurar una distribución, ni que funcione el TCL, siempre puedo acotar con Chebyshev



# Ley de los grandes números
---

1. Hemos dicho al comienzo del curso que si una moneda honesta se tira muchas veces, la proporción de caras obtenida estará cerca de 1/2.
2. La ley de los grandes números formaliza esta afirmación empírica.
3. Los resultados de los tiros consecutivos de la moneda son variables aleatorias independientes X¡ que toman valores 0 o 1 según la i-esima repetición es cara o número, y la proporción de caras en los n tiros es
$$ \overline{X}_n = \frac{1}{n} \sum_{i=1}^{n} X_i $$

>[!info] Definición
>Sea $\{X_n \}$ una sucesión de variables aleatorias. Se dice que $\{X_n\}$ converge en probabilidad a $Y$ si para todo $\varepsilon > 0$ $$ \lim_{n \to \infty} P(|X_n - Y| \ge \varepsilon) = 0 $$


>[!info] Ley débil de los grandes números
>Sea $X_1, . . ., X_n$ variables aleatorias independientes con $E(X_i) = \mu$ y $Var(X_i) = \sigma^2$. Sea $$ \overline{X}_n = \frac{1}{n} \sum_{i=1}^n X_i $$
>Entonces para cada t > 0$$ \begin{aligned} P(|\overline{X}_n - \mu| \ge \varepsilon) & \le \frac{\sigma^2}{n\varepsilon^2} \\ P(|\overline{X}_n - \mu| < \varepsilon) & \ge 1 - \frac{\sigma^2}{n\varepsilon^2} \end{aligned} $$ Por lo cual $$ \lim_{n \to \infty} P(|\overline{X}_n - \mu| \ge \varepsilon) = 0 \quad \lim_{n \to \infty} P(|\overline{X}_n - \mu|< \varepsilon) = 1 $$ y $\{\overline{X}_n\}$ converge en probabilidad a la variable aleatoria concentrada en $\mu$.


**Observación**
1. Es importante observar que la noción de convergencia usual en cálculo $a_n \to a$ implica que $a_n$ se transforma cuando $n$ varía y ser acerca a $a$ tanto como uno quiera, siempre que $n$ sea suficientemente grande.
2. En cambio la convergencia enunciada en la ley de los grandes números implica que si $X_n \to X$ en probabilidad, entonces la probabilidad del suceso ($|X_n - X| < \epsilon$) puede hacerse arbitrariamente próxima a 1 tomando $n$ suficientemente grande.

>[!Example] Ejemplo: Frecuencia relativa
>-  Sea A un suceso con $P(A) = p$, que es uno de los resultados posibles de un experimento.
>- Supongamos que repetimos el experimento $n$ veces en forma independiente y consideramos las variables aleatorias indicadoras $X_i$ que valen 1 si el i-esimo experimento resulta en A y cero si no.
>- Estas variables resultan Bernoulli independientes y el promedio $$ \hat{p}_n = \frac{1}{n} \sum_{i=1}^{n} X_i $$ es la frecuencia relativa del evento $A$ en las $n$ repeticiones.
>- Como $E(X_i) = p$, y $Var(X_i) = p(1 − p)$, por la ley de los grandes números
$$ \hat{p}_n \xrightarrow[n \to \infty]{} p $$
esto es, la frecuencia relativa del evento A converge débilmente (en probabilidad) a la probabilidad del evento A.

>[!example] Ejemplo 
Tiramos un dado 20 veces ¿Cuál es la probabilidad de que la frecuencia relativa $\hat{p}_n$ de veces que aparece el cuatro difiere de la probabilidad real en menos de 0.1? (APROXIMADA)
>- La ley de los grandes números afirma que $$P(|\hat{p}_n - p| < \varepsilon) \geq 1 - \frac{p(1-p)}{n\varepsilon^2}$$
>- En este caso sabemos que la verdadera probabilidad $p$ es 1/6, por lo cual $p(1-p) = 1/6(1-1/6) = 0.14$. Como $\varepsilon = 0.1$ y $n = 20$ resulta
$$P(|\hat{p}_n - (1/6)| < \frac{0.14}{0.1}) \geq 1 - \frac{20(0.01)}{20(0.01)} = 1 - 0.7 = 0.3$$

>[!example] Ejemplo
¿Cuantas veces tenemos que tirar el dado para que estemos un 90% veces seguros de que la frecuencia relativa pn de veces que aparece el cuatro difiere de la probabilidad real en menos de 0.1?(CONSERVATIVO!!)
>- La ley de los grandes números afirma que $$P(|\hat{p}_n - p| < \varepsilon) \geq 1 - \frac{p(1-p)}{n\varepsilon^2}$$
>- en este caso,$$P(|\hat{p}_n - p| < 0.1) \geq 1 - \frac{0.14}{n(0.1^2)} = 0.9$$  $$por \, lo \, cual \quad \frac{0.14}{n(0.1^2)} = 0.1 \, y \, n = \frac{0.14}{(0.1)^3} = 140.$$

## Aproximaciones Normales: Binomial
La ley de los grandes números tiene como corolario fundamental dar una estimación de la probabilidad del cometer por lo menos un error $\varepsilon$ al aproximar $p$, la probabilidad de un evento, usando $\hat{p}_n$, la frecuencia relativa de este.
Dicha probabilidad se achica cuando el número de repeticiones independientes del experimento aumenta.

$$P(|\hat{p}_n - p| \geq \varepsilon) \leq \frac{p(1-p)}{n\varepsilon^2} \leq \frac{1}{4n\varepsilon^2} = \tau$$

Si deseo calcular cualquier otra probabilidad que involucre la variable $\hat{p}_n$ debo estudiar qué distribución tiene este promedio.

## Ejemplos

---
>[!example] Ejemplo
Sea $p$ la proporción real de votantes a favor del candidato Marquez en la población, y sea $\hat{p}_n$ la proporción muestral de votantes a favor de Marquez, calculado sobre una muestra aleatoria de tamaño $n$.
(a) Acotar $P (|\hat{p}_{900} − p| \geq 0.025)$ y comparar con la cota encontrada usando la ley de los grandes números.
(b) Calcular un valor de $n$ que garantice que $P (|\hat{p}_n − p| \geq 0.025) \leq 0.01$. y comparar con el $n$ encontrado usando la ley de los grandes números.
>
 >- Como la variable $X$ que mide el número de votantes de la muestra a favor de Marquez tiene distribución binomial de parámetros $n$ y $p$, usando la aproximación normal a la binomial resulta $$\begin{align*}
P(|\hat{p}_{900} - p| \ge 0.025) &= P(|X - np| \ge n0.025) \\
&= P\left( \left| \frac{X - np}{\sqrt{np(1-p)}} \right| \ge \frac{n0.025}{\sqrt{np(1-p)}} \right) \\
&= P\left( |Z| \ge \frac{n0.025}{\sqrt{np(1-p)}} \middle| \right) \\
&= 2\Phi\left(-\frac{900*0.025}{\sqrt{900\frac{1}{4}}}\right) \\
&= 2\Phi(-1.5) = 2*0.0668 = 0.1336
\end{align*}$$
>- Debemos observar que la ley de los grandes números solo nos permite decir que
$$P(|\hat{p}_{900} - p| \geq 0.025) \leq 0.44$$ mientras que la verdadera probabilidad es tres veces menor.
>- Si queremos encontrar un valor de n que garantice que  $$P(|\hat{p}_n - p| \geq 0.025) \leq 0.01$$ entonces  $$\begin{align*}
P(|\hat{p}_n - p| \ge 0.025) &= P\left( \left| \frac{X - np}{\sqrt{np(1-p)}} \right| \ge \frac{n0.025}{\sqrt{np(1-p)}} \right) \\
&= P\left( |Z| \ge \frac{n0.025}{\sqrt{np(1-p)}} \middle| \right) \\
&= 2\Phi\left(-\frac{n*0.025}{\sqrt{n\frac{1}{4}}}\right) = 0.01
\end{align*}$$ por lo cual $−2.575 = z−0.005 = - \frac{n * 0.025}{\sqrt{n \frac{1}{4}}} = −n^{1/2} 0.05$ y $n = 2653$.
>- Este es un tamaño de muestra grande pero 20 veces más chico que el calculado con la ley de los grandes números.


 Consistencia
---
Las leyes de los grandes números explican por qué el promedio de una muestra al azar de una población de gran tamaño tenderá a estar cerca de la media de la población completa.

 >[!example] Lanzamiento de monedas o dados
Imagina que tiras tres veces un dado normal de seis caras. Puedes obtener resultados como 6, 2 y 5. La media es de 4,3, superior al valor esperado de 3,5. Pero ahora tiras el dado 100 veces, y luego 1.000 veces. A medida que aumenta el número de tiradas, tu media se acerca a 3,5. La ley de los grandes números suaviza la aleatoriedad a lo largo del tiempo.![[Pasted image 20261001200904.png]]



>[!example] Estadísticas deportivas
Los deportistas pueden tener días buenos y días malos. Un quarterback puede completar 9 de cada 10 pases en un partido, un impresionante 90%. Pero eso no significa que siempre jueguen a ese nivel. A lo largo de toda una temporada, con cientos de lanzamientos, el porcentaje de finalización empieza a nivelarse. Esa estadística de toda la temporada da una idea mucho mejor de la capacidad real del jugador.![[Pasted image 20261001201021.png]]

>[!example] Agrupación de riesgos del sector asegurador
Las compañías de seguros no saben exactamente cuánto les costará una persona. Algunas personas no utilizan ningún tipo de atención médica, mientras que otras sí.
>
Pero cuando observas a un grupo grande de personas, esos altibajos se equilibran. Al agrupar el riesgo entre miles de asegurados, las aseguradoras pueden predecir el costo medio con mayor precisión.
Esto les permite fijar precios justos (primas) al tiempo que se mantienen financieramente estables.![[Pasted image 20261001201116.png]]


>[!example] Juegos de casino y ventaja de la casa
Los casinos crean una ligera ventaja en todos los juegos. Si juegas al blackjack, puedes ganar cinco manos seguidas o perder diez. Pero en miles de partidas, el resultado medio favorece al casino.
Por ejemplo, si la ventaja de la casa es del 0,5%, entonces, con el tiempo, el casino espera ganar 50 céntimos por cada 100 $ apostados de media. Puede que eso no ocurra en una sesión corta, pero a lo largo de millones de jugadas, se acumula exactamente como se esperaba. ![[Pasted image 20261001201251.png]]

>[!example] Pruebas A/B en empresas tecnológicas
Supongamos que una empresa quiere probar dos versiones del botón de un sitio web: Botón A y Botón B. Después de que 20 personas prueben cada uno, el Botón A parece mejor. Pero no son datos suficientes para confiar en el resultado.
Ahora deja que 20.000 usuarios vean las dos cosas. A medida que aumenta el tamaño de la muestra, los porcentajes medios de clics se hacen más fiables, y el botón con mejores resultados se hace más evidente.
Por eso las empresas confían en muestras grandes para las pruebas A/B. La ley de los grandes números les ayuda a evitar falsos positivos y a tomar decisiones más inteligentes.
>![[Pasted image 20261001201359.png]]


