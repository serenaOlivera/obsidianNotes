>[!example] Ejemplo
Supongamos tener una población de tapitas de gaseosa. Y observamos su diámetro. Cada punto representa una tapita muestreada de la población. Un modelo paramétrico consiste en suponer la fórmula de $p(x)$  conocida, excepto por algunos parámetros. Por ejemplo, podemos suponer que es $N(\mu,\sigma^{2})$. ![[Pasted image 20261014194921.png]]

>[!info] Parámetros
En un modelo paramétrico, los parámetros son los valores que determinan la densidad de la población $p(x)$ de la variable aleatoria medida en el modelo. 
>- Denotaremos un parámetro general por la letra $\theta$ , y la densidad correspondiente por $p(x;\theta)$.
>- Si el modelo es discreto $p(x;\theta)$ denota la función de probabilidad puntual.
>- En este estadio de nuestro estudio, los parámetros son los únicos valores desconocidos de la densidad (función de frecuencia) marginal o conjunta.

>[!info] Estimación Puntual
>
Como no conocemos los parámetros de la población, el problema central es cómo estimarlos. Sea $X_{1},\dots,X_{n}$  una muestra aleatoria con distribución que depende de un parámetro $\theta$ , desconocido. Entonces se dice que la función de la muestra $$\hat{\theta}=h(X_{1},\dots,X_{n})$$ es un estimador puntual de $\theta$ si $\hat{\theta}$ es una variable aleatoria.

## Precisión y exactitud

![[Pasted image 20261014195439.png|603]]

## Diferencia entre Estimador Insesgado/No Consistente y Sesgado/Consistente
![[Pasted image 20261014201202.png|599]]

>[!info] Bondad de un estimador
>Un estimador es el método para calcular una estimación.
>Características deseables en estimadores son:
>1. Sesgo nulo
>2. . Consistencia
>3. Varianza mínima en la clase de los insesgados
>
Dentro de un conjunto de estimadores, podemos elegir como el mejor el que tenga el menor Error Cuadrático Medio(ECM). 
>- Si consideramos la clase de los insesgados, el ECM es la varianza del estimador.
En muchas ciencias, no se reporta solo el valor estimado en un experimento, sino que también se reporta el error estándar:
$$\hat{\theta}_{obs}\pm\sqrt{Var(\hat{\theta})}$$

## Observaciones

### ¿Por qué reportar la estimación y el error?

Porque se sabe que el valor estimado no es el valor real del parámetro, sino un valor cercano. Y alguna estimación de qué tan lejos está del verdadero valor es de interés.
![[Pasted image 20261014201423.png|498]]

Cuando uno elige un estimador insesgado de mínima varianza en la clase de los insesgados, está diciendo que el método para calcular la estimación es **exacto** y con **precisión máxima** en esa clase. Y el error estándar da idea de esa precisión. Pero no da confianza. Entonces una alternativa es calcular lo que llamaremos **INTERVALO DE CONFIANZA**.

>[!info] Estimación por intervalo
Sea $X_{1},\dots,X_{n}$ una muestra aleatoria con distribución que depende de un parámetro $\theta$, desconocido. Entonces, dado un valor $\alpha$, se dice que el par de variables aleatorias (funciones de la muestra) $$L(X_{1},\dots,X_{n})$$y$$R(X_{1},\dots,X_{n})$$ que cumplen $$P(L(X_{1},\dots,X_{n})\le\theta\le R(X_{1},\dots,X_{n}))=1-\alpha$$ es un estimador por intervalo de $\theta$  de nivel  $(1-\alpha)$.

>[!info] Definición
>Sea  $X_{1},\dots,X_{n}$ una muestra aleatoria con distribución que depende de un parámetro $\theta$ , desconocido. Sea $\hat{\theta}$ un estimador puntual de $\theta$  y $(L(X_1,\dots,X_n), R(X_1,\dots,X_n))$ un estimador por intervalo de $\theta$  de nivel $(1-\alpha)$  Dada una observación $x_{1},\dots,x_{n}$, el valor de 
>- $\theta$ estimado es $\hat{\theta}(x_{1},\dots,x_{n})$ 
>- y el intervalo estimado es: $[L(x_{1},\dots,x_{n}), R(x_{1},\dots,x_{n})]$

## Intuición de Intervalos de Confianza

1. **¿Qué es?**
   Un rango de valores posibles para un parámetro poblacional desconocido, calculado a partir de datos de una muestra.  No es un valor único, sino un margen de estimación que refleja incertidumbre.
2. **Nivel de Confianza: ¿Qué significa 95%?**
   Si repetimos el muestreo 100 veces, aproximadamente 95 de los 100 intervalos construidos contendrán el verdadero parámetro.
   -  **Compromiso de Precisión:** A mayor confianza requerida, el intervalo debe ser más ancho para asegurar la captura del valor real.
1. **Componentes**
   -  **Estimador Puntual:** El centro del intervalo (ej. la media muestral).
   -  **Margen de Error:** La distancia máxima a cada lado. Se expresa como:        $$\text{Est.} \pm \text{Margen}$$
## Observaciones

- Un Intervalo de Confianza (IC) para el parámetro $\theta$  permite tener una medida de la **CONFIABILIDAD** y **PRECISIÓN** de la estimación del parámetro.
- La **PRECISIÓN** de un IC tiene que ver con su longitud: cuanto menor sea su longitud, mayor es la precisión.   
- La **CONFIABILIDAD** es medida con el nivel de confianza del intervalo, que denotaremos con $(1-\alpha)$.
- Los niveles más usados son de 0.90, 0.95 y 0.99. Cuanto mayor sea el nivel de confianza, mayor es la chance de que el IC contenga al verdadero valor poblacional.
Luego es bueno pedirle a un IC que tenga una longitud pequeña y una alta confiabilidad de contener al parámetro poblacional.

>[!info] Método del pivote
Sea $X_{1},\dots,X_{n}$  una muestra aleatoria con distribución que depende de un parámetro $\theta$, desconocido. Sea $h(X_{1},\dots,X_{n})$  una variable aleatoria con distribución conocida que no depende de $\theta$. Sea $(1-\alpha)$ el nivel del intervalo a construir.
>1. Calcular los valores $a$ y $b$  tales que:$$P(a\le h(X_{1},\dots,X_{n})\le b)=1-\alpha$$  
>2. A partir de la expresión del evento $$(a\le h(X_{1},\dots,X_{n})\le b)$$ hay que tratar de obtener $$(L(X_{1},\dots,X_{n}),R(X_{1},\dots,X_{n}))$$ tales que:$$P(L(X_{1},\dots,X_{n})\le\theta\le R(X_{1},\dots,X_{n}))=1-\alpha$$ 
>3. Luego $[L(X_{1},\dots,X_{n}),R(X_{1},\dots,X_{n})]$ es un IC aleatorio para $\theta$ con un nivel de confianza $(1-\alpha)$.

>[!info] $h(X_1, \dots, X_n)$ es un Pivote para $\theta$ si: 
>1. **Distribución Conocida:** La distribución de probabilidad de $h(X_{1},\dots,X_{n})$ es conocida. 
>2. Independiente de $\theta$ : La distribución de $h(X_{1},\dots,X_{n})$ no depende del parámetro desconocido $\theta$.
>3.  **Límites Encontrables:** Es posible encontrar constantes $a$  y $b$ para fijar el nivel de confianza. 
>>[!tip] **Ecuación Fundamental:** 
>$$P(a < h(X_{1},\dots,X_{n}) < b) = 1-\alpha$$

>[!info] Construcción del Intervalo de Confianza
Obtención de los límites $L(X_1,\dots,X_n)$ y  $R(X_1,\dots,X_n)$ a partir del pivote 
>1. **Valores Conocidos:** A partir de $a$, y  $b$ y la función pivote $h(X_{1},\dots,X_{n})$.
>2. **Límites A Encontrar:** Hallar las funciones estadísticas $L(X_{1},\dots,X_{n})$ $R(X_{1},\dots,X_{n})$. 
>3. **Nivel de Confianza:** Asegurar que la probabilidad de despeje del parámetro $\theta$ sea $1-\alpha$.
>>[!tip] **Condición Equivalente Despejada:** 
>$$P(L(X_{1},\dots,X_{n})<\theta<R(X_{1},\dots,X_{n}))=1-\alpha$$

>[!info] ¿Es posible encontrar un pivote?
>4. **Muestra Aleatoria:** Sea $X_{1},\dots,X_{n}$ una muestra Normal con media $\mu$  desconocida y varianza $\sigma^{2}$ conocida. 
>5. **Distribución:** La variable estandarizada $\frac{\overline{X}-\mu}{\sigma/\sqrt{n}}$  tiene distribución normal estándar $N(0,1)$.
>6. **Propiedad Pivotal:** Su distribución es fija y no depende del parámetro desconocido $mu$.
> >[!tip] **Conclusión Pivotal**:
>$$Z=\frac{\overline{X}-\mu}{\sigma/\sqrt{n}}$$es un pivote para la media $\mu$ .   
 
# Distribuciones derivadas de la Normal
----

## Distribución Chi-Cuadrado

Recordemos a la distribución chi cuadrado con $k$ grados de libertad $\chi_{k}^{2}=\text{Gamma}(k/2, 1/2)$ tiene densidad: $$f_{X}(x)=\frac{(\frac{1}{2})^{\frac{k}{2}}}{\Gamma(\frac{k}{2})}x^{\frac{k}{2}-1}e^{-x/2}$$
![[Pasted image 20261014211701.png|565]]

## Distribución t de Student

>[!info] Definición
>Sean $X$ y $Z$ dos variables aleatorias independientes tales que $Z\sim N(0,1)$ y $X\sim\chi_{\nu}^{2}$. Entonces: $$T=\frac{Z}{\sqrt{X/\nu}}$$ se dice que tiene distribución t-student con $\nu$ grados de libertad. 
>**Densidad de la distribución t de Student:** $$f(t)=\frac{\Gamma(\frac{\nu+1}{2})}{\sqrt{\nu\pi}\Gamma(\nu/2)}\left(1+\frac{t^{2}}{\nu}\right)^{-(\nu+1)/2}, \quad \forall t\in\mathbb{R}$$

![[Pasted image 20261014211850.png|570]]


>[!info] Distribuciones derivadas de la normal
>Sea $X_{1},X_{2},\dots,X_{n}$  una m.a. con distribución $N(\mu,\sigma^{2})$, con $\mu$ y $\sigma^{2}$ desconocidas. Entonces: 
>1. $$Z=\sqrt{n}\frac{(\overline{X}-\mu)}{\sigma}$$ es una variable aleatoria normal estándar. 
>2. $$X=(n-1)\frac{S^{2}}{\sigma^{2}}=\frac{\sum_{i=1}^{n}(X_{i}-\overline{X})^{2}}{\sigma^{2}}$$ es una variable aleatoria con distribución $\chi^{2}$ con $n-1$ grados de libertad. 
>3. $X$ e $Z$ son independientes, por lo tanto:$$\frac{Z}{\sqrt{X/(n-1)}}=\sqrt{n}\frac{(\overline{X}-\mu)}{S}$$ tiene distribución t de Student con $n-1$ grados de libertad.


![[Pasted image 20261014212207.png|531]]

 **Notación**
Denotaremos con $z_{\alpha}$ al valor crítico, hallado en la tabla de la distribución Normal Estándar, tal que: $$\Phi(z_{\alpha})=1-\alpha$$
![[Pasted image 20261014212304.png|539]]
## Intervalos de confianza para la media

## CASO A
>[!info]  CASO A: muestra $N(\mu,\sigma^{2})$ con$\sigma>0$ conocida 
>Sea $X_{1},X_{2},\dots,X_{n}$ una m.a. con distribución$N(\mu,\sigma^{2})$, con $\sigma^{2}$ conocida. 
>**1ro)** Conocemos la distribución del promedio muestral $$\overline{X}$$y esta es $$\overline{X}\sim N\left(\mu,\frac{\sigma^{2}}{n}\right)$$ Al estandarizar $\overline{X}$ obtenemos una v.a. con distribución $N(0,1)$  $$h(X_{1},X_{2},\dots,X_{n};\theta)=\sqrt{n}\frac{(\overline{X}-\mu)}{\sigma}\sim N(0,1)$$
>
> **2do)** Fijado un nivel de confianza $(1-\alpha)$ , hay que buscar en la tabla normal estándar los valores de $a$ y $b$ tales que cumplan: $$P\left(a\le\frac{(\overline{X}-\mu)}{\sigma}\sqrt{n}\le b\right)=1-\alpha$$ Estos valores son $a=-z_{\alpha/2}$$y$$b=z_{\alpha/2}$.
> 
**3ro)** Despejando $\mu$ resulta: $$P\left(\overline{X}-z_{\alpha/2}\frac{\sigma}{\sqrt{n}}\le\mu\le\overline{X}+z_{\alpha/2}\frac{\sigma}{\sqrt{n}}\right)=1-\alpha$$
>
Por lo tanto un IC aleatorio de nivel $(1-\alpha)$ para$\theta=\mu$  es: $$\overline{X}\pm z_{\alpha/2}\frac{\sigma}{\sqrt{n}}$$  El intervalo observado resulta: $$\left[\overline{x}-z_{\frac{\alpha}{2}}\frac{\sigma}{\sqrt{n}}, \quad \overline{x}+z_{\frac{\alpha}{2}}\frac{\sigma}{\sqrt{n}}\right]$$

![[Pasted image 20261014212831.png|508]]
####  Áreas bajo la curva Normal para distintos niveles de confianza
![[Pasted image 20261014212857.png|536]]

## Observaciones
- Un Intervalo de Confianza (IC) para el parámetro $\theta$  es un par de variables aleatorias que permite tener una medida de la CONFIABILIDAD y PRECISIÓN de la estimación del parámetro.
- El pivote que usamos para calcular el intervalo anterior permite construir muchos intervalos asimétricos con la misma CONFIABILIDAD $(1-\alpha)$.
- El intervalo que dimos es simétrico y puede verse que tiene la mayor PRECISIÓN. Es decir, es el intervalo de menor longitud que puede crearse con ese pivote, para un $n$ y $\alpha$ fijo. La longitud de este intervalo es: $$L=2z_{\alpha/2}\frac{\sigma}{\sqrt{n}}$$
- Si se quiere obtener un intervalo de confianza de longitud a lo sumo $L$ y una confiabilidad $(1-\alpha)$ para  $\mu$, entonces hay que tomar:  $$n\ge\left(2z_{\alpha/2}\frac{\sigma}{L}\right)^{2}$$
- Dada una muestra observada, $x_{1},\dots,x_{n}$ podemos construir el intervalo observado: $$\overline{x}\pm z_{\alpha/2}\frac{\sigma}{\sqrt{n}}$$
- El método con el que lo construimos tiene un nivel de confianza de $(1-\alpha)$. La observación, no.
- **¿Qué podemos decir entonces?** Que si construimos 100 intervalos observados con muestras independientes, esperamos que no más de $\alpha\%$ de esas muestras no contengan el verdadero parámetro.
- Pero no podemos decir nada de una observación específica porque no tenemos conocimiento del verdadero parámetro.
![[Pasted image 20261014212945.png|474]]


>[!example] Ejemplo
>Supongamos que cuando se transmite una señal con valor $\mu$ desde la ubicación A, el valor recibido en la ubicación B está distribuido normalmente con media $\mu$ y varianza 4. Es decir, si se envía $\mu$ , entonces el valor recibido es $\mu+N$ donde $N$, que representa el ruido, es normal con media 0 y varianza 4. Para reducir el error, supongamos que se envía el mismo valor 9 veces. Si los valores sucesivos recibidos son: 5, 8.5, 12, 15, 7, 9, 7.5, 6.5, 10.5; construyamos un intervalo de confianza del 95 por ciento para $\mu$.
A partir de los valores de la muestra obtenemos: $$\overline{x}=\frac{81}{9}=9$$ El valor crítico de un nivel 95% para la distribución normal es $z_{0.025}=1.96$. Por lo cual el intervalo de confianza estimado para $\mu$ es: $$\left[\overline{x}-z_{\alpha/2}\frac{\sigma}{\sqrt{n}}, \quad \overline{x}+z_{\alpha/2}\frac{\sigma}{\sqrt{n}}\right] = \left[9-1.96\frac{2}{3}, \quad 9+1.96\frac{2}{3}\right] \approx [7.69, 10.31]$$
Por lo cual se suele reportar el intervalo observado $[7.69, 10.31]$ o el valor de la media muestral más o menos el error cometido $9\pm1.31$ y se dice que tenemos una confianza del 95% de que el verdadero mensaje se encuentra en este intervalo.
>
La interpretación de este resultado es delicada. Pueden ocurrir dos cosas:
>1. El intervalo observado $[7.69, 10.31]$ contiene el verdadero valor de $\mu$.
>2. Nuestra muestra es una de las pocas muestras para las cuales $\overline{x}$ no está a 1.31 puntos del valor de $\mu$. Solo un 5% de todas las muestras dan estos resultados incorrectos.
>Por lo tanto, no podemos asegurar que $\mu\in[7.69,10.31]$, pero tenemos un 95% de confianza de que lo contiene, pues llegamos a estos números por un procedimiento que falla solo el 5% de las veces.

![[Pasted image 20261014213642.png|572]]


>[!example] Ejemplo (Tamaño Muestral)
Por experiencia pasada se sabe que los pesos de los salmones criados en una incubadora comercial son normales con una media que varía de una temporada a otra, pero con una desviación estándar que se mantiene fija en 0.3 libras. Si queremos estar un 95 por ciento seguros de que nuestra estimación del peso medio de un salmón de la temporada actual es correcta dentro de $\pm0.1$ libras, ¿qué tamaño de muestra se necesita?
>
El valor crítico de un nivel 95% para la distribución normal es $z_{0.025}=1.96$. Observemos que el error en la estimación en un intervalo del 95% es: $$1.96\frac{\sigma}{\sqrt{n}}=\frac{0.588}{\sqrt{n}}$$  Por lo cual si se quiere tener una certeza del 95% de que esté a lo sumo a 0.1 de $\mu$ tiene que ocurrir que: $$\frac{0.588}{\sqrt{n}}\le0.1$$ Esto es: $$\sqrt{n}\ge5.88 \implies n\ge34.57$$. Esto es, un tamaño muestral de 35 o más grande va a ser suficiente.


## CASO B
>[!info] Caso B: muestra $N(\mu,\sigma^{2})$ con $\sigma>0$
desconocida Sea $X_{1},X_{2},\dots,X_{n}$ una m.a. con distribución $N(\mu,\sigma^{2})$, con $\sigma^{2}$ desconocida.
**1ro)** Dado que $\sigma^{2}$ es desconocido, ya no podemos basar nuestro intervalo en el hecho de que $\sqrt{n}(\overline{X}-\mu)/\sigma$ es una variable aleatoria normal estándar. Sin embargo, si: $$S^{2}=\frac{\sum_{i=1}^{n}(X_{i}-\overline{X})^{2}}{n-1}$$ es la varianza muestral, entonces:  $$h(X_{1},X_{2},\dots,X_{n};\mu)=\sqrt{n}\frac{(\overline{X}-\mu)}{S}\sim t_{n-1}$$ tiene distribución t con $n-1$ frados de libertad.
>
**2do)** Fijado un nivel de confianza $(1-\alpha)$, hay que buscar en la tabla de la distribución t de Student los valores de $a$ y $b$ tales que cumplan: $$P\left(a\le\frac{(\overline{X}-\mu)}{S}\sqrt{n}\le b\right)=1-\alpha$$ Estos valores son $a=-t_{\alpha/2,n-1}$ y $b=t_{\alpha/2,n-1}$. 
>
**3ro)** Despejando $\mu$ resulta: $$P\left(\overline{X}-t_{\alpha/2,n-1}\frac{S}{\sqrt{n}}\le\mu\le\overline{X}+t_{\alpha/2,n-1}\frac{S}{\sqrt{n}}\right)=1-\alpha$$
>
 Por lo tanto un IC aleatorio de nivel $(1-\alpha)$ para $\theta=\mu$ es: $$\overline{X}\pm t_{\alpha/2,n-1}\frac{S}{\sqrt{n}}$$

![[Pasted image 20261014214412.png]]

>[!example] Ejemplo con varianza desconocida
Supongamos que cuando se transmite una señal con valor $\mu$ desde la ubicación A, el valor recibido en la ubicación B está distribuido normalmente con media $\mu$y varianza **DESCONOCIDA**. Es decir, si se envía $\mu$, entonces el valor recibido es $\mu+N$ donde $N$, que representa el ruido, es normal con media 0 y varianza $\sigma^{2}$. Para reducir el error, supongamos que se envía el mismo valor 9 veces. Si los valores sucesivos recibidos son 5, 8.5, 12, 15, 7, 9, 7.5, 6.5, 10.5, construyamos un intervalo de confianza del 95 por ciento para $\mu$ usando la distribución t de Student.
>
A partir de los valores de la muestra obtenemos: $$\overline{x}=\frac{81}{9}=9$$ $$s^{2}=\frac{\sum_{i=1}^{n}x_{i}^{2}-9(\overline{x})^{2}}{8}=9.5 \implies s=3.082$$ El valor crítico de un nivel 95% para la distribución t con 8 grados de libertad es $t_{0.025,8}=2.306$. Por lo cual el intervalo de confianza estimado para $\mu$
es: $$\left[\overline{x}-t_{\alpha/2,n-1}\frac{s}{\sqrt{n}}, \quad \overline{x}+t_{\alpha/2,n-1}\frac{s}{\sqrt{n}}\right] =$$
$$\left[9-2.306\frac{3.082}{3}, \quad 9+2.306\frac{3.082}{3}\right] \approx [6.63, 11.37]$$ El cual es un intervalo más largo que el calculado conociendo la varianza y usando la distribución normal  $[7.69, 10.31]$. Aún si el $s$ estimado fuese el valor 2, el uso de la distribución t da un intervalo más grande que usando la normal: $$\left[9-2.306\frac{2}{3}, \quad 9+2.306\frac{2}{3}\right] = [7.46, 10.54]$$

