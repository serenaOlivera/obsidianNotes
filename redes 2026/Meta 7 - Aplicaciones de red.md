Este bloque responde a ¿Cómo diseñamos aplicaciones que usan la red para ofrecer servicios reales?

## Protocolos
Un protocolo define tipos de mensajes con su estructura, define reglas de comunicación entre los procesos e información de estado.
Entonces tenemos aplicaciones que proporcionan servicios (llamadas aplicaciones de red) definidas mediante protocolos.

Antes de escribir un protocolo, necesitamos algo básico: identificar qué procesos participan en la aplicación, cómo se comunican entre sí y qué roles cumple cada uno. Esa organización previa - quién habla con quién, quién inicia, quién responde, quién almacena, quien distribuye- es lo que se conoce como arquitectura de la aplicación de red.

La arquitectura define la estructura general de la comunicación, y el protocolo especifica los detalles de cómo se lleva a cabo. Por eso, antes de diseñar un protocolo de aplicación, necesitamos entender las distintas arquitecturas posibles. EN general, una arquitectura describe qué procesos participan en la aplicación, qué roles cumplen y cómo se comunican entre sí. 

tipos de arquitecturas:
- arquitecturas cliente-servidor: un proceso actúa como cliente (inicia pedidos) y otro como servidor (atiende pedidos)
- arquitectura peer to peer: los procesos pueden cumplir ambos roles: a veces piden, a veces responden, y pueden compartir recursos entre sí sin un servidor central

[[Capa de Aplicación]]