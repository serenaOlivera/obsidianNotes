## Vectores Discretos
---
>[!example] Distribución Conjunta: Ejemplo
Una gran tienda de departamentos vende camisas deportivas
>1. en tres talles (pequeño, mediano y grande),
>2. en tres modelos (a cuadros, estampados y de franjas)
>3. con dos largos de mangas (corta y larga).
>
Si $\Omega$ es el conjunto de todas las camisas vendidas, sea
>1. X la variable indicadora del talle,
>2. Y la variable indicadora del modelo
>3. W la variable indicadora del largo de manga.
Las siguientes tablas presentan las proporciones de camisas vendidas que caen en varias combinaciones de categorías.
![[Pasted image 20260923231218.png]]
>
>
>1. ¿Que representa la tabla? 
>2. ¿Cuál es la función de densidad puntual de la variable X?
>3. ¿Cuál es la función de densidad puntual de la variable Y ? 
>4. ¿Cuál es la función de densidad puntual de la variable W ? 
>5. ¿Puedo calcular funciones de las variables a partir de esta información? $$X + Y + Z; \quad X^2 - Y; \quad [\sin(X) + \cos(Y)]W$$
>La tabla muestra las probabilidades de las intersecciones de todos los valores de las indicadoras.
$$P((\text{pequeño, franjas, manga larga}))$$
## Codificación
Codifiquemos las variables, $X = 1$ si el talle es pequeño, $X = 2$ si el talle es mediano y $X = 3$ si el talle es grande. $Y = 1$ si el modelo es a cuadros, $Y = 2$ si el modelo es estampado y $Y = 3$ si el modelo es a franjas; $W = 1$ si la camisa es manga corta y $W = 2$ si la camisa en manga larga.
$$P((\text{pequeño, franjas, manga larga})) = P(X = 1, Y = 3, W = 2)$$

>[!notes] Distribución Conjunta: Definición
>**Densidad de masa**
Sean $X_1, . . . , X_n$ un vector aleatorio, es decir, una $n$-upla donde cada coordenada es una variable aleatorias discreta sobre el espacio de probabilidad $(\Omega, A, P)$, se define la función densidad de masa conjunta del vector $(X_1, . . . , X_n)$ como
$$p(x_1, \dots, x_n) = P[(X_1 = x_1, \dots, X_n = x_n)] \quad \forall x_i \in \mathbb{R}$$
>
**Distribución acumulada conjunta**
Se define la función de distribución acumulada conjunta del vector (X1, . . . , Xn) como
$$F(x_1, \dots, x_n) = P[(X_1 \leq x_1, \dots, X_n \leq x_n)] \quad \forall x_i \in \mathbb{R}$$

>[!notes] Propiedades
La función densidad de probabilidad (densidad de masa) conjunta del vector $(X_1, · · · , X_n)$ cumple
>1. $0 \leq p(x_1, · · · , x_n) \leq 1$
>2. $P[(X_1 = x_1, · · · , X_n = x_n) \in A] = \sum_{(x_1,···,x_n) \in A} p(x_1, · · · , x_n), \forall A \subset \mathbb{R}^ n$
>3. $\sum_{(x_1,···,x_n) \in \mathbb{R}^n} p(x_1,···,x_n) = 1$

>[!info] Ejemplo
> - Notemos que conocer la función de masa conjunta nos dice mucho mas que conocer las funciones de masa puntuales individuales.
> - Consideremos el experimento de tirar una moneda honesta. Las variables indicadoras del evento ’cara’ y del evento ’contracara’ toman los mismos valores con igual probabilidad. Sin embargo, de la distribución conjunta surge la información de que se relacionan linealmente X = 1 − Y.
> 1. ¿Cuál es la función de densidad puntual de la variable X?
$$P(X=1) =$$  $$P(X=1,Y=1,W=1) + P(X=1,Y=1,W=2) + P(X=1,Y=2,W=1)$$ $$+ P(X=1,Y=2,W=2) + P(X=1,Y=3,W=1) + P(X=1,Y=3,W=2) =$$ $$0.04 + 0.03 + 0.02 + 0.02 + 0.05 + 0.03 = 0.19$$
> $$\begin{align*}
P(X = 2) &= P(X = 2, Y = 1, W = 1) + P(X = 2, Y = 1, W = 2) \\
&\quad + P(X = 2, Y = 2, W = 1) + P(X = 2, Y = 2, W = 2) \\
&\quad + P(X = 2, Y = 3, W = 1) + P(X = 2, Y = 3, W = 2) \\
&= 0.08 + 0.1 + 0.07 + 0.05 + 0.12 + 0.07 \\
&= 0.49
\end{align*} $$
>$$\begin{align*}
P(X = 3) &= P(X = 3, Y = 1, W = 1) + P(X = 3, Y = 1, W = 2) \\
&\quad + P(X = 3, Y = 2, W = 1) + P(X = 3, Y = 2, W = 2) \\
&\quad + P(X = 3, Y = 3, W = 1) + P(X = 3, Y = 3, W = 2) \\
&= 0.03 + 0.04 + 0.07 + 0.02 + 0.08 + 0.08 \\
&= 0.32
\end{align*}$$

>[!example] Ejemplo Vector $(X, Y)$
> 1. ¿Cuál es la función densidad de masa conjunta del vector (X, Y)?
La tabla es la función de masa conjunta del vector (X; Y; W). Si unimos los eventos relacionados con los valores de W obtenemos la distribución conjunta de (X, Y)
$$P(X = x, Y = y) = P(X = x, Y = y, W = 1) + P(X = x, Y = y, W = 2)$$
> ![[Pasted image 20260924213704.png]]
> Observemos que el centro de la tabla suma 1, como debe ser y todos los valores son no negativos.
> También podemos observar que la función de masa de X puede ser obtenida sumando cada columna de la tabla, y los valores de la función de masa de Y pueden ser obtenidos sumando a través de las filas de la tabla.


>[!info] Marginales
Sea $(x_1, · · · , X_n)$ un vector aleatorio discreto sobre el espacio de probabilidad $(\Omega, A, P)$, se definen las funciones densidad de masa marginales de Xi como
$$p_{X_i}(x_i) = \sum_{x_j / j \neq i} p(x_1, \cdots, x_n)$$
>![[Pasted image 20260924213937.png]]
>¿Como encontramos la varianza y esperanza de las variables X e Y?
>$E(Y) = \sum xp_Y(y) = 1 \times 0.32 + 2 \times 0.25 + 3 \times 0.43 = 2.11$
 $Var(Y) = E(Y^2) - [E(Y)]^2 =$ $[1^2 \times 0.32 + 2^2 \times 0.25 + 3^2 \times 0.43] - (2.11)^2 = 0.73$

###  Teorema
Sea $(X_1, . . . , X_n)$ un vector aleatorio $n$-dimensional. Sea $g : \mathbb{R}^ n \rightarrow \mathbb{R}$ una función, entonces $g(X_1, . . . , X_n)$ es una variable aleatoria cuya esperanza es
$$E[g(X_1, \dots, X_n)] = \sum_{(x_1, \dots, x_n)} g(x_1, \dots, x_n)p(X_1, \dots, X_n)$$

#### Corolario
$$E(X + Y) = E(X) + E(Y)$$
Mas generalmente
$$E(g_1(X) + g_2(Y)) = E(g_1(X)) + E(g_2(Y))$$
Este resultado se extiende a un número finito de variables
$$E(X_1 + \cdots + X_n) = \sum_{i=1}^{n} E(X_i)$$
Mas generalmente
$$E(g_1(X_1) + \cdots + g_n(X_n)) = \sum_{i=1}^{n} E(g_i(X_i))$$

>[!example] Ejemplo
>Supongamos tirar una moneda honesta tres veces. Definimos las siguientes variables aleatorias, $X_1$ representa el número de caras en la primer tirada, $X_2$ representa el número de caras en las primeras dos tiradas y $X_3$ es el total de caras en las tres tiradas.
>1. Encuentre la densidad discreta conjunta de $X_1$ y $X_3$ y las densidades marginales $p_{X_1}$ y $p_{X_3}$.
>   2. Calcule la esperanza de $X_1 + X_3$
>   3. Encuentre la densidad discreta conjunta de las tres variables.
>   4. Calcule $P(X_1 + X_3 = 2)$ y $P(X_1 + 1 ≤ X_3)$. 
>
>Si llamamos cara por c y número por s, el espacio muestral Ω es
$$ \Omega = \{ (ccc), (ccs), (csc), (scc), (ssc), (scs), (css), (sss) \} $$
La densidad conjunta entre X1 y X3 se calcula de la siguiente forma: $$\begin{align*}
p_{X_1, X_3}(0, 0) &= P(X_1 = 0, X_3 = 0) = P((sss)) = \frac{1}{8} \\
p_{X_1, X_3}(0, 1) &= P(X_1 = 0, X_3 = 1) = P((scs), (scs)) = \frac{2}{8} \\ p_{X_1, X_3}(0, 2) &= P(X_1 = 0, X_3 = 2) = P((scc)) = \frac{1}{8}
\end{align*}$$
los demás valores se calculan de forma similar.
> La tabla queda:
> ![[Pasted image 20260924214757.png]]
> La esperanza de $X_1 + X_3$ es 
> $$\begin{align*}
E[X_1 + X_3] &= [0 + 0]1/8 + [0 + 1]2/8 + [0 + 2]1/8 + [0 + 3]0 \\
&\quad + [1 + 0]0 + [1 + 1]1/8 + [1 + 2]2/8 + [1 + 3]1/8 \\
&= 2 \end{align*}$$
> - Para calcular la densidad conjunta de las tres variables operamos de la misma forma, solo que tenemos que armar una tabla más complicada $$\begin{align*}
p_{X_1, X_2, X_3}(0, 0, 0) &= P(X_1 = 0, X_2 = 0, X_3 = 0) = P((sss)) = \frac{1}{8} \\
p_{X_1, X_2, X_3}(1, 1, 1) &= P(X_1 = 1, X_2 = 1, X_3 = 1) = P((css)) = \frac{1}{8} \\
p_{X_1, X_2, X_3}(1, 2, 2) &= P(X_1 = 1, X_2 = 2, X_3 = 2) = P((ccs)) = \frac{1}{8}
\end{align*}$$
> La tabla de la distribución conjunta de las tres variables
> ![[Pasted image 20260924214958.png]]
> 
> Para calcular $P(X_1 + X_3 = 2)$ y $P(X_1 + 1 ≤ X_3)$, basta con ver cuantos duplas de valores satisfacen estos eventos y buscar su probabilidad en la tabla de $p_{X_1,X_3}$. $$\begin{align*}
P(X_1 + X_3 = 2) &= P(X_1 = 0, X_3 = 2) + P(X_1 = 1, X_3 = 1) \\
&= p_{X_1, X_3}(0, 2) + p_{X_1, X_3}(1, 1) \\
&= 1/8 + 1/8 = 1/4
\end{align*}$$  $$\begin{align*} P(X_1 + 1 \le X_3) &= P(X_1 = 0, 1 \le X_3) + P(X_1 = 1, 2 \le X_3) \\
&= p_{X_1, X_3}(0, 1) + p_{X_1, X_3}(0, 2) + p_{X_1, X_3}(0, 3) \\
&+ p_{X_1, X_3}(1, 2) + p_{X_1, X_3}(1, 3) \\
&= 2/8 + 1/8 + 0 + 2/8 + 1/8 = 1/4
\end{align*}$$

## Independencia
Sea $(X_1, · · · , X_n)$ un vector aleatorio discreto sobre el espacio de probabilidad $(\Omega, A, P)$, se dice que las variables $X_i$ son independientes si
$$P[X_1 \in B_1, \dots, X_n \in B_n] = P(X_1 \in B_1) \times \dots \times P(X_n \in B_n)$$
Las variables aleatorias $X_1, . . . , X_n$ son independientes si y solo si la función de distribución conjunta del vector $(X_1, . . . , X_n)$ se escribe como producto de las funciones de distribución de cada una de las coordenadas del vector:
$$F(x_1, \dots, x_n) = F_{X_1}(x_1) \times \dots \times F_{X_n}(x_n)$$
Las variables aleatorias$X_1, . . . , X_n$  son independientes si y solo si la función de masa (probabilidad puntual) conjunta del vector $(X_1, . . . , X_n)$ se escribe como producto de las funciones de masa (probabilidad puntual) de cada una de las coordenadas del vector:
$$p(x_1, \dots, x_n) = p_{X_1}(x_1) \times \dots \times p_{X_n}(x_n)$$

### Lema- Independencia y Esperanza
Si X e Y son independientes entonces
$$E(XY) = E(X)E(Y)$$
Mas generalmente
$$E(h_1(X)h_2(Y)) = E(h_1(X))E(h_2(Y))$$

## Covarianza 
>[!info] Definición
>Dadas dos variables aleatorias X e Y definimos la covarianza entre ellas mediante la fórmula
$$Cov(X, Y) = E[(X - E(X))(Y - E(Y))]$$
Puede probarse usando las propiedades de la esperanza que
$$Cov(X, Y) = E[XY] - [E(X)E(Y)]$$
 
### Lema
Si X e Y son independientes entonces
$$Cov(X, Y) = 0$$
**Propiedades**
Sea $(X, Y)$ un vector aleatorio con densidad conjunta $f_{XY}$, entonces 
1. $Cov(X, X) = V(X)$ 
2. $Cov(X, Y) = E(XY) − E(X)E(Y)$
3. Si $X$ e $Y$ son independientes, entonces $Cov(X, Y) = 0$.
4. $Cov(aX + b, cY + d) = acCov(X, Y) \quad \forall a, b, c, d \in \mathbb{R}$ 
5. $Var(aX + bY) = a^2Var(X) + b^2Var(Y) + 2abCov(X, Y) \quad \forall a, b \in \mathbb{R}$
6. Si $X$ e $Y$ son independientes entonces $Var(aX + bV) = a^2Var(X) + b^2Var(Y)$



## Correlación 
>[!info] Definición
>Sean X e Y variables aleatorias con 0 < Var(X) < ∞, 0 < Var(Y) < ∞. Definimos el coeficiente de correlación lineal como
$$ \rho(X, Y) = \frac{Cov(X, Y)}{\sqrt{(Var(X))} \sqrt{Var(Y)}} $$

### Propiedades
1. El coeficiente de correlación lineal es independiente de posición y escala, pues
$$ \rho(X + a, Y + a) = \rho(X, Y) \qquad \rho(aX, aY) = \rho(X, Y), a > 0 $$
2. $-1 \le \rho(X, Y) \le 1$
3. $\rho(X, Y) = 1$ si y solamente si $P(Y = aX + b) = 1$, con $a > 0$.
$\rho(X, Y) = -1$ si y solamente si $P(Y = aX + b) = 1$, con $a < 0$.

![[Pasted image 20260924220315.png|538]]

# Vectores conjuntos
--- 
>[!info] Definición
>**Densidad**
>Recordemos que una variable aleatoria se dice continua con densidad o absolutamente continua cuando existe una función $F_X : \mathbb{R} \rightarrow \mathbb{R}$ no negativa que nos permite calcular la probabilidad de que $X$ este en $A$ de la siguiente forma
$$P(X \in A) = \int_A f_X(x) dx$$
>
>**Densidad Conjunta**
Sea $(X_1, . . . , X_n)$ un vector aleatorio continuo, es decir, una $n$-upla donde cada coordenada es una variable aleatoria continua con densidad sobre el espacio de probabilidad $(\Omega, A, P)$, se dice que la función $f : \mathbb{R}^n \rightarrow \mathbb{R}$ no negativa es una función densidad conjunta del vector $(X_1, . . . , X_n)$ si ocurre que
$$P[(X_1, \dots, X_n) \in A] = \int_{-\infty}^{\infty} \dots \int_{-\infty}^{\infty} f(x_1, \dots, x_n) I_A(x_1, \dots, x_n) dx_1 \dots dx_n$$
para todo $A \subset \mathbb{R} ^ n$
>
> **Distribución acumulada conjunta**
> Se define la función de distribución acumulada conjunta del vector $(X_1, · · · , X_n)$ como $$\begin{align*} F(x_1, \dots, x_n) &= P[(X_1 \leq x_1, \dots, X_n \leq x_n)] \\
&= \int_{-\infty}^{x_1} \dots \int_{-\infty}^{x_n} f(x_1, \dots, x_n) dx_1 \dots dx_n
\end{align*}$$

**Propiedades de la Distribución Conjunta**
La función densidad de probabilidad (densidad de masa) conjunta del vector $(X_1, · · · , X_n)$ cumple
1. $f$ no es única, pues cualquier función que no coincida con $f$ en un número finito o numerable de puntos también es una densidad conjunta para el vector aleatorio.
2. $f \geq 0$, es decir, es no negativa
3. $\int_{-\infty}^{\infty} \dots \int_{-\infty}^{\infty} f(x_1,⋯,x_n)dx_1⋯dx_n=1$
4. Si $F$ es derivable entonces $f = \frac{\partial ^ n F}{\partial_{x_1} \dots \partial_{x_n}}$ 

### Marginales 
Sean $( X_1 , · · · , X_n )$ un vector aleatorio continuo con función densidad conjunta $f$ , entonces las densidades marginales de las variables componentes del vector son
$$f_{X_j}(x_j) = \int_{-\infty}^{\infty} \cdots \int_{-\infty}^{\infty} f(x_1, \cdots, x_n) dx_1 \cdots, dx_{j-1}, dx_{j+1} \cdots dx_n$$
esto es, integro sobre todas las coordenadas salvo la coordenada $x_j$.

### Independencia 
>[!info] Definición
>Sean $(X_1, · · · , X_n)$ un vector aleatorio continuo con función densidad conjunta $f$ , decimos que las componentes del vector son independientes si
$$f(x_1, \cdots, x_n) = f_{X_1}(x_1) \cdots f_{X_n}(x_n)$$

>[!example] Ejemplo
Considere la siguiente función:
$$f(x, y) = \begin{cases} k(x + y^3) & \forall x, y \in [0, 1] \\ 0 & cc \end{cases}$$
>1. Determine el valor de la constante k para que f sea la función de densidad conjunta de un vector (X, Y)
>2. Encuentre las densidades marginales $f_X$ y $f_Y$
>3. Diga si las variables son independientes o no.
>4. Encuentre la esperanza y varianza de X e Y
>   
>   Para calcular la integral doble $\int_{0}^{1} \int_{0}^{1} (x + y3)dx dy$, vamos a dividir la integral en dos partes:
$$ \int_{0}^{1} \int_{0}^{1} (x + y^3) dx \, dy = \int_{0}^{1} \int_{0}^{1} x \, dx \, dy + \int_{0}^{1} \int_{0}^{1} y^3 \, dx \, dy $$
>
>- Calculando la primera parte
$$ \int_{0}^{1} \int_{0}^{1} x \, dx \, dy $$
Primero, calculamos la integral con respecto a $x$:
$$ \int_{0}^{1} x \, dx = \left[ \frac{x^2}{2} \right]_0^1 = \frac{1^2}{2} - 0 = \frac{1}{2} $$
Ahora, la integral con respecto a $y$:
$$ \int_{0}^{1} \frac{1}{2} \, dy = \frac{1}{2} \cdot [y]_0^1 = \frac{1}{2} \cdot (1 - 0) = \frac{1}{2} $$
> - Calculando la segunda parte
$$ \int_{0}^{1} \int_{0}^{1} y^3 \, dx \, dy $$
La integral con respecto a x es:
$$ \int_{0}^{1} y^3 \, dx = y^3 \cdot [x]_0^1 = y^3 \cdot (1 - 0) = y^3 $$
Ahora integremos con respecto a y:
$$ \int_{0}^{1} y^3 \, dy = \left[ \frac{y^4}{4} \right]_0^1 = \frac{1^4}{4} - 0 = \frac{1}{4} $$
>
>- Sumando las partes
Ahora sumamos los resultados de ambas partes
$$ \int_{0}^{1} \int_{0}^{1} (x + y^3) dx \, dy = \frac{1}{2} + \frac{1}{4} = \frac{2}{4} + \frac{1}{4} = \frac{3}{4} $$
Por lo tanto, el valor de la integral es $\frac{3}{4}$: y la densidad conjunta resulta
$$ f(x, y) = \begin{cases} \frac{4}{3}(x + y^2) & \forall x, y \in [0, 1] \\ 0 & cc \end{cases} $$
>- Marginales $f_X$ y $f_Y$  
Integrando la densidad f(x, y) en la variable y
$$f_X(x) = \frac{4}{3} \int_0^1 (x+y^3) \, dy = \frac{4}{3} \left[ \int_0^1 x \, dy + \int_0^1 y^3 \, dy \right] = \frac{4}{3} \left[ x + \frac{1}{4} \right] = \frac{4}{3} x + \frac{1}{3}$$
Integrando la densidad f(x, y) en la variable x
$$f_Y(y) = \frac{4}{3} \int_0^1 (x+y^3) \, dx = \frac{4}{3} \left[ \int_0^1 x \, dx + \int_0^1 y^3 \, dx \right] = \frac{4}{3} \left[ \frac{1}{2} + y^3 \right] = \frac{4}{3} y^3 + \frac{2}{3}$$
>- Independencia
$$f(x,y) = \begin{cases} \frac{4}{3}(x+y^3) & \forall x, y \in [0, 1] \\ 0 & cc \end{cases} \\ $$ $$f_X(x) = \begin{cases} \frac{4}{3}x + \frac{1}{3} & \forall x \in [0, 1] \\ 0 & cc \end{cases} \\ $$ $$f_Y(y) = \begin{cases} \frac{4}{3}y^3 + \frac{2}{3} & \forall y \in [0, 1] \\ 0 & cc \end{cases} \\ $$ $$ (\frac{4}{3}x + \frac{1}{3}) \times (\frac{4}{3}y^3 + \frac{2}{3}) \neq \frac{4}{3}(x+y^3) $$
por lo cual X e Y no son independientes
>- $E(X)$ y $E(Y)$   $$\begin{align*}
E(X) &= \int_0^1 x f_X(x) dx = \int_0^1 \frac{4}{3} x^2 dx + \int_0^1 \frac{1}{3} x dx \\
&= \frac{4}{3} \left[ \frac{x^3}{3} \right]_0^1 + \frac{1}{3} \left[ \frac{x^2}{2} \right]_0^1 \\
&= \frac{4}{3} \frac{1}{3} + \frac{1}{3} \frac{1}{2} = \frac{11}{18}
\end{align*}$$ $$\begin{align*}
E(Y) &= \int_0^1 y f_Y(y) dy = \int_0^1 \frac{4}{3} y^4 dy + \int_0^1 \frac{2}{3} y dy \\
&= \frac{4}{3} \left[ \frac{y^5}{5} \right]_0^1 + \frac{2}{3} \left[ \frac{y^2}{2} \right]_0^1 \\
&= \frac{4}{3} \frac{1}{5} + \frac{2}{3} \frac{1}{2} = \frac{3}{5}
\end{align*}$$


>[!example] Ejemplo 
>Considere la siguiente función:
$$f(x, y) = \begin{cases} \frac{12}{7}(x^2 + xy) & \forall x, y \in [0, 1] \\ 0 & cc \end{cases}$$
>1. Encuentre las densidades marginales $f_X$ y $f_Y$
>2. Calcule $P(X > Y)$
>   
>   - Marginales fX y fY
Integrando la densidad f(x, y) en la variable y
$$f_X(x) = \frac{12}{7} \int_0^1 (x^2 + xy) \, dy = \frac{12}{7} (x^2 + \frac{x}{2})$$
Integrando la densidad f(x, y) en la variable x
$$f_Y(y) = \frac{12}{7} \int_0^1 (x^2 + xy) \, dx = \frac{12}{7} (\frac{1}{3} + \frac{y}{2})$$
> -  P(X > Y)
Integrando la densidad $f(x, y)$ sobre el conjunto $\{(x, y)|0 \leq y \leq x \leq 1\}$
$$P(X > Y) = \frac{12}{7} \int_{0}^{1} \int_{0}^{x} (x^2 + xy) \, dy \, dx = \frac{9}{14}$$
$$\int_{0}^{x} (x^2 + xy) \, dy = x^2[y]_0^1 + x \left[\frac{y^2}{2}\right]_0^x = x^3 + \frac{x^3}{2} = \frac{3x^3}{2}$$
$$\int_{0}^{1} \frac{3x^3}{2} \, dx = \frac{3}{2} \int_{0}^{1} x^3 \, dx = \frac{3}{2} \left[\frac{x^4}{4}\right]_0^1 = \frac{3}{2} \frac{1}{4} = \frac{3}{8}$$
$$\frac{12}{7} \cdot \frac{3}{8} = \frac{36}{56} = \frac{9}{14}$$


## Esperanza de funciones de vectores contínuos

Proposición
Sea (X, Y) un vector aleatorio con densidad conjunta $f_{XY}$, entonces
$$E(h(X, Y)) = \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} h(x, y) f_{X,Y}(x, y) dx dy$$

>[!example] Ejemplo
> Sea $(X, Y)$ un vector aleatorio con densidad conjunta
$$f_{XY}(x, y) = e^{-y} \qquad 0 \le x \le y$$
Hallar la esperanza de $Z = XY$.
> 
> Aplicando el teorema anterior $$\begin{align*} E(XY) &= \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} xy f_{XY}(x, y) dx dy \\
&= \int_{0}^{\infty} y e^{-y} \left[ \int_{0}^{y} x dx \right] dy = \int_{0}^{\infty} y e^{-y} \left[ \frac{y^2}{2} \right] dy \\
&= \int_{0}^{\infty} \frac{y^3}{2} e^{-y} dy = \frac{\Gamma(4)}{2} \int_{0}^{\infty} \frac{1^4}{\Gamma(4)} y^{4-1} e^{-y} dy \\
&= \frac{\Gamma(4)}{2} = \frac{(4-1)!}{2} \\
&= 6/2 = 3
\end{align*}$$ usando el hecho de que
$$1 = \int_{0}^{\infty} \frac{\lambda^{\alpha}}{\Gamma(\alpha)} y^{\alpha-1} e^{-\lambda y} dy$$  para todo $\alpha$ y $\lambda$ positivos.

Propiedades
Sea $(X, Y)$ un vector aleatorio con densidad conjunta $f_{XY}$, entonces
1. $E(aX + bY) = aE(X) + bE(Y)$
2. Si $X$ e $Y$ son independientes entonces $E(XY) = E(X)E(Y)$


