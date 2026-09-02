do look at this simulator, https://hcmus-hqhuy.github.io/LEGv8-Simulator/
esta cool.

Hoy presentan p.2
objetivo: hacer andar el procesadodr completo, debemos verificar que todas las entradas y salidas estén bien.
Integrar todo el micro, compilamos.
maldito memdump.

no seteemos as top el archivo procesador_arm
tenemos que situarnos en proccesor_core

nota para ej. 1 (practico 2):
la salida de memoria 16 daba 0 antes porque no se tocaba, en este micro, como esta modelada la memoria, si no se toca queda en X. En nuestro codigo, la memoria 16 debería quedar en 0.


