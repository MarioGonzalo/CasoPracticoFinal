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

*Insertar capturas cuando esté el cisco y el drawio y tal *

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

# Hay que terminar esto

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

# Esto para cuando el cisco esté terminado y tal mejor

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










