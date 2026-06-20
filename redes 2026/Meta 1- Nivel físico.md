Este bloque se ocupa del nivel más fundamental: cómo viaja la información por un medio físico.
En este bloque estudiamos conceptos como "señales analógicas y digitales" y "representación de señales como funciones del tiempo" que son la base para entender codificación, modulación y multiplexado.

Este bloque responde a la pregunta ¿Cómo transformamos bits en algo que pueda viajar por un cable, por el aire o por la luz?

## Señales
- Señales analógicas y digitales:
  Representación de señales como funciones del tiempo
  ![[Pasted image 20260310164426.png]]
-  Ondas sinusoidales 
  $s(t) = A \ sin(2 \pi ft + \phi)$ , t número real.
  Propiedades de las ondas sinusoidales: frecuencia, amplitud, y fase
  ![[Pasted image 20260310165105.png]]


## Medios Físicos 
¿Por dónde viajan las señales? Por medios físicos, que se clasifican en:
- medios guiados:
  - cable de cobre: hay dos tipos de cable de cobre: cables de par trenzado de cobre y cable coaxial .
    ![[Pasted image 20260310165704.png]]
  - fibra óptica: 
    fibras multimodo: 50 micras (luz rebota)
    fibras monomodo: 8 a 10 micras  (luz línea recta)
- medios no guiados :
   como radios o microondas
- medios magnéticos:
  DVD's, Blu-ray, cintas magnéticas

Por ejemplo, la radio es una señal transportada en el espectro electromagnético, no se usan cables físicos, bidireccional. Efectos de la propagación en el entorno: reflexión, obstrucción por objetos, interferencia. 
Los **tipos de enlace de radio** son los siguientes:
- Microondas terrestres 
- LAN (ej: wifi)
- área amplia (ej cellular)
- satélite

## Degradación de una señal
El transmitir señales por medios físicos nos lleva al siguiente problema: la degradación de las señales. Estudiaremos las distintas formas en que esta puede ocurrir
- **Interferencia:**
  Se refiere a perturbaciones externas que afectan la transmisión de la señal, puede ser interferencia electromagnética (EMI) causada por motores, radios, microonda, etc. Es cuando señales de un canal se mezclan con otro.
  
  Su consecuencia es la degradación de la señal y posibles errores en la comunicación.
- **Ruido:**
  Es cualquier señal no deseada que se mezcla con la señal útil durante la transmisión, puede ser causado por interferencias electromagnéticas, variaciones térmicas o equipos eléctricos cercanos.
  
  Su efecto es la distorsión o pérdida de calidad en la comunicación, aumentando la probabilidad de errores en los datos.
  ![[Pasted image 20260310171500.png]]
- **Atenuación:tipos de enlace de radio**
  Es la pérdida de intensidad de la señal conforme viaja a través del medio de transmisión (por ejemplo: cable, fibra óptica). Las señales digitales sufren más de atenuación que las señales analógicas. A frecuencias mayores los pulsos se tornan más redondeados y pequeños.
  ![[Pasted image 20260310172231.png]]

## Codificación y decodificación de señales

El siguiente paso lógico es preguntarnos qué se hace para pasar de secuencias de bits a señales físicas y recíprocamente.

**Codificación**
Es el proceso de transformar la secuencia de bits (0 y 1) en una señal física que pueda transmitirse por el medio.  Se representan los bits en forma de pulsos eléctricos, variaciones de voltaje, ondas de luz o radiofrecuencia.
El objetivo: asegurar que la señal sea interpretada correctamente por el receptor y que se minimicen errores durante la transmisión.

**Decodificación:**
Es el proceso inverso: recibir la señal física y convertirla nuevamente en la secuencia original de bits (0 y 1).  El receptor aplica el mismo esquema de codificación que usó el transmisor para interpretar correctamente la señal.
Si la señal llega afectada por ruido, atenuación o interferencia, la decodificación puede ser más difícil y requerir técnicas adicionales de corrección de errores.

## Modulación 
Las computadoras procesan y generan información en forma de señales digitales (secuencias de ceros y unos). Sin embargo, no todos los medios físicos de transmisión - como el aire en comunicaciones inalámbricas o ciertos tipos de cableado- pueden transportar directamente esas señales digitales. 

*Modulación:* El proceso de modulación sirve para convertir la señal digital en una señal analógica, lo que permite que la información viaje de manera eficiente y confiable a través del medio que no permite señales digitales.
![[Pasted image 20260310174411.png]]

## Multiplexado 
Modulación nos permite adaptar una señal al medio. Pero en redes se exige algo más: aprovechar al máximo ese medio. Para resolver esto introducimos el mecanismo de multiplexado.

*Multiplexado:* Consiste en combinar dos o más señales independientes para transmitirlas simultáneamente a través de un mismo medio físico. En el receptor, se aplica el proceso inverso llamado demultiplexado, que separa las señales originales
![[Pasted image 20260310174659.png]]

* Si queremos mandar varias señales digitales por un mismo canal, usamos **multiplexado por división de tiempo:** varios emisores comparten un mismo medio físico enviando sus señales en distintos intervalos de tiempo, de modo que cada uno transmite solo en su propio turno.
  
  Esto es usado en redes telefónicas, redes troncales de fibra óptica, redes de celulares (GSM), redes de cable, en redes satelitales.
  ![[Pasted image 20260311183230.png]]
* Si queremos multiplexar varias señales analógicas, utilizamos **multiplexado por división de frecuencia (FDM):** varios emisores comparten un mismo medio físico asignando a cada uno una banda de frecuencias distinta, de modo que todas las señales viajan simultáneamente sin interferirse. 
  
  Esto es usado en cables de cobre y canales inalámbricos. En redes telefónicas, de celulares, de cable y satelitales.
  ![[Pasted image 20260311183206.png]]
