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














