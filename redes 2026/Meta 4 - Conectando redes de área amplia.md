Conectar LANs es útil dentro de una red de área amplia. Las redes de área amplia son manejadas por organizaciones que se ocupan de proveer servicios de red. Pero hace falta escalar aún más la perspectiva interconectando redes de área amplia. 
Este bloque responde a: ¿Cómo se organiza una red como la internet a nivel global para que cualquier red pueda comunicarse con cualquier otra?

## Redes de acceso
Una sola empresa no puede prestar el servicio de conectar todas las LAN del planeta, porque la inversión en infraestructura sería prohibitiva, y porque hay políticas de permiso diferentes en los distintos países.

Para poder interconectar todas las LAN entre sí hacen falta varias redes de acceso interconectadas. A esto se le llama interred. La internet es una interred
![[Pasted image 20260314184845.png]]

## Redes globales de tránsito
Las redes de acceso nos permiten conectar hogares, empresas o instituciones a un proveedor de servicio de red. Pero una vez que el tráfico sale de esa red de acceso, necesita recorrer distancias mucho mayores y atravesar múltiples dominios. En ese punto, la infraestructura de acceso ya no alcanza: no está diseñada para mover grandes volúmenes de tráfico entre ciudades, países o continentes.
¿Cómo resolvemos esto? Conectamos cada red de acceso a una red global de tránsito, y las redes globales de tránsito se conectan entre sí.
![[Pasted image 20260314185458.png]]

Las redes globales de tránsito pueden competir entre sí. Una red global de tránsito contiene enrutadores de alta velocidad interconectados usando enlaces de fibra óptica de alta velocidad. Cada red de acceso o global de tránsito es manejada independientemente.

## Redes regionales
Las redes globales de tránsito forman la infraestructura que permite mover tráfico entre países y continentes, conectando grandes proveedores y sosteniendo la escala planetaria de redes como la internet. Sin embargo, las redes globales no siempre llegan a todas las regiones para conectar directamente sus redes de acceso. Surge entonces la necesidad de una solución intermedia que conecte las redes de acceso dentro de una región y las vincule con la infraestructura global.

Se usa una red regional en la región que se va a conectar con alguna red global de tránsito:
- Redes de acceso pagan a redes regionales
- Redes regionales pagan a redes globales de tránsito
- Redes regionales pueden conectarse entre sí.
-![[Pasted image 20260314190516.png]]