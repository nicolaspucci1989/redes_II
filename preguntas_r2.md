# X25 #

### Indique diferencias y semejanzas de las redes abiertas y cerradas
Las redes abiertas definen la interfaz UNI y NNI, define la interfaz usuario-red, las reglas de comunicación usuario-red, y especifican que sucede dentro de la red. las redes cerradas solo definen la interfaz NNI, sin especificar lo que sucede dentro de la red.

### ¿Qué modelos de la capa OSI comprende?
Comprende las capas 1, 2 y 3.  A nivel físico usa x.21. A nivel enlace usa LAP-B. A nivel de red X.25

### Indique las diferencias y semejanzas de los circuitos virtuales permanentes y conmutados
Los circuitos virtuales conmutados son conexiones temporales. Hay que establecer el circuito previamente a la comunicación, cuando no se necesita enviar más información se lo cierra. Implica un costo menor, ya que no está constantemente activo. Puede ser establecido según las necesidades de transferencia de información. En X.25 el usuario establece el enlace enviando un paquete a la red diciéndole que se quiere conectar con otro host.
En los circuitos virtuales permanentes no es necesario establecer la comunicación, ya que como su nombre lo indica, son permanentes, similar a las líneas arrendadas. Una vez finalizada la comunicación no se cierra el circuito, sino que permanece abierto es estado idle (inactivo). En X.25 la red administr los PVC, los canales lógicos se configuran de antemano. 

Ventajas de circuito virtuales vs datagramas.
* El encaminamiento en cada nodo se hace solo una vez para el grupo de paquetes. Por lo cual los paquetes llegan antes a su destino.
* Todos los paquetes llegan en el mismo orden que salieron, ya que siguen el mismo camino.
* En cada nodo se realiza una detección de errores, si se detecta un paquete erróneo se pide la retransmisión al nodo anterior.
Desventajas de circuitos virtuales vs datagramas.
* Con datagramas no hay que establecer conexión, es conveniente si se envían pocos paquetes.
* Son más flexibles. si un paquete encuentra un nodo congestionado en la red, los paquetes siguientes pueden tomar otro camino. Esto no es posible con circuitos virtuales.
* Si un nodo falla solo se pierde un paquete. En cambio con circuitos virtuales se pierden todos los paquetes.

### ¿Cómo realiza el usuario la conexión en circuitos virtuales conmutados?
Call setup, data transfer, idle y call termination.

En X.25.
* __Call Request__: paquete enviado a la red para indicarle que se desea comunicar con otra estación. 
Incoming call: paquete que le envia la red a la estación destino. Indica que otra estación desea comunicarse.
* __Call Connect__: paquete que la estación destino le envía a la red si acepta la comunicación con el origen.
* __Clear Request__: paquete enviado para finalizar la conexión.  Transporta la dirección.

### ¿Qué tipo de paquetes intercambia X25 (nivel de capa de red)?. Indique la utilidad de cada uno.
Paquetes de __conexión__. Sirven para establecer la comunicación entre dos estaciones.
Paquetes de __control__. Control de flujo (RNR)
Paquetes de __datos__.

### ¿Cómo se determinan las direcciones en X25?
Se representan en BCD. Puede ser par o impar, se rellena con ceros. En números decimales van de 2 a 14, concatenadas sin separador. Como las direcciones son de longitud variable, antes de esta se indica la longitud con 4 bits.

### ¿Tiene X.25 (o Fr?) relay control de flujo? ¿Qué logra de esa forma?
Cuando la red está congestionada se elimina la sesión, enviando un reset por el canal 0.

### ¿Qué entiende por ventana deslizante y cuáles son las diferencias con la ventana selectiva?
Ventana deslizante: A y B negocian el tamaño W de la ventan de transmisión. B puede aceptar W tramas y A puede enviar W tramas sin esperar un ACK. El ACK incluye el número de secuencia para tener un registro de las tramas enviadas. También es posible validar múltiples tramas con un solo ACK.
Ventana selectiva: las únicas tramas retransmitidas son aquellas que recibieron un ACK negativo. El transmisor debe mantener buffers más grandes y una lógica más compleja para poder reinsertar una trama en la secuencia correcta.

En x.25 existen dos ventanas, a nivel de enlace y otra a nivel de red.

------------------------------------------------------------------------------------------------------


# Frame relay #

### Si pensamos en Frame relay como la evolución de X25, ¿Qué progresos originaron tal evolución?
Los avances tecnológicos a nivel físico, medios mas confiables. Aplicaciones más complejas y más demandantes. El tráfico se vuelve más diverso. Necesidad de mayor ancho de banda, la cantidad de controles en X.25 generan un gran overhead. Estos controles ya no son necesarios debido a la existencia de medios mas confiables.

### ¿Tiene Frame relay control de flujo? ¿Qué logra de esa forma?
No tiene control de flujo, esto hace posible el envio de datos a ráfaga. Se evitan los controles, si es necesario se retransmite.

### ¿Qué entiende por congestión? ¿Cómo se realiza el control de congestión en Frame Relay? 
Control de congestión. Uno o varios de los nodos intermedios de la red recibe más paquetes de los que puede procesar. Los paquetes que no pueden ser procesados debido a que los buffers estan llenos son descartados.
En Frame Relay utilizan paquetes FECN y BECN prar el control de congestion. Avisan a los transmisores o a los receptores de la existencia de congestión en la red, pero estos no están obligados a tomar acción.
__FECN__. La red envía este paquete a los receptores en caso de congestión. Los receptores pueden ignorar este paquete. Si los receptores envían menos también lo harán los transmisores.
__BECN__. Enviado por la red a los transmisores. También es posible ignorar este paquete. 
En caso de que la red necesite descartar tramas, se descartan aquellas que tiene el bit DE encendido (Discard Eligibility)

### ¿Qué se entiende por calidad de servicio? ¿Cómo procede frame relay?
QoS. Servicio preferencial a las aplicaciones que los necesiten, asegurandoles un ancho de banda suficiente. Cierto tipo de tráfico necesita tratamiento preferencial. Frame Relay poss un QoS muy elemental.
Hay una ráfaga garantizada __CIR__ que es la velocidad mínima. Frame Relay garantiza un throughput mínimo. 
BC. Volumen de tráfico alcanzable transmitiendo a la velocidad del CIR.
Una vez alcanzado el __BC__ puedo seguir transmitiendo pero la red no lo garantiza. 
__BE__. Volumen de adicional. Se envían con el bit DE en 1. Son descartadas si es necesario.
Si sobrepaso el BE se descartan las tramas

### ¿Qué parámetros tiene en cuenta la calidad de servicio de frame relay?
CIR, BC, BE.

### ¿Cómo logra frame relay reducir el overhead?
La capa de enlace actúa como capa de red. Elimina una capa. Quito controles, no hay control de flujo, no hay confirmación. Si es necesario reenvío. El control se envía por un canal aparte.


------------------------------------------------------------------------------------------------------


# ATM #

### Describa ATM y su funcionalidad
Busca integrar distintos tipos de tráfico; voz, datos, video. telefonía. Es un método de transmisión asincrónica de señales en un solo canal realizando multiplexación de diversos servicios. Es orientado a la conexión. La información se segmenta en unidades llamadas celdas

### ¿Por qué ATM utiliza celdas tan pequeñas?
Con celdas pequeñas se logra una mejor distribución y se reduce el retardo, mejorando el rendimiento para la transmisión de voz y video. También se reduce el tiempo de procesamiento.

### ¿Cómo afecta al rendimiento de ATM el uso de celdas tan pequeñas?
ATM necesita un poder de __conmutación__ de miles de bytes. Las celdas pequeñas ayudan a esta conmutación, ya que son de rápido procesamiento. Para detectar una celda solo tengo que contar bits. 
Las celdas pequeñas reducen el __tiempo de transmisión__, logrando un mayor grado de multiplexación. Es más probable conseguir un retardo constante entre celdas del mismo tipo.
Favorece el tratamiento de __distintos tipos de tráfico__, otorga mayor variedad en los tipos de throughput que se consiguen. Multiplexar distintos tipos de tráfico es más fácil, porque cada tipo de tráfico tiene mayor oportunidad de entrar en la trama.
El uso de celdas pequeñas reduce el delay por encolamiento para celdas de alta prioridad, ya que espera menos si llega detrás de una celda de baja prioridad que ha ganado acceso a un recurso.
Pueden ser switcheadas más eficientemente, lo cual es importante para las altas tasas de transmisión de ATM. Con celdas de tamaño fijo es más fácil implementar los mecanismos de switcheo en hardware.

### Explique cuál es el concepto de canal lógico.
__VCC (Virtual Channel Connection)__ . Es la unidad básica de conmutación en una red ATM. Un VCC se establece entre dos usuarios de la red. También son usados para el intercambio usuario-red.
En ATM se agrega una segunda capa de procesamiento que trata con el concepto de camino virtual. Un __VPC (Virtual Path Connection)__ es un conjunto de VCCs que tienen los mismos extremos. Por lo tanto, todas las celdas que fluyen por todos los VCCs en un solo VPC se conmutan juntas.
Esto simplifica la arquitectura de la red, mejora el rendimiento y confiabilidad.

### ¿Cómo se sincronizan las celdas en ATM?
Para sincronizar celdas se utiliza el __HEC__ (Header Error Control). Transcurren varios estados.
* HUNT: Se busca la llegada de una celda verificando si coinciden los bits del campo HEC.
* PRESYNCH: Ya detectado el campo HEC se continúa su verificación. Una vez que se detectaron x celdas de manera consecutiva se considera sincronizado.
* SYNCH: La pérdida de sincronización se detecta si no se logra detectar el HEC x veces consecutivas.

### ¿Cuál es la capa física habitual de ATM?
Existen dos subcapas. PM (Physical Medium) proporciona las funciones de transferencia de bits. Depende del medio físico a adoptar . TC (Transmission Convergence) controla la sincronización de celdas. Extracción de información contenida en la capa física. Incluye la generación y chequeo del HEC. 

### ¿Cómo resuelve ATM el problema de tener celdas pequeñas en su relación con otras tecnologías?
Incorpora un nivel de adaptación, AAL (ATM Adaptation Layer). Se observa el mensaje para armar la celda. Tiene dos subniveles:
* SAR (Segmentation and Reassembly): segmentar y reensamblar la información recibida del subnivel de convergencia en celdas de 53 bytes.
* CS (Convergence Sublayer): se basa en los niveles de servicio. Realiza multiplexaje, detección de celdas perdidas y recuperación de tiempo. Prepara la información de los niveles altos para su conversión en celdas.

Hay cinco versiones de la capa de adaptación según el tráfico.
* AAL1, servicios CBR. De conexión y tráfico síncrono. Voz y vídeo sin comprimir.
* AAL2, servicios VBR. De conexión y tráfico síncrono. Voz y video comprimido.
* AAL3/4, servicios ABR. Para transferencias cortas pero de grandes ráfagas de datos.
* AAL5, servicios UBR. Para redes locales de alta velocidad.
¿Qué tipos de tráficos reconoce ATM? Describa características y parámetros asociados. 

------------------------------------------------------------------------------------------

# SDH #
http://robertoares.com.ar/wp-content/uploads/2010/06/Seccion-4.pdf

### ¿Qué diferencia hay entre PDH y SDH?
* PDH tiene una multiplexación asíncrona en una red plesíncrona, mientras que SDH tiene multiplexación síncrona en una red síncrona.
* En PDH la estructura de la trama es distinta en cada orden jerárquico. En SDH existe una única estructura de la trama.
* En PDH el intercalado es de bit, en SDH el intercalado es de bytes.
* SDH permite la multiplexación de canales sincrónicos y asincrónicos. Se conoce la posición de cada tributario dentro de la trama indicada mediante los punteros.
        
### ¿Cuántas tramas E1 se pueden transportar en STM-1 de SDH

### ¿Qué relación tuvo la vinculación entre 10 GIGAbit Ethernet y SDH con el crecimiento de ATM?

### ¿Qué medios de transmisión utiliza SDH o SONET?

### ¿Qué es un anillo óptico bidireccional?
Se divide la capacidad de la fibra en partes iguales, se envía tráfico principal y de protección. La transmisión entre nodos se realiza usando la ruta más corta y con tráfico normal. Cuando hay una falla en la red se puentean los tráficos.

Consiste en dos anillos, cada uno de ellos formado por __2 fibras__. Las señales de cada uno de ellos viajan en __sentido contrario__. Al mismo tiempo la capacidad de cada anillo se divide en __partes iguales__ para transportar el __tráfico__ de la red y la otra se reserva como __protección__ .Cada fibra divide su capacidad en partes iguales y la dedica a llevar a llevar tráfico principal y de protección. La transmisión entre 2 nodos se realiza siempre sobre la ruta más corta utilizando la parte de tráfico normal. La capacidad de protección puede utilizarse para transportar tráfico extra de baja prioridad.
Diferencie SONET de SDH


------------------------------------------------------------------------------------------------------


# BGP #

### ¿Por qué se dice que BGP tiene una fuerte componente estática en su ruteo?

### ¿Qué es un sistema autónomo?
Un sistema autónomo es un conjunto de redes bajo una o más administraciones que comparten una política común de ruteo externo
Cada Sistema Autónomo tiene un número asociado el cual es usado como un identificador para el Sistema Autónomo en el intercambio de información del ruteo externo. Los protocolos de ruteo externos tales como BGP son usados para intercambiar información de ruteo entre Sistemas Autónomos. El sistema autònomo debe garantizar que las rutas internas permanezcan persistentes y alcanzables.

### ¿Qué complicaciones añade la existencia de los sistemas autónomos al ruteo?
Con el objetivo de disminuir la complejidad de las tablas rutas globales, un nuevo __Número__ de Sistema Autónomo (ASN), debe ser asignado solamente en el caso en que una nueva política de ruteo es necesaria.
Compartir un mismo ASN entre un grupo de redes que no están bajo de la misma gestión va a requerir una __coordinación__ adicional entre los administradores de las redes y en algunos casos, va a requerir algún nivel de rediseño de la red.

### ¿Cómo es un SA Multihome non transit?
Un sistema autónomo conectado a dos ISP. No es un sistema de paso. No permite tráfico

Son organizaciones que utilizan los servicios de ISPs pero que no pasan ni rutas ni tráfico de un ISP a otro. Se los descarta si no se los reconoce. Los atributos opcionales reconocidos se propagan a los vecinos de acuerdo con su contenido. Son Multi_Exit_Disc (discrimina entre multiples salidas a un SA). Esto es útil cuando un cliente está conectado a dos redes de ISP y desea que los clientes de cada ISP utilicen sus propias conexiones para llegar a él. Los dos ISP utilizan
una política de no-tránsito, mientras que proporcionana una política de tránsito para todos sus clientes. Todos los clientes pueden comunicarse netre si, pero los ISP no pueden comunicarse entre sí a través del sistema multi home non transit.

### ¿Cómo es un SA Multihome transit?
Un SA conectado  a otros dos SA. Permite el tráfico.

### ¿Con BGP, cuantas tablas de enrutamiento se generan para manejar el Forwarding?
Dos, tabla BGP y tabla de ruteo IP.

### ¿Quién establece las políticas de ruteo y qué busca con ello?
El administrador de la red. Controlar el tráfico

### ¿Cómo se produce el intercambio de rutas en BGP?
Mediante protocolo eBGP. Con sesión TCP. Solo con trigger update. Se almacenan temporalmente y luego se envían.
Para intercambiar información de ruteo BGP entre sistemas autónomos las router deben anunciarse, explique el proceso en siguiente grafo
   
El tráfico fluye en dirección contraria a la información de ruteo.
De N1 a N16
* N16 se anuncia a N8
* N8 acepta N16
* N8 se anuncia a N1
* N1 acepta a N8

### ¿Por qué BGP no utiliza un protocolo de estado de enlace?
El camino más corto calculado por un protocolo de estado de enlace no necesariamente resulta en la mejor ruta.
Si se hace un broadcast de la base de datos a toda la red, se haría a toda la internet. A nivel de SA no resulta práctico, se superan los 200 nodos recomendados en OSPF.

### ¿Qué son los path vectors y cómo se obtiene?
Indica los sistemas autónomos que se recorrieron entre el origen y el destino. Cuando un router externo recibe una ruta detecta si se genero un loop.
A medida que se recorren los SAs, se agrega el número de SA al vector.
El SA que lo recibe chequea si su número en el vector. Si lo encuentra indica un loop, el paquete es descartado.


### ¿Cómo se evitan los loops típicas de los protocolos de vector distancia?
Con el Path Vector.

### ¿Indique y explique 2 atributos protocolos mandatorios de BGP?
Origen. Indica el origen de la ruta BGP. Puede ser IGP, EGP o desconocido.
AS_PATH. Secuencia de SA a través del cual se alcanza una red.

### ¿Qué es el next hop? Ejemplifique.
Es la dirección IP del próximo salto. Por lo general es la dirección ip del router BGP que lo envía. Puede ser la dirección IP de un tercer router para optimizar el ruteo. 
AS1------AS2-------AS3
AS1 indica su ip como próximo salto al router BGP del AS2

### ¿Cómo se descubren los vecinos BGP? ¿es necesaria una sesión?
No se descubren vecinos. Se configuran manualmente en abos extremos. Se necesita una sesión TCP. 

### ¿Cuáles son los criterios de selección de una ruta?
1. El menor código de origen.
2. Se prefieren caminos externos (eBGP) frente a caminos internos (iBGP).
3. Para caminos iBGP el camino a través del vecino IGP más cercano.
4. Para caminos eBGP el camino más estable, el de más antigüedad.
5. Se prefieren las rutas del router con el menor BGP ID.

### Explique cuáles son las funciones de los mensajes open, notification, update y keepalive.
Open. Usado para establecer vecindad e intercambio de parámetros básicos, incluyendo número de AS y valores de autenticación.
Update. Usado para intercambiar PAs (Path Attributes) y la longitud/prefijo asociado que usan esos atributos.
Keepalive. Se envía periódicamente para mantener la relación de vecindad. Si no se recibe un mensaje keepalive dentro del Hold timer negociado BGP baja la conección entre los vecinos.

### Explique el problema de continuidad BGP
Las rutas externas que se reciben por iBGP no se propagan, se necesitan conexiones lógicas entre routers BGP

### ¿Cuáles son las tareas de iBGP y eBGP?
iBGP. Uso interno. Administra la información dentro del SA
eBGP. Uso externo. Intercambio de rutas con otros SAs. Implementa políticas.
¿Para qué se usa el route reflector?
Se usa para evitar la malla completa en iBGP.


------------------------------------------------------------------------------------------------------


# Multicast #

### En qué consiste la tecnología multicast y qué problemas resuelve.
Es una tecnología de conservación de ancho de banda. Reduce el tráfico distribuyendo la información hacia los hosts que lo necesitan evitando hacer broadcast.

### ¿Qué es IGMP y que función cumple?
Protocolo de manejo de grupos multicast, agregar quitar hosts de un grupo multicast. Registrar hosts dentro de un grupo multicast.
IGMP V3 soporta aplicaciones que señalan explícitamente las fuentes desde donde el receptor desea recibir tráfico, podría explicar los tipos de modos existentes.
INCLUDE MODE.  En este modo, el receptor anuncia su pertenencia a un grupo de hosts y provee una lista de direcciones IP (lista INCLUDE) de la cual desea recibir tráfico.
EXCLUDE MODE. En este modo, el receptor anuncia su pertenenci a un grupo de hosts y provee una lista de direcciones IP (lista EXCLUDE) de la cual no desea recibir tráfico. Esto indica que el hosts quiere recibir tráfico solo de otras fuentes.

### Explique que es un árbol compartido y como se resuelve.
A diferencia de los árboles fuente que tienen su raíz en la fuente, los árboles compartidos usan una sola raíz común compartida ubicada en algún punto de la red. Esta raíz compartida es llamada rendezvous point (RP).
Los emisores envían el tráfico a la fuente compartida. Luego el tráfico es reenviada hacia abajo del árbol compartido desde el RP en dirección a los receptores.
Los árboles compartidos tienen la ventaja de requerir una cantidad mínima del estado de cada router. Esto disminuye los requerimientos de memoria de una red que solo permite árboles compartidos. La desventaja de los árboles compartidos es que bajo ciertas circunstancias los caminos entre la fuente y los receptores puede no ser óptimo, lo cual puede introducir alguna latencia en la entrega de los paquetes. 
¿Qué es el Protocol Independent Multicast (PIM)?
Protocolo de ruteo independiente que puede aprovechar cualquier protocolo de ruteo unicast usado para llenar las tablas de ruteo unicast. PIM usa esta información de ruteo unicast para llevar a cabo la función de reenvío multicast. Aunque PIM sea llamado un protocolo de ruteo multicast, usa las tablas de ruteo unicast para llevar a cabo la función de chequeo RPF en lugar de construir una tabla de ruteo multicast completamente independiente. A diferencia de otros protocolos de ruteo, PIM no envía y recibe actualizaciones entre routers.


------------------------------------------------------------------------------------------------------


# TCP #

### ¿Qué características tiene TCP
Orientado a la coneccion. Confiable. Ordenado. Usa byte streams. Con ventana. Control de flujo y congestión.

### ¿Por qué TCP es byte stream?
Porque los acks se realizan conforme a los bytes recibidos 

### ¿Cuál es la estructura del segmento TCP?
Son 5 palabras de 32 bits como mínimo, luego siguen los datos. Los primeros 32 bits contienen los puertos destino y origen. Los siguentes 32 indican el número de secuencia. Sigue el ack con 32 bits. Header length indica el tamaño del header. Un campo con valor 0 reservado para uso futuro. Flags o bits de control. Tamaño de la ventana. Checksum de 16 bits. Puntero de urgencia.  Sigu un campo de opciones de longitud variable, al final se encuentran los datos.

### ¿Qué diferencia hay entre el número de secuencia de TCP y el de X25?
En x25 se enumera el segmento. En tcp se enumera al byte.

### ¿Para qué sirven los bits de flag?
Referencian distintos estados de la coneccion, o tratamiento especial del paquete. Ej. Reducción de la ventana de congestión. Finalización de datos del emisor. Tratamiento urgente de un paquete. PSH para enviar la información directo a la aplicación.

### ¿Qué representa el campo de ventana? ¿Por qué aparece en el segmento TCP?
Indica la cantidad de bytes que se puede transmitir antes de esperar el ack.

### ¿Cómo se puede realizar control de flujo utilizando el campo de ventana?
Se indica cuántos bytes se pueden enviar. Con una ventana más pequeña estoy indicando que deseo recibir menos bytes. Con una ventana de 0 

### ¿Cómo se establece y finaliza la conexión en TCP?
El host A envía un mensaje syn con el isn y el tamaño de su ventana. Host B envia un syn con su isn, su ventana el ack = syn +1. Host A responde con un ack.
Host A envía un mensaje fin. Host B responde con fin ack. Host B envía un fin. Host A responde con fin ack.
Inicialización:
1- Host A que requiere la conexión envía un segmento SYN especificando el número de puerto al cual desea conectarse, y el número de secuencia inicial ISN.
2- Host B responde con su propio segmento SYN que contiene su ISN. También reconoce el SYN del host A enviando un ACK con el ISN del host A más uno.
3- Host A reconoce el SYN del host B enviando un ACK con el ISN del host B más uno.
Finalización:
1- Host A inicializa la finalización enviando un FIN al host B, cerrando el flujo de datos en esa dirección.
2- Host B envía un ACK del número de secuencia recibido más uno. 
3- Host B cierra su conexión enviando un FIN.
4- Host A reconoce el segmento enviando un ACK con el número de secuencia recibido más uno

### ¿Qué representa la opción de tamaño de segmento máximo (MSS)? ¿En qué momento se establece? ¿Para qué se definió?
Indica la máxima longitud del segmento. Generalmente vinculado al MTU. Se define durante el inicio de la coneccion TCP.

### ¿Cómo actúa la ventana de recepción de TCP en el emisor? Explique vinculando ack, tamaño de ventana y tamaño del buffer.
La ventana de recepción indica cuántos bytes puedo enviar. El receptor indica en su ventana el tamaño del buffer disponible. Si el receptor incrementa su ventana también lo hace el emisor. El ack cual fue el último byte recibido y así determinar a partir de que byte continuar la transmisión. 

### ¿Qué hace TCP cuando recibe un segmento? ¿puede retardar el ack? ¿qué efecto logra? 
Al recibir un segmento, puede ser que se esperen demás segmentos o enviar un ack por el segmento recibido dependiendo del tamaño de la ventana, 
El retardar el ack evito que el emisor siga transmitiendo. Asi puedo evitar el síndrome de silly window.
Mejoro la performance.                 

### ¿Qué ocurre cuando se pierde algún segmento TCP? Recree un escenario explicando lo que ocurre en los buffers de recepción y emisión.
Pasado el tiempo de retransmisión hay que retransmitir el segmento a partir del último ack.
Host A envía un segmento de 50 bytes con un número de secuencia de 100, mantiene en un buffer los bytes transmitidos . El host B mantiene un buffer de recepción y envía un ack con un número de 151 indicando que recibió los 50 bytes y está preparado para recibir más bytes a partir del 151. El host A elimina los bytes que han sido recibidos y  envía un segmento con un número de secuencia de 151. Transcurrido el timer el host A supone que se ha perdido el segmento y retransmite los 50 bytes almacenados en el buffer

### ¿Qué diferencia existe entre el timer RTO de TCP y el de nivel de enlace? ¿Cómo se determina el tiempo de espera para la retransmisión?
A nivel de enlace el rto es consistente. En cambio a nivel tcp donde tengo una red cambiante el rto puede variar constantemente, debido a los cambios en la red. 
El tiempo de retransmisión se vuelve a estimar luego de una retransmisión exitosa.

### ¿Qué es el ack ambiguo? ¿Cómo se resuelve?
Se envía un paquete, pasado el rto se retransmite, llega el ack. A qué segmento pertenece al ack, al transmitido o a su retransmisión. Como resuelvo el RTT.
No actualizar el rtt con paquetes retransmitidos. Usar transmisiones exitosas, usar el time stamp.

### ¿Cómo controla TCP la congestión?
Hay que evitar la retransmisión cuando ocurre la congestión. Uso slow start y delay multiplicativo.
Ausencia de congestión, la ventana de congestión es igual a la ventana de recepción. Si reduzco la ventana de congestión se reduce el tráfico. Se asume que la pérdida de datagramas se debe a la congestión. Si hay congestión reducir la ventana de congestión por la mitad. Luego de un período de congestión, incrementar linealmente la ventana de congestión luego de recibir el ACK. 

### ¿Cuál es la desventaja de controlar la congestión desde los extremos como lo hace TCP?
No es confiable. La pérdida de paquetes no solo se debe a la congestión.

### ¿Qué hace TCP para definir el tamaño de la ventana que se publica en el encabezado del segmento?
Utiliza la ventana de recepción y la ventana de congestión.

### ¿Cómo detecta TCP que hay congestión? 
Las retransmisiones indican congestión Los extremos se ocupan de detectar la congestión. 
Basado en la red. Los nodos intermedios de la red se ocupan del tratamiento de la congestión
