Link al repositorio: https://github.com/MarioGonzalo/CasoPracticoFinal.git

# CasoPracticoFinal

## 1. Diseño y Modelado de la Arquitectura de Comunicación

### Análisis de Modelos

**Modelo OSI (Open Systems Interconnection)**

| Capa OSI              | Función Principal                                     |
|------------------------|------------------------------------------------------|
| 7. Aplicación          | Interfaz con el usuario final, servicios de red.     |
| 6. Presentación        | Formato de datos, cifrado, compresión.              |
| 5. Sesión              | Control de diálogo entre aplicaciones.              |
| 4. Transporte          | Control de flujo, corrección de errores.            |
| 3. Red                 | Direccionamiento lógico, enrutamiento.              |
| 2. Enlace de Datos     | Control de acceso al medio, detección de errores.   |
| 1. Física              | Transmisión de bits por el medio físico.            |

**Modelo TCP/IP**

| Capa TCP/IP       | Correlación con OSI | Función                                  |
|-------------------|----------------------|-------------------------------------------|
| Aplicación         | Capas 5-7            | Servicios como HTTP, FTP, DNS, etc.       |
| Transporte         | Capa 4               | TCP/UDP para entrega de datos.            |
| Internet           | Capa 3               | IP, ICMP, enrutamiento.                   |
| Acceso a Red       | Capas 1-2            | Ethernet, WiFi, acceso físico/lógico.     |

---

### Integración de Modelos para los Servicios

#### A. Servicios Gubernamentales

- **Aplicación:** HTTPS, REST/SOAP, correo (SMTP), DNS con DNSSEC.
- **Transporte:** TCP para comunicaciones fiables.
- **Red:** IP (DHCP), OSPF/BGP para enrutamiento.
- **Enlace/Física:** Ethernet y fibra óptica en oficinas.

#### B. Seguridad Pública y Emergencias

- **Aplicación:** RTSP (videovigilancia), VoIP (SIP/RTP), alertas ciudadanas.
- **Transporte:** UDP para baja latencia, TCP para datos críticos.
- **Red:** Multicasting, MPLS para calidad de servicio (QoS).
- **Seguridad:** VPN IPSec, firewall, autenticación 802.1X.

#### C. Transporte y Monitoreo Ambiental (IoT)

- **Aplicación:** MQTT, CoAP.
- **Transporte:** UDP para sensores, TCP cuando se requiere fiabilidad.
- **Red:** IPv6, RPL (IoT mesh networks).
- **Enlace/Física:** LoRaWAN, ZigBee, WiFi 6, 5G.

#### D. Servicios Multimedia para el Ciudadano

- **Aplicación:** HTTP Live Streaming, portales web (HTML5).
- **Transporte:** TCP (streaming adaptativo), UDP (tiempo real).
- **Red:** CDN local, QoS.
- **Seguridad:** TLS, DNSSEC, WAF (firewall de aplicaciones).

### Diseño lógico y segmentación

![Image](https://github.com/user-attachments/assets/b3e38dbf-42e9-4b1b-a3b1-89aba3432091)

Esta captura representa la composición de la red de la ciudad que es un spanning tree con dos switches auxiliares pra más seguridad, y siendo el switch de arriba a la derecha el asignado a seguridad y el de arriba a la izquierda el asignado a transporte, también tiene un firewall para mayor seguridad que se conecta a la zona desmilitarizada y al exterior.

![image](https://github.com/user-attachments/assets/997d4d71-1f89-439e-bb93-ba9c45bef608)

Esta parte est la del edificio gubernamental, tiene varias plantas conectadas a un switch principal con vlans asignadas para mayor privacidad, al igual que el resto de edificios este tiene un firewall con zona desmilitarizada para protegerse de posibles vulnerabilidades.


## 2. Capa Física – Cálculos y Selección de Tecnologías

### Cálculo de la Capacidad de los Enlaces:

Para calcular la capacidad necesaria en los enlaces cableados e inalámbricos del campus emplearemos la fórmula de Shannon:

$$ C = B \times log_2(1+SNR)$$

Donde:


- C: Capacidad máxima del canal (bps)

- B: Ancho de banda del canal (Hz)

- SNR: Relación señal a ruido (unitaria, no en decibelios)

Para convertir SNR en dB a forma unitaria emplearemos la fórmula:

$$𝑆𝑁𝑅_{lineal} = 10 𝑙𝑜𝑔_{10}(𝑆𝑁𝑅) = 10^{\frac{SNR}{10}} [dB]$$

Por ejemplo,  para un enlace inalámbrico crítico: B = 300MHz y SNR = 20 dB

### Paso 1: Convertir SNR de dB a escala lineal

Se usa la fórmula:

$ \text{SNR}_{\text{lineal}} = 10^{\frac{SNR_{dB}}{10}} $

$ \text{SNR}_{\text{lineal}} = 10^{\frac{20}{10}} = 10^2 = 100 $

---

### Paso 2: Aplicar la fórmula de Shannon

$ C = 300 \times 10^6 \times \log_2(1 + 100) $

$ C = 300 \times 10^6 \times \log_2(101) $

---

### Paso 3: Calcular logaritmo en base 2

$ \log_2(101) \approx \frac{\log_{10}(101)}{\log_{10}(2)} \approx \frac{2.004}{0.3010} \approx 6.6582 $

---

### Paso 4: Calcular capacidad

$ C = 300 \times 10^6 \times 6.6582 \approx 1.997 \times 10^9 \, \text{bps} $


### Selección de Técnicas de Modulación:

| Modulación  | Bits por Símbolo | Eficiencia Espectral | Robustez ante Interferencias | Complejidad Computacional |
|-------------|------------------|-----------------------|------------------------------|----------------------------|
| **BPSK**     | 1                | Baja                  | Muy Alta                     | Baja                       |
| **QPSK**     | 2                | Moderada              | Alta                         | Moderada                   |
| **8-PSK**    | 3                | Alta                  | Media                        | Alta                       |
| **16-QAM**   | 4                | Alta                  | Media-Baja                   | Alta                       |
| **64-QAM**   | 6                | Muy Alta              | Baja                         | Muy Alta                   |

---

#### Modulación para Enlaces **Cableados**

- Para los enlaces cableados emplearemos 16-QAM o 64-QAM ya que los enlaces cableados ofrecen una baja atenuación e inteferencia por lo que no se necesita demasiada robustez y se puede priorizar la eficiencia sin temer mucho a las interferencias.


---

#### Modulación para Enlaces **Inalámbricos**

- Para los enlaces inalámbricos emplearemos QPSK o 16-QAM en los mejores casos ya que los canales inalámbricos, a lo contrario que los enlaces cableados, tiene más ruido e interferencias por lo que es necesario sacrificar un poco de eficiencia por robustez ante interferencias.


## 3. Capa de Red – Direccionamiento, Subneteo y Enrutamiento

### Diseño del Esquema de Direccionamiento IP:

### Segmentación por Funciones

| Segmento                  | Subred asignada     | Descripción                                      |
|---------------------------|---------------------|--------------------------------------------------|
| Zona Gubernamental        | 192.168.0.0/24       | Oficinas administrativas, portales internos      |
| Seguridad Pública         | 192.168.10.0/24       | Cámaras, patrullas, centros de monitoreo         |
| Transporte e IoT Ambiental| 192.168.20.0/24       | Semáforos, sensores, estaciones meteorológicas    |


---

### Cálculos por Segmento (/24 = 255.255.255.0)

#### 1. Zona Gubernamental – 192.168.0.0/24
- **Dirección de red:** 192.168.0.0  
- **Dirección de broadcast:** 192.168.0.255  
- **Rango de hosts válidos:** 192.168.0.1 – 192.168.0.254

#### 2. Seguridad Pública – 192.168.10.0/24
- **Dirección de red:** 192.168.10.0  
- **Dirección de broadcast:** 192.168.10.255  
- **Rango de hosts válidos:** 192.168.10.1 – 192.168.10.254

#### 3. Transporte y Monitoreo Ambiental – 192.168.20.0/24
- **Dirección de red:** 192.168.20.0  
- **Dirección de broadcast:** 192.168.20.255  
- **Rango de hosts válidos:** 192.168.20.1 – 192.168.20.254


---

### Justificación del Diseño

- El uso de subredes /24 permite una administración simple y eficiente.
- Cada segmento puede ser gestionado de forma aislada, lo que mejora la seguridad y facilita el control de tráfico.



### Enrutamiento y Rutas Óptimas:

Para emplear el algoritmo de Dijkstra para calcular rutas óptimas entre los diferentes egmentos asumiremos que cada segmento es un nodo con un peso en un grafo ponderado siendo:

- **A:** Centro de Control Principal  
- **B:** Zona de Seguridad Pública  
- **C:** Centro de Emergencias  
- **D:** Oficina Administrativa  
- **E:** Nodo de Monitoreo Ambiental

Con estos pesos:

| Enlace | Costo |
|--------|-------|
| A - B  | 2     |
| A - C  | 5     |
| B - C  | 1     |
| B - D  | 4     |
| C - E  | 2     |
| D - E  | 3     |

El algoritmo de Dijkstra calcula la ruta más eficiente desde un nodo origen hacia los demás, acumulando los costos más bajos posibles a medida que explora el grafo. No se limita al primer salto más barato, sino que evalúa todas las rutas posibles y actualiza los caminos si encuentra uno de menor costo acumulado.

En cuanto al algoritmo de inundación este consiste en que en vez de distribuir el paquete de un nodo origen a un nodo destino buscando y empleando la ruta más óptima este distribuye el paquete por todos los nodos posibles exceptuando por el que se mandó. Para que no haya bucles o errores similares a cada paquete se le atribuye un número limitados de saltos o, dicho de otra manera, de transiciones entre nodos.

En caso de que falle algún enlace o nodo se empeará este método para aseegurar la entrega de mensajes críticos.

## 4. Capa de Transporte – Selección de Protocolos y Cálculo del Tamaño de Ventana

### Selección de Protocolos de Transporte:

#### Protocolo TCP (Transmission Control Protocol)

El protocolo TCP se empleará para procesos que requieran una alta fiabilidad ya que es mucho más seguro que el UDP porque se asgura de mantener una conexión con el receptor.

**Aplicaciones típicas:**
- Transferencia de archivos (FTP/SFTP)
- Acceso y actualización de bases de datos gubernamentales
- Servicios administrativos web seguros
- Comunicaciones entre servidores críticos

**Justificación:**
- TCP utiliza mecanismos como el **control de congestión**, **retransmisión automática**, **número de secuencia**, y **ventanas deslizantes** para garantizar la entrega confiable.
- Se prioriza la integridad sobre la velocidad.

---

#### ⚡ Protocolo UDP (User Datagram Protocol)

Se usará en servicios a tiempo real ya que UDP es notablemente más rápido que el TCP siendo perfecto para estos tipos de procesos.

**Aplicaciones típicas:**
- Streaming en tiempo real de cámaras de vigilancia
- Alertas de tráfico o emergencias (broadcast/multicast)
- Comunicaciones IoT de baja latencia (CoAP sobre UDP)

**Justificación:**
- UDP no espera confirmaciones ni realiza retransmisiones, lo que **minimiza la latencia**.
- Permite el envío de datagramas livianos sin sobrecarga adicional, ideal para aplicaciones con tolerancia a pérdidas.

### Cálculo del Tamaño de Ventana en TCP:

### Cálculo del Tamaño de Ventana en TCP

El **tamaño de la ventana TCP** determina cuántos datos pueden estar en tránsito sin haber sido confirmados (ACK). Este parámetro es clave para aprovechar el ancho de banda disponible.

#### Fórmula general:

$ \text{Ventana óptima} = \text{Ancho de banda} \times \text{RTT} $

---

### Ejemplo práctico

Supuestos:

- Ancho de banda = 10 Mbps (megabits por segundo)
- RTT (Round Trip Time) = 50 ms
- MSS (Maximum Segment Size) = 1,500 bytes

---

### Paso 1: Convertir unidades

**Ancho de banda:**

$ 10 \, \text{Mbps} = 10 \times 10^6 \, \text{bps} = 10{,}000{,}000 \, \text{bits/segundo} $

**RTT:**

$ 50 \, \text{ms} = 50 \div 1000 = 0.05 \, \text{segundos} $

---

### Paso 2: Calcular tamaño de ventana en bits

$ \text{Ventana óptima} = 10{,}000{,}000 \, \text{bps} \times 0.05 \, \text{s} = 500{,}000 \, \text{bits} $

---

### Paso 3: Convertir a bytes

$ 500{,}000 \div 8 = 62{,}500 \, \text{bytes} $

---

### Paso 4: Calcular número de segmentos MSS

$ \frac{62{,}500 \, \text{bytes}}{1{,}500 \, \text{bytes/segmento}} \approx 41.67 $

**Resultado:** Aproximadamente 41 segmentos MSS pueden estar en tránsito simultáneamente sin recibir confirmaciones.

---

### Conclusión

- Con un ancho de banda de 10 Mbps y un RTT de 50 ms, el tamaño óptimo de ventana es de 62,500 bytes.
- Esto permite tener hasta 41 segmentos MSS en tránsito de forma eficiente.
- Si se necesita transmitir más datos en paralelo, puede habilitarse **TCP Window Scaling** para superar el límite de 65,535 bytes de ventana estándar.

## 5. Capa de Aplicación – Servicios, Multiplexación y Multimedia

### Implementación de Servicios y Resolución de Nombres:

### Implementación de Servicios y Resolución de Nombres

La red de la ciudad inteligente contará con servidores dedicados para DNS, FTP/SFTP y HTTP/HTTPS, esenciales para ofrecer servicios internos, acceso ciudadano y comunicación segura.

---

### 1. Configuración de Servidores

#### a. Servidor DNS

- Se encargará de traducir nombres de dominio internos a direcciones IP.
- Utiliza zonas locales para gestionar dispositivos, servicios y recursos internos.
- Debe estar configurado con registros A, AAAA, CNAME y PTR según sea necesario.
- Debe operar en un entorno seguro, aislado de la resolución DNS externa, si es posible.

#### b. Servidor FTP/SFTP

- Se utilizará para transferencia de archivos entre departamentos y sistemas.
- SFTP será el protocolo preferido por seguridad (cifrado de datos y autenticación).
- La configuración debe restringir accesos no autorizados y registrar todas las transferencias.

#### c. Servidor HTTP/HTTPS

- Proveerá acceso a portales web, paneles informativos y contenido multimedia.
- Se requerirá HTTPS para garantizar la confidencialidad y autenticidad de la comunicación.
- El servidor debe soportar múltiples sitios y asegurar su disponibilidad.

---

### 2. Proceso de Resolución de Nombres

- Cuando un cliente requiere acceder a un servicio por nombre, realiza una consulta DNS.
- El servidor DNS local responde con la dirección IP correspondiente al nombre solicitado.
- Una vez obtenida la IP, el cliente establece la conexión con el servicio deseado.

---

### 3. Multiplexación de Solicitudes

Los servidores deben ser capaces de atender múltiples solicitudes simultáneas mediante:

#### a. Multiplexación por Puerto

- Cada servicio opera en un puerto específico, permitiendo coexistencia en una misma máquina.

#### b. Multiplexación por Hilo o Proceso

- Los servidores gestionan múltiples conexiones simultáneas mediante procesos o hilos independientes.

#### c. Multiplexación por Dominio

- Un servidor web puede manejar múltiples sitios o servicios diferenciados por nombre de dominio.


### Servicios Multimedia

Dependiendo de qué se quiera retransmitir y sus necesidades se emplearán dos procesos:

##### 1. UDP Streaming (Low Latency)

- Utilizado para transmisiones de **baja latencia**, como vigilancia en tiempo real.
- Se emplea junto con protocolos como **RTP (Real-Time Protocol)** sobre UDP.
- No hay retransmisión de paquetes perdidos, lo cual reduce el retardo.
- Recomendado para:
  - Cámaras de vigilancia
  - Alertas visuales en tiempo real

##### 2. Adaptive HTTP Streaming – DASH (Dynamic Adaptive Streaming over HTTP)

- Divide el contenido en pequeños segmentos (2–10 segundos), disponibles en diferentes calidades.
- El cliente selecciona dinámicamente la calidad más adecuada según las condiciones actuales de red.
- Utiliza TCP como protocolo subyacente, lo que proporciona robustez y compatibilidad con firewalls.
- Recomendado para:
  - Streaming de eventos públicos
  - Pantallas informativas con contenido multimedia

---

#### Adaptación de Calidad en Tiempo Real

El sistema se adapta automáticamente al ancho de banda disponible para garantizar una reproducción continua:

- En **DASH**, el reproductor mide el throughput (rendimiento de red) entre segmentos y ajusta la calidad del siguiente segmento.
- En sistemas UDP con codecs como **H.264/H.265**, se puede usar:
  - **FEC (Forward Error Correction)** para compensar pérdidas.
  - **Escalabilidad** en códecs (como **SVC - Scalable Video Coding**) que permite reducir la calidad sin re-encodear.

## 6. Seguridad – Estrategias y Configuración

### Políticas y Medidas de Seguridad:

### Paso 6: Seguridad – Estrategias y Configuración

Una infraestructura crítica como la de una ciudad inteligente requiere una política de seguridad integral que combine aislamiento de tráfico, autenticación fuerte, cifrado de extremo a extremo y control de accesos en cada nivel.

---

#### 1. Políticas y Medidas de Seguridad

##### a. Uso de VPN (Red Privada Virtual)

- Se establecerán túneles VPN para comunicar de forma segura segmentos críticos (por ejemplo, redes de emergencia con oficinas centrales).
- El tráfico entre estos segmentos será cifrado y autenticado.
- La VPN deberá utilizar cifrado fuerte (como AES) y protocolos robustos (como IPsec o WireGuard).
- La autenticación puede basarse en certificados digitales o credenciales seguras.

##### b. Firewalls

- Se ubicarán firewalls en los límites de cada segmento de red.
- Filtrarán tráfico entrante y saliente según políticas definidas por IP, puerto y protocolo.
- Deben registrar eventos sospechosos y permitir la creación de listas negras dinámicas.
- La política por defecto será "denegar todo" y permitir solo tráfico explícitamente autorizado.

##### c. Listas de Control de Acceso (ACLs)

- Se aplicarán en routers y switches de capa 3 para restringir el acceso entre subredes.
- Las ACLs controlarán qué direcciones IP o rangos pueden comunicarse y con qué servicios.
- Se aplicarán tanto a tráfico entrante como saliente para minimizar posibles vectores de ataque.
- Las reglas deben ordenarse desde las más específicas a las más generales.

---

#### 2. Configuración General

##### a. Segmentación de la Red

- Cada función crítica de la ciudad tendrá su propia subred aislada.
- La segmentación limitará el impacto de ataques laterales y facilitará la aplicación de políticas de seguridad específicas.

##### b. Monitoreo y Registro

- Todos los dispositivos de red (firewalls, routers, servidores) deben mantener logs.
- Se debe implementar un sistema centralizado de monitoreo y alertas (SIEM).
- El análisis de tráfico y patrones anómalos ayudará a detectar intrusiones o accesos no autorizados.

##### c. Actualizaciones y Mantenimiento

- Todos los dispositivos y servicios deben estar actualizados con parches de seguridad.
- Se implementará un ciclo de revisión regular de reglas de firewall, ACLs y certificados.

### Cifrado y Autenticación:

### Cifrado y Autenticación

En una infraestructura crítica, es indispensable aplicar mecanismos de cifrado y autenticación robustos para garantizar la confidencialidad, integridad y autenticidad de las comunicaciones y datos en tránsito.

---

### 1. Cifrado de Comunicaciones (TLS/SSL)

- **TLS (Transport Layer Security)** se utilizará para cifrar todas las comunicaciones entre clientes y servidores (web, correo, VPN).
- TLS reemplaza al antiguo SSL y debe implementarse en su versión más actualizada (TLS 1.3).
- Los certificados digitales serán generados por una CA (autoridad certificadora) interna o confiable.
- Los servicios HTTP, FTP y correo operarán sobre TLS para prevenir la interceptación o manipulación de datos.
- La validación del certificado garantiza la autenticidad del servidor.

---

### 2. Autenticación y Cifrado con RSA

- **RSA (Rivest-Shamir-Adleman)** se utilizará para establecer canales seguros de comunicación e intercambio de claves.
- El proceso consiste en:
  - Generar un par de claves pública/privada.
  - Usar la clave pública para cifrar datos (como una clave de sesión).
  - El receptor usa su clave privada para descifrar el mensaje.

Este esquema permite el establecimiento de una clave simétrica (para TLS, por ejemplo) de forma segura mediante un canal inseguro.

- Las claves deben ser de al menos 2048 bits para garantizar un nivel de seguridad adecuado.
- Las claves privadas deben almacenarse de forma segura, idealmente con protección por contraseña o en módulos de hardware (HSM).

---

### 3. Protección de Resolución de Nombres (DNSSEC)

- **DNSSEC (Domain Name System Security Extensions)** se implementará para proteger las consultas DNS frente a ataques como DNS Spoofing o Cache Poisoning.
- Funciona mediante:
  - Firmas digitales asociadas a cada registro DNS.
  - El servidor DNS responde con los datos solicitados y una firma que puede verificarse usando claves públicas.
- Solo los servidores con la clave correspondiente podrán firmar registros válidos.
- Los clientes (resolvers) deben estar configurados para validar firmas DNSSEC y descartar respuestas no verificadas.










