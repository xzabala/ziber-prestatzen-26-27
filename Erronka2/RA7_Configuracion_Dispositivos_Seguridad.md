# RA7. Configuración de Dispositivos y Sistemas de Seguridad

## Descripción General
Este Resultado de Aprendizaje se enfoca en configurar cortafuegos avanzados, sistemas y reglas de filtrado perimetral, desplegar firewalls de aplicaciones web (WAF) y gestionar centros de operaciones de seguridad (SOC) mediante herramientas de monitorización y SIEMs.

## Herramientas y Tecnologías en Profundidad

1. **Wazuh (XDR y SIEM):**
   - Una de las plataformas *Open Source* más completas para seguridad endpoint, monitorización de logs, análisis de vulnerabilidades y cumplimiento normativo (PCI-DSS, CIS).
   - Combina motor de OSSEC con stack Elastic (ahora Wazuh Indexer) para visualizar alertas en tiempo real.

2. **Suricata / Snort (IDS/IPS):**
   - Motores de análisis de tráfico en red.
   - Suricata es moderno, multi-hilo y nativamente compatible con reglas Snort. Pueden configurarse en modo prevención (IPS) desechando paquetes maliciosos (ej. *drop* en nfqueue).

3. **ModSecurity (WAF):**
   - Firewall de aplicaciones web (Web Application Firewall). 
   - Inspecciona peticiones HTTP buscando ataques a la capa de aplicación (SQL Injection, XSS, Path Traversal). Se utiliza siempre con las reglas OWASP Core Rule Set (CRS).

4. **Elastic Stack (ELK - Elasticsearch, Logstash, Kibana):**
   - Herramientas de ingesta, indexación y visualización de volúmenes masivos de datos/logs. Base fundamental de cualquier arquitectura de monitorización moderna.

5. **Wireshark / tcpdump:**
   - Esenciales para análisis forense de paquetes de red y solución de problemas (*troubleshooting*).

## Ejercicios Prácticos Propuestos

### Ejercicio 1: Despliegue de un entorno SIEM con Wazuh
- **Objetivo:** Centralizar logs y monitorizar activos de la organización (conceptos básicos de un SOC).
- **Desarrollo:** Instalar Wazuh Server en una máquina virtual. Desplegar Wazuh Agent en dos servidores (Windows y Linux). Generar eventos anómalos intencionados (creación masiva de usuarios locales, fallos de login) y monitorizar cómo saltan las alertas en el dashboard web.

### Ejercicio 2: Detección y prevención de intrusiones en red (Suricata)
- **Objetivo:** Analizar tráfico de red y detectar escaneos o ataques automatizados.
- **Desarrollo:** Instalar Suricata en modo IDS escuchando la interfaz externa de un servidor. Desde una máquina atacante externa (Kali Linux), lanzar escaneos agresivos con Nmap y ataques de denegación de servicio (SYN Flood). Revisar los archivos `fast.log` o `eve.json` de Suricata para comprobar que las firmas han saltado correctamente.

### Ejercicio 3: Protección de una aplicación web vulnerable (WAF)
- **Objetivo:** Mitigar vulnerabilidades de código de capa 7 sin modificar el software.
- **Desarrollo:** Desplegar una aplicación intencionadamente vulnerable (como DVWA o OWASP Juice Shop). El alumno realizará un ataque exitoso de *SQL Injection*. Posteriormente, instalarán Nginx o Apache como *Reverse Proxy* con el módulo ModSecurity y OWASP CRS activado. Repetirán el ataque para comprobar que ahora es bloqueado y se devuelve un error 403.

### Ejercicio 4: Análisis de tráfico forense con Wireshark
- **Objetivo:** Identificar comportamiento no deseado a nivel de paquetes.
- **Desarrollo:** Se proporciona al alumno un archivo PCAP (`.pcap`) que contiene la captura de red de un ataque de malware o exfiltración de datos encubierta (ej. exfiltración a través de peticiones DNS). Deben utilizar los filtros de Wireshark para identificar la máquina comprometida y el payload extraído.
