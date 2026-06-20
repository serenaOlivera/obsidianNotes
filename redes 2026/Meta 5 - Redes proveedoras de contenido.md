En la práctica, enormes plataformas - servicios de video, redes sociales, buscadores, almacenamiento en la nube - generan volúmenes masivos de datos que deben llegar a usuarios distribuidos por todo el mundo. Y estas plataformas no siempre quieren depender de las reglas, los costos o las políticas de servicio de las redes de tránsito o regionales.

Para evitar esos costos y limitaciones, y para mejorar la calidad de entrega de su propio contenido, se vuelve necesaria una solución que permita que el contenido de estas plataformas llegue eficientemente a todas las redes de acceso.

Por eso se usan **Redes proveedoras de contenido (CDN)** (por ejemplo: Google, Microsoft, Apple, Meta). Las mismas son infraestructuras propias diseñadas para llevar su contenido lo más cerca posible  de los usuarios.

## Puntos de Presencia (PoPs)
Los POPs son nodos distribuidos que reducen latencia y evitan tránsito global. Son como servidores en distintos lugares del mundo, acercarlos a los usuarios y conectarlos a redes de acceso o regionales.

Un PoP está pensado para entregar contenido a usuarios cercanos, no para generarlo ni coordinarlo. Si solo existieran los PoPs, aparecen tres problemas inevitables:
- No pueden generar contenido: no tienen la infraestructura para producir, transcodificar o almacenar la versión maestra.
- No pueden mantenerlo actualizado: cada PoP tendría que obtener actualizaciones desde algún origen remoto.
- No pueden replicar contenido entre ellos sin pagar tránsito: si un PoP copia contenido desde otro PoP lejano, el tráfico cruza redes regionales o globales, generando altos costos y alta latencia.
Conclusión: Los PoPs  no pueden ser el origen del contenido ni coordinar su distribución global.

¿Qué necesita un PoP para cumplir su función?
- almacena contenido popular localmente para reducir latencia, usando una caché dentro de un PoP que guarda sólo lo más pedido.
- atiende a muchos usuarios a la vez a través de servidores de borde para atender usuarios y balanceadores de carga para repartir la carga
- se conecta a redes de acceso o regionales para entregar contenido,  usando equipos de redes, enlaces de alta capacidad y acuerdos de peering local con redes de acceso y regionales.
- recibir contenido actualizado desde algún centro de datos

![[Pasted image 20260316200403.png]]

## Centros de datos

Los centros de datos aparecen como la única forma viable de tener la versión maestra del contenido, procesarlo (transcodificarlo, empaquetarlo, indexarlo), mantenerlo actualizado, replicarlo hacia los PoPs, coordinar consistencia entre múltiples ubicaciones, balancear carga y manejar picos globales. 
Los PoPs quedan así aliviados: solo almacenan copias parciales y sirven contenido localmente.

![[Pasted image 20260316195100.png]]

Un centro de datos genérico es una instalación diseñada para alojar infraestructura de cómputo y almacenamiento que soporta aplicaciones, servicios y datos de todo tipo. Sus funciones típicas incluyen:
- Ejecutar aplicaciones empresariales
- alojar servicios en la nube
- Procesar cargas de cómputo (machine learning, análisis de datos)
- almacenar información corporativa
- soportar servicios internos de una organización 
- correr aplicaciones web, APIs, microservicios, etc.


Un centro de datos necesita:
- Generar contenido (procesarlo, transcodificarlo, empaquetarlo)
- Mantener la versión maestra de cada objeto
- Coordinar actualizaciones para que todos los PoPs tengan contenido consistente 
- Replicar contenido hacia los PoPs de forma eficiente
- Almacenar grandes volúmenes de datos 
- Balancear carga global entre regiones
- Tener alta disponibilidad (fallas, redundancia, energía, clima)
- Conectarse a una red propia que distribuya contenido sin pagar tránsito global.

>[!question] ¿Cómo se genera y procesa contenido a  gran escala?
Se usa capa de procesamiento pesado con: servidores de cómputo (para análisis de contenido, generación de metadatos, validación y empaquetado), clústers de procesamiento y sistemas de transcodificación.
La transcodificación es el proceso de convertir un contenido digital de un formato, resolución o tasa de bits a otro, para que pueda ser entregado de manera eficiente a distintos tipos de dispositivos, redes y condiciones de ancho de banda.

¿Cómo se mantiene una versión maestra del contenido?
	Se usa capa de almacenamiento maestro: sistemas de almacenamiento de objetos distribuidos en varios nodos, sistemas de archivos distribuidos, bases de datos.


>[!question] ¿Cómo se coordinan actualizaciones entre regiones?
Se usa capa de control y coordinación: 
>- Orquestación (qué tarea va a qué máquina)
>- Coordinación global (qué PoP recibe qué contenido)
>- Gestión de versiones
>- Consistencia (que los PoPs tengan lo que deben tener)
>- Políticas de distribución (popularidad, geografía)
>- Monitoreo y telemetría (estado de PoPs, carga, fallos)
>- Replicación (decidir cuándo y cómo mover contenido)

¿Cómo se asegura disponibilidad contínua?
- Redundancia energética
- climatización 
- Monitoreo
- failover regional
	  El failover regional es el mecanismo mediante el cual un servicio puede migrar automáticamente su operación desde una región que falla hacia otra región que sigue funcionando, sin que los usuarios pierdan acceso al contenido.
	  Este mecanismo garantiza continuidad incluso ante fallas grandes: cortes eléctricos, problemas climáticos, errores de software, congestión extrema o caídas de conectividad.
![[Pasted image 20260316202213.png]]
## Red privada global
Incluso con centros de datos, si cada réplica hacia los PoPs viaja por redes de tránsito global, volvemos al problema original: alto costo, alta latencia y dependencia de terceros.

Para llevar contenido desde los centros de datos a los PoPs sin pagar tránsito, usamos una red privada global propia del proveedor de contenido que conecte centros de datos y PoPs sin depender de tránsito global. Esto permitirá: enlaces troncales privados, rutas optimizadas para replicación masiva. 
Con esto el proveedor puede mover contenido desde centros de datos hacia la periferia (PoPs) sin pagar tránsito y con baja latencia.

