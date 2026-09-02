## Probabilidad Condicional
****
>[!example] Ejemplo 1
>Un urna contiene tres bolas rojas y una bola azul. Dos bolas son seleccionadas sin reposición y su color anotado. 
>1. ¿Cuál es el espacio muestral del experimento?
>2. ¿Es equiprobable?
>3. ¿Cuál es la probabilidad de que ambas bolas seleccionadas sean rojas?
>   
>  Sean $R_1$ y $R_2$ eventos tales que la bola roja se selecciona en la primera extracción y en la segunda extracción respectivamente. 
>  De la regla de la multiplicación $$P(R_1 \cap R_2) = P(R_1) P(R_2 | R_1)$$
>  La probabilidad de $R_1$ es claramente 3/4, pues tengo cuatro bolas, tres de ellas rojas.
>  
>  Ahora, si una de las bolas rojas fue removida en la primera extracción, quedan dos bolas rojas y una azul en la urna, por lo cual cambio mi experimento y la probabilidad de $R_2/R_1$, es decir sacar una bola roja dado que cambió mi experimento es ahora 2/3.
>  Por lo cual $$P(R_1 \cap R_2) = \frac{3}{4} * \frac{2}{3} = \frac{1}{2}$$


## Independencia
**** 
>[!example] Ejemplo 2
> Consideremos el lanzamiento de dos monedas; estamos interesados en estudiar la independencia de los sucesos A = "obtener cara en el primer lanzamiento" = {C+, CC},y B = "obtener un resultado diferente en los dos lanzamientos" = {C+,+C}.
> 
> Se tiene que: $$\mathcal{P}(A)=\frac{2}{4} = \frac{1}{2} \ \ \ \ \ \mathcal{P}(B) = \frac{2}{4} = \frac{1}{2},$$
> $$A \cap B = \{C+\}, \ \ \ \ \ \mathcal{P}(A \cap B) = \frac{1}{4}$$
> por lo que se cumple que $$\mathcal{P}(A\cap B) = \mathcal{P}(A) * \mathcal{P}(B)$$ 
> y los sucesos son independientes.

### Regla de la Probabilidad Total
En ocasiones, $\Omega$ se puede partir en varios sucesos de probabilidad positiva $B_1, B_2,...,B_r$, incompatibles entre sí, es decir, en:
1. Sucesos exhaustivos: $\Omega = \cup_{i=1}^{r} B_i$
2. Sucesos excluyentes: $B_i  \cap B_j = \emptyset$ para todo $i \neq j$
![[Pasted image 20260823192516.png]]

La probabilidad de un suceso A puede calcularse a partir de las probabilidades de A condicionadas por los diferentes sucesos $B_1, B_2,...,B_r$
$$\mathcal{P}(A) = \mathcal{P}(A\cap B_1) + \mathcal{P}(A \cap B_2) + ...+ \mathcal{P}(A \cap B_r) = $$
$$=\mathcal{P}(A|B_2)\mathcal{P}(B_1) + \mathcal{P}(A|B_2)\mathcal{P}(B_2)+...\mathcal{P}(A|B_r)\mathcal{P}(B_r) \implies $$
$$\mathcal{P}(A) = \sum_{i=1}^{r} \mathcal{P}(A|B_i)\mathcal{P}(B_i)$$
>[!Example] Ejemplo 3 
>En una población, el 40% son hombres, de los cuales el 80% son aficionados al fútbol, mientras que sólo el 20% de las mujeres, son aficionadas al fútbol. ¿Cuál es la probabilidad de que una persona elegida al azar sea aficionada al fútbol?
>
>El espacio muestral puede dividirse en los ucesos exhaustivos y excluyentes $B_1 = \text{"hombres, y"} B_2 = \text{"mujeres"}$, cuyas probabilidades respectivas son $\mathcal{P} (B_1)= 0,40 \text{y} mathcal{P}(B_2)= 0,60$
>![[Pasted image 20260823192833.png]]
>¿Porqué? Porque el enunciado dice que hay 40% hombres, por lo cual hay un 60% de mujeres. Si el modelo considera la probabilidad de Laplace, $\mathcal{P}(B_1)=0,4 y \mathcal{P}(B_2)=0,60$
>
>Además, A="Ser aficionado al fútbol" cumple que $\mathcal{P}(A|B_1)=0,80$ y $\mathcal{P}(A|B_2)=0,20$. POr tanto, utilizando la regla de la probabilidad total: $$$\mathcal{P}(A)=\mathcal{P}(A|B_1)\mathcal{P}(B_1) + \mathcal{P}(A|B_2)\mathcal{P}(B_2)= 0,8 * 0,4 + 0,2 * 0,6 = 0,44$$

### Regla de Bayes
En el mismo caso de un espacio muestral particionado en sucesos exhaustivos y excluyentes $B_1,...,B_r$, reescribimos la probabilidad de $B_j$ condicionada por el suceso A, utilizando la regla de la probabilidad total: $$\mathcal{P}(B_j |A) = \frac{\mathcal{P}(B_j \cap A)}{\mathcal{P}(A)}= \frac{\mathcal{P}(B_j \cap A)}{\sum_{i=1}^r \mathcal{P} (A|B_i)\mathcal{P}(B_i)}$$
Muy útil para obtener una probabilidad condicionada $\mathcal{P}(B_i|A)$ a partir de las probabilidades condicionadas en el sentido contrario $\mathcal{P}(A|B_j), \ \ \ j=1,...,r$


>[!example] Ejemplo 4: 
>En una urna hay 3 bolas azules, 4 blancas y 7 rojas. Se extrae una bola. Si es blanca no se repone, si es roja se vuelve a poner en la urna, y si es azul se devuelve a la urna y se agrega una azul más. A continuación se extrae otra bola.
>1. Hallar la probabilidad de sacar una bola azul en la segunda extracción.
>2. Si la segunda bola es azul, que color tuvo mayor probabilidad de haber salido en la primera extracción?
>3. Hallar la probabilidad de no sacar azul en ninguna de las dos extracciones.
>
>1- En este caso es más obvio aún que conviene resolver las preguntas usando información condicional en vez de pasar por el espacio muestral. Sea $B_,R_1,A_1$ los eventos se seleccionó en la primera extracción una bola blanca, una bola roja, una bola azul, respectivamente. Sean $B_2,R_2,A_2$ los eventos se seleccionó en la segunda extracción una bola blanca, una roja y una azul, respectivamente. Entones,
>$$P(A_2) = P(B_1 \cap A_2) + P(R_1 \cap A_2) + P(A_1 \cap A_2)$$ $$= P(A_2 |B_1)P(B_1)+ P(A_2|R_1)P(R_1) + P(A_2|A_1)P(A_1)$$ $$= \frac{3}{13}\frac{4}{14} + \frac{3}{14}\frac{7}{14} +\frac{4}{15}\frac{3}{14} = \frac{3}{14}[\frac{4}{13}+\frac{7}{14}+\frac{4}{15}] = 0,2302198$$
>
>2- $$P(B_1|A_2) = \frac{P(A_2|B_1)P(B_1)}{P(A_2)} = \frac{\frac{3}{13}\frac{4}{14}}{0,2302198} = 0,2863963$$
>$$P(R_1|A_2) = \frac{P(A_2|R_1)P(R_1)}{P(A_2)} = \frac{\frac{3}{14}\frac{7}{14}}{0,2302198} = 0,4653939$$
>$$P(A_1|A_2) = \frac{P(A_2|A_1)P(A_1)}{P(A_2)} = \frac{\frac{4}{15}\frac{3}{14}}{0,2302198} = 0,2482102$$
>
>3- $$P(A_1^{c} \cap A_2^{c}) = 1- P(A_1)-P(A_2)+P(A_1\cap A_2) = 1 - \frac{3}{14} - 0,2302198 + \frac{4}{15}\frac{3}{14}$$ $$ = 0,5554945+0,0571429 = 0,6126374$$



## Variable Aleatoria 
****
Si en un experimento aleatorio, a cada suceso elemental del espacio $(\Omega, \mathcal{P})$ le asignamos un valor numérico obtenemos una variable que "hereda" de $\Omega$ la probabilidad $\mathcal{P}$, y que denominamos **variable aleatoria**
![[Pasted image 20260823200014.png]]

La probablidad P de que X tome un valor concreto a, P(X = a), es la probabilidad que corresponde a la unión de los sucesos aleatorios elementales a los ue hemos asignado ese valor a.

>[!example] Ejemplo 5:
>Experimento aleatorio: "lanzar un dado".
>- V.a más natural X: asignar a cada cara del dado su valor numérico $\implies X$ toma seis valores, del 1 al 6, con probabilidad $$P(X = a) = \frac{1}{6}, a= 1,...,6$$
>-  v.a. no tan natural Y: asignar el valor 1 a las caras que son múltiplos de tres y el valor 0 a las que no lo son, 
> Y =  1, con probabilidad $p = \frac{1}{3}$
>     0, con probabilidad $p = \frac{2}{3}$  

>[!example] Ejemplo 6
>Vamos a realizar un experimento aleatorio que consiste en "seleccionar una persona al azar". Para cada persona observamos el número de hermanos que tiene y su peso.
>
>Podemos usar las v.a's:
>- X para el número de hermanos, cuyos valores serán números enteros a partir de cero,
>- Y para el peso; con rango de valores todos los posibles entre los límites naturales; entre dos valores posibles de Y se podrían obtener infinitos valores intermedios (si utilizáramos aparatos con suficiente precisión).
>
>Estos infinitos valores en el rango de la variables es lo que diferencia a las variables contínuas (Y) de las discretas (X).


Una **variable aleatoria** X es una función $C: \Omega \rightarrow \mathbb{R}$, que a cada elemento del espacio muestral le hace corresponder un número real.
- El conjunto de valores reales que tienen asociado algún elemento del espacio muestral se denomina **rango** de la v.a.: $$\Omega_{X} ={x \in \mathbb{R}: \exists s \in \Omega, X(s) = x}$$
- Si $\Omega_X$ es un conjunto finito o numerable, entonces la variable aleatoria se denomina **discreta**.
- En caso de que $\Omega_X$ sea un intervalo, finito o infinito, entonces la variable aleatoria se denomina **continua**. 
![[Pasted image 20260823201728.png]]

Ejemplo: 
- Cualitativa Nominal -> $X(\Omega) = \{\text{banana, manzana, pera, uva}\}$
- Cualitativa Ordinal -> $X(\Omega) = \{\text{chico, mediano, grande, extra grande}\}$
- Cuantitativa Discreta -> $X(\Omega) = \{1,2,3,4,5,6\}$
- Cuantitativa contínua -> $X(\Omega) = [0,1]$
![[Pasted image 20260823202104.png]]

¿Cómo asignamos probabilidad P a los valores del rango de una v.a.? (¿Cómo hereda la variable X la función de probabilidad $\mathcal{P}$ del espacio $\Omega$?)
Dado $A \subset \mathbb{R}$, la probabilidad de A viene dada por $$P(A) = P(X \in A) = \mathcal{P}(s \in \Omega: X(s) \in A)$$
La función de $\left\{\begin{array}{l}\text{masa (v.a. discreta)}\\\text{densidad (v.a. continua)} \end{array} \right.$ caracteriza P (inducida por $\mathcal{P}$)
- ¿Qué significa? que conocida la función de masa/ densidad de X podemos calcular la probabilidad de cualquier subconjunto $A \subset \mathbb{R}$
- ¿Por qué usarlas? porque son más fáciles de calcular y de manipular

>[!info] Función de masa (v.a. discreta)
>Es una función que representa la probabilidad de que X tome cada uno de los posibles valores discretos $x_i, \ \ \ i=1,...,n,...:$ $$p: \mathbb{R} \rightarrow [0,1]$$ $$x_i \rightarrow p(x_i) = P(X=x_i) = \mathcal{P}(s \in \Omega: X(s) = x_i)$$
>
>**Propiedades**
>1. $0 \leq p(x) \leq 1, \forall x \in \mathbb{R}$
>2. $\sum_{i} p(x_i) = 1$
>3. Dado $A \subset \mathbb{R}, \ P(X \in A) = \sum_{x_i \in A} p(x_i)$


>[!info] Función de distribución
>Otra función F que caracteriza la función de probabilidad P de una v.a. X: $$F(x) = P(-\infty,x] = P(s \in \Omega: X(s) \leq x), \ \ \ \  \forall x \in \mathbb{R}$$
>
>Propiedades:
>1. $\lim_{x \to -\infty} F(x) = 0$
>2. $\lim_{x \to \infty} F(x) = 1$
>3. $x_1 < x_2 \implies F(x_1) \leq F(x_2)$ (monótona no decreciente)
>4. $F(x^{+}) = \lim_{h \to 0^{+}} F(x+h) = F(x)$ (contínua por la derecha)
>
>Como consecuencia
>- $P(a,b] = P(-\infty, b] - P(-\infty, a] = F(b)-F(a)$
>  
>  **Función de distribución de una v.a. discreta**
>$$F(x) = \sum_{x_i \leq x} P(X = x_i) = \sum_{x_i \leq x} p(x_i)$$
>- es una función  contínua a trozos (función en escalera)
>  La diferencia, es que en este conjunto $\sum_{x_i \leq x} P(X = x_i)$ pueden ser muchos puntos de Omega , cuando lo traduje, esas probabilidades pueden ser distintas.

![[Pasted image 20260823204327.png|473]]
 

