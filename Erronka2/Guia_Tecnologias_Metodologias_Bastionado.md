# Guía de Tecnologías y Metodologías - Bastionado de Redes y Sistemas

## Introducción
Este documento detalla las metodologías didácticas y las tecnologías (software, hardware y plataformas) recomendadas para impartir los Resultados de Aprendizaje (RA4 a RA10) del módulo "Bastionado de Redes y Sistemas" del Curso de Especialización en Ciberseguridad en Entornos de las Tecnologías de la Información.

## Metodología General
Para el desarrollo de estos RAs se propone una metodología eminentemente práctica y orientada a la realidad del sector profesional:
- **Aprendizaje Basado en Retos (ABR / ETHAZI):** Planteamiento de escenarios realistas donde el alumnado debe diseñar, implementar y asegurar infraestructuras completas.
- **Laboratorios Virtuales (Hands-on Labs):** Uso intensivo de entornos de virtualización (nativa o anidada) para desplegar topologías de red complejas sin riesgo para la infraestructura del centro educativo.
- **Simulación de Escenarios (Blue Team / Red Team):** Prácticas donde el alumnado debe defender una infraestructura (Blue Team) mientras otro equipo o el docente realiza pruebas de intrusión (Red Team).
- **Resolución de Casos Prácticos y Troubleshooting:** Fomento de la capacidad analítica mediante la resolución de problemas técnicos (ej. análisis de logs, investigación de caídas de servicio, alertas de seguridad).

---

## RA4. Configura sistemas de control de acceso y autenticación de personas preservando la confidencialidad y privacidad de los datos.

### Metodologías
- **Talleres prácticos guiados:** Configuración paso a paso de los diferentes métodos de autenticación en múltiples sistemas operativos.
- **Análisis de vulnerabilidades:** Laboratorios controlados de *cracking* de contraseñas (fuerza bruta, diccionario) y evasión de medidas débiles para justificar la necesidad de MFA/2FA.

### Tecnologías a utilizar
- **Gestión de Identidades:** Windows Server (Active Directory), entornos GNU/Linux (OpenLDAP, PAM).
- **Autenticación Multifactor (MFA/2FA y OTP):** Google Authenticator, Authy, Duo Security. Integración práctica con Linux mediante `libpam-google-authenticator`.
- **Certificados y Tarjetas Inteligentes:** OpenSSL (generación manual), XCA (interfaz gráfica), simuladores de Smartcards, OpenSC.
- **Tokens Físicos:** YubiKey (si hay disponibilidad en el aula) o en su defecto emuladores virtuales de tokens de hardware.
- **Gestores de Contraseñas:** KeePassXC (local), Bitwarden / Vaultwarden (despliegue de un servidor propio en el aula para entorno corporativo).
- **Biometría:** Configuración de Windows Hello for Business o herramientas en Linux como `howdy` o `fprintd`.

---

## RA5. Administra credenciales de acceso a sistemas informáticos aplicando los requisitos de funcionamiento y seguridad establecidos.

### Metodologías
- **Laboratorios de Infraestructura de Clave Pública (PKI):** Diseño completo, implementación y revocación en una jerarquía de certificación.
- **Análisis de Casos de Estudio:** Inspección de certificados reales en internet, identificación de certificados revocados o autofirmados no confiables.

### Tecnologías a utilizar
- **Infraestructura de Clave Pública (PKI):** Easy-RSA, EJBCA (para simular un entorno empresarial completo) o Microsoft Active Directory Certificate Services (AD CS).
- **Control de Acceso a la Red (NAC):** PacketFence (solución *Open Source* muy completa) o Forescout (si existen licencias o versiones de evaluación).
- **Servidores de Administración de Credenciales / AAA:** FreeRADIUS (RADIUS), demonios TACACS+.
- **Protocolos y Servicios de Acceso:** Kerberos (mit-krb5 en Linux o integrado en Windows AD), SSH con autenticación basada en claves y certificados.

---

## RA6. Diseña redes de computadores contemplando los requisitos de seguridad.

### Metodologías
- **Diseño Topológico:** Uso de herramientas de diagramación antes de la implementación para planificar la segmentación lógica y perimetral.
- **Implementación Simulada:** Despliegue de topologías complejas que en equipos físicos sería inviable por coste, aplicando VLANs, DMZ y subredes.

### Tecnologías a utilizar
- **Simulación y Emulación de Redes:** GNS3, EVE-NG o Cisco Packet Tracer (para conceptos base).
- **Entornos de Virtualización de Servidores:** Proxmox VE, VMware ESXi o OpenStack.
- **Cortafuegos Perimetrales (Virtuales):** pfSense, OPNsense, Sophos XG Firewall (versión Home/Educativa), FortiGate (VM de evaluación).
- **Seguridad Inalámbrica:** Hostapd (para simular APs directamente desde Linux), WPA3, 802.1x con RADIUS.
- **Túneles Seguros y VPN (IPSec):** strongSwan, OpenVPN, WireGuard.
- **Proxy Web:** Squid Proxy (configuración explícita y transparente), E2guardian (filtrado de contenido).

---

## RA7. Configura dispositivos y sistemas informáticos cumpliendo los requisitos de seguridad.

### Metodologías
- **Auditoría y Análisis de Tráfico:** Laboratorios de captura y disección de paquetes para detectar anomalías y errores de configuración.
- **Despliegue de un SOC básico en el aula:** Integración de herramientas *Open Source* para centralizar alertas y monitorizar eventos de seguridad.

### Tecnologías a utilizar
- **WAF y NGFW:** pfSense/OPNsense con complementos IDS, ModSecurity o Coraza (como Web Application Firewall).
- **Prevención y Detección de Intrusiones (IDS/IPS):** Snort, Suricata, Zeek.
- **Monitorización, Análisis de Logs y SIEM:** Elastic Stack (Elasticsearch, Logstash, Kibana), Wazuh (XDR y SIEM integral, muy recomendado por su facilidad y potencia), Graylog.
- **DLP y Seguridad de Correo:** Proxmox Mail Gateway, Apache SpamAssassin, soluciones DLP *Open Source* como MyDLP (o similares).
- **Análisis de Tráfico:** Wireshark, tcpdump, Nmap.
- **Monitorización de Dispositivos (SNMP):** Zabbix, Nagios o LibreNMS.

---

## RA8. Configura dispositivos para la instalación de sistemas informáticos minimizando las probabilidades de exposición a ataques.

### Metodologías
- **Prácticas Bare-Metal y Máquinas Virtuales:** Interacción con el proceso pre-arranque, particionado estructurado y aplicación de cifrado integral.
- **Simulación de Desastres:** Ejercicios de alta disponibilidad forzando caídas de nodos y verificando la continuidad.

### Tecnologías a utilizar
- **Pre-Instalación y Arranque:** Simuladores de BIOS/UEFI, Secure Boot, contraseñas de GRUB/Firmware.
- **Cifrado de Discos y Particionado:** LUKS (Linux Unified Key Setup), BitLocker (Windows), VeraCrypt. LVM (Logical Volume Manager) para aislar `/var`, `/tmp`, `/home`.
- **Alta Disponibilidad (HA):** Proxmox HA Cluster, Pacemaker, Corosync, DRBD, configuraciones de bonding de red.
- **Honeypots y Honeynets:** T-Pot (plataforma multi-honeypot de Telekom Security), Pentbox, Dionaea.
- **Procesamiento de Logs:** Uso de herramientas de agregación como Rsyslog o Fluentd conectados a Kibana/Grafana.

---

## RA9. Configura sistemas informáticos minimizando las probabilidades de exposición a ataques.

### Metodologías
- **Aplicación de Estándares (Hardening):** Seguimiento y aplicación rigurosa de guías de buenas prácticas institucionales (CIS, INCIBE, CCN-CERT).
- **Automatización de Seguridad:** Uso de metodologías *Infrastructure as Code* (IaC) para aplicar políticas de bastionado de forma uniforme a múltiples máquinas.

### Tecnologías a utilizar
- **Guías de Hardening:** CIS Benchmarks, Guías STIG.
- **Automatización del Bastionado:** Ansible, Chef o Puppet (recomendado Ansible por su curva de aprendizaje).
- **Protección del Sistema Operativo:** AppArmor, SELinux, Iptables/Nftables/UFW, Windows Firewall con Seguridad Avanzada.
- **Sistemas de Detección en Host (HIDS):** OSSEC, Wazuh Agent, Fail2Ban, AIDE (Advanced Intrusion Detection Environment) o Tripwire.
- **Sistemas de Copias de Seguridad:** Bacula, Veeam Backup & Replication (Community Edition), rsync, Duplicati.

---

## RA10. Diseña la integración de la parte IT con la parte OT asegurando los dispositivos OT ante posibles ataques internos o externos a la organización.

### Metodologías
- **Simulación de Entornos Industriales (ICS/SCADA):** Dada la dificultad de disponer de hardware OT real en muchas aulas, se prioriza el uso de potentes simuladores virtuales interconectados.
- **Role-play IT vs OT:** Talleres para comprender el choque de prioridades (ej. en IT prima la Confidencialidad, en OT prima la Disponibilidad absoluta y la seguridad física).
- **Búsqueda e Inteligencia de Amenazas OT:** Laboratorios sobre cómo los atacantes descubren sistemas de control industrial expuestos en internet.

### Tecnologías a utilizar
- **Sistemas de Control Industrial / Simuladores:** OpenPLC (simulador de PLC en software), ScadaBR / ScadaLTS, Factory I/O (para simular de forma visual entornos 3D de fábrica conectados a los PLCs).
- **Sistemas de Auditoría:** Kali Linux, Moki (distribución enfocada a auditoría de control industrial).
- **Inteligencia y Descubrimiento:** Shodan (búsqueda de PLCs, RTUs, HMI expuestos).
- **Explotación y Pentesting OT:** Metasploit Framework (uso de módulos específicos para ICS/SCADA), scripts de Nmap para Modbus (`modbus-discover`, etc.).
- **Protocolos OT y Honeypots Industriales:** Simuladores para Modbus TCP y Profinet, Conpot (Honeypot de ICS/SCADA para detectar escaneos).
