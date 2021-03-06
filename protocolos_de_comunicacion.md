# Protocolos de comunicación

Existen multitud de protocolos con propósitos muy similares o incluso idénticos. De hecho, a diferencia de lo que ocurre en el ámbito de las tecnologías de información en el entorno corporativo, donde organizaciones como IETF y la ISCO, a través de sus RFC, estandarizan la práctica totalidad de los protocolos, en el ámbito industrial cada fabricante define el suyo propio.

En este sentido cada fabricante establece normalmente un protocolo diferente, e incluso a veces un mismo fabricante define distintos protocolos según la serie del dispositivo y el propósito de la comunicación. Solo existen algunos intentos de estandarización como puede ser el protocolo Modbus adoptado, aparte del propietario actual de la marca Modicon (Schneider) en algunos de sus dispositivos, por fabricantes de dispositivos auxiliares como pudieran ser variadores de frecuencia, medidores de potencia o instrumentación, y también como segunda opción en muchos dispositivos de control como PLCs.

| MARCA | SERIE | PROTOCOLO |
| -- | -- | -- |
| SIEMENS | S7 1200/300/400 | S7 MESSAGING |
| OMRON | CJ/CS | FINS |
| HITACHI | H SERIES | HI-PROTOCOL |
| ROCKWELL | LOGIX | RS-LOGIX |
| B&R | X20 | INA |
| SCHNEIDER | TSX | UNITELWAY |
| HONEYWELL | UDC 3000 | UDC |
| MITSUBISHI | FX | FX PROTOCOL |

## Profibus
---

## Profinet
---
Profinet es el mismo protocolo de Profibus pero en el medio físico de Ethernet.

## Modbus
---
El protocolo basado en comunicación continua más extendido dentro de la industria es Modbus.

El protocolo Modbus se formuló a finales de los 70 por los creadores del primer PLC (Modicon) y
aún persiste, con unas pocas variaciones, en los PLCs de dicha marca (en la actualidad propiedad de Schneider Electric).

Al pasar el protocolo a libre uso, ha sido incorporado en infinidad de dispositivos (generalmente de un rango inferior a un PLC) como variadores de frecuencia, RTUs, IEDs y, como segunda opción, en algunos PLCs a través de módulos de comunicación (software y/o hardware adicional).

Las especificaciones del protocolo también soportan el encapsulamiento de las tramas serie dentro de tramas TCP, lo que permite como ya hemos comentado, la comunicación a través de
dispositivos Ethernet con dispositivos serie RS-232 o RS-485 con la pasarela adecuada.

Las especificaciones del protocolo son bastante sencillas, con unos pocos comandos de lectura y
escritura, y unos tipos de datos muy reducidos.

Los tipos de datos a leer y escribir se reducen a 4 tipos:
* Bobinas (salidas digitales)
* Contactos (bits de programa)
* Entradas analógicas (registros de 16 bits)
* Holding Registers (registros de programa de 16 bits).

En cuanto al tamaño de los datos (registros de 16 bits, enteros de 32 bits con signo o sin signo, floats) el protocolo no contempla distinciones, sino que la conversión se realiza a nivel de aplicación. Por ejemplo, la lectura de un registro de 32 bits con signo correspondería a la lectura de dos registros de 16 bits, y será el driver de comunicaciones quien compusiese el dato final a través de los datos proporcionados por el dispositivo.

## DNP3
---
Protocolo DNP3 por sus especiales características, que lo proyectan como un estándar de futuro, ya que incorpora prestaciones no incluidas en la mayoría de protocolos industriales (time stamp, eventos, autentificación, cifrado, etc.). Desarrollado originariamente por General Electric, hoy en día está promovido por el “DNP Users Group”, por lo que no está ligado a una marca en concreto, como la mayoría de protocolos.

Sus características principales son:
* **Orientado a eventos:** A diferencia de otros protocolos que la iniciativa de la comunicación parte del cliente de las comunicaciones, en los dispositivos con comunicación DNP3 es posible también definir que eventos deben comunicarse. De esta forma es posible optimizar
el volumen de comunicaciones.

* **Medidas con Time Stamp:** Todos los valores proporcionados por el driver incorporan el
tiempo de la medida. El driver es capaz de enviar series de datos para recomponer un
histórico de datos entre conexiones.

* **Unsolicited Messages:** Desde la programación del PLC es posible configurar qué
condiciones generarán el envío de un “Unsolicited Messages”, donde un evento es enviado
al cliente sin que éste pregunte por él.

* El protocolo incluye **mecanismos de identificación y autentificación** de forma que es
posible habilitar/denegar el acceso de determinados clientes a la información del dispositivo.


## OPC DA
---
Promovido por la OPC Foundation, se publicó el estándar OPC DA (Ole for Process Control), que
con una operatividad basada en los mecanismos de Windows OLE y COM, realizaba una
funcionalidad similar al enlace que realizaba DDE.

Hoy en día es el estándar principal para la comunicación entre SCADAs y drivers pese a que ya
están en uso especificaciones del protocolo mucho más avanzadas como es el caso de OPC UA.
Incluye funcionalidades adicionales como la búsqueda de elementos desde el editor de los SCADA
para facilitar la programación.

Además de que OPC DA solo está soportado por máquinas Windows, el protocolo OPC padece de
algunas deficiencias en cuanto al funcionamiento distribuido en diferentes ordenadores, debido
principalmente a los problemas de configuración de DCOM.

Estas deficiencias lo hacen especialmente difícil de configurar en algunos casos e impone barreras insalvables cuando los ordenadores se encuentran en diferentes dominios Windows. Igualmente, el protocolo OPC DA no dispone de mecanismos de seguridad para la protección del acceso a la información.

## Versiones Seguras de Protocolos de Comunicacion Industrial
### DNP3 SECURE
---
Algunos fabricantes de dispositivos que incluyen comunicación DNP3, incorporan al mismo
soluciones criptográficas que añaden autenticación y cifrado a través del denominado “DNP3
Secure".


### OPC UA
---
La OPC foundation, en una renovación tecnológica de OPC, publicó hace unos pocos años las
nuevas especificaciones denominadas OPC UA, que incluso incluyen la redefinición de las siglas
OPC por Open Platform Communications.

#### OPC DA vs. OPC UA

La redefinición del estándar OPC con las especificaciones UA incorpora al estándar una nueva
serie de características que podemos ver en Figura 29 comparadas con las especificaciones
anteriores. Uno de los principales avances en esta tecnología, y ya indicada en el nombre “Unified Arquitecture”, es que el estándar abandona la exclusividad del entorno Windows para abrirse a cualquier sistema. De esta forma los PLCs y DCSs que lo incorporen ya podrán comunicar de una forma nativa con el dispositivo monitorizador o historiador sin necesidad de ningún protocolo adicional.

#### Características

1. Nueva Arquitectura
La nueva arquitectura, que está basada en SOA (Service Oriented Architecture) y no en usuarios
de Windows, resuelve los problemas de configuración entre diferentes ordenadores.

2. Nuevas funcionalidades de seguridad
Las especificaciones OPC UA incluyen medias de seguridad hasta el momento inexistentes:
* Autentificación a nivel de aplicación: A partir de niveles de usuario y contraseña.
* Cifrado y autenticación de mensajes: Mediante el intercambio de certificados. 

3. Configuración de los Firewall más sencilla
Debido a la utilización de los puertos estándar http (TCP/80) y https (TCP/443), la configuración de los firewalls resulta más sencilla con la nueva tecnología.

4. Multiplataforma
OPC UA rompe la barrera Windows, y ya es posible implementarla en otras plataformas. Esto
permite que los dispositivos de control puedan incorporar directamente dicho protocolo.