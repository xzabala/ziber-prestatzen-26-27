# RA9. Configuración y Bastionado de Sistemas (Hardening)

## Descripción General
Este Resultado de Aprendizaje profundiza en minimizar las probabilidades de exposición de un sistema ya instalado. Incluye el concepto de *hardening* o bastionado, eliminación de servicios innecesarios, HIDS, prevención de exploits de memoria, y automatización y copias de seguridad.

## Herramientas y Tecnologías en Profundidad

1. **Ansible:**
   - Herramienta líder en configuración de *Infrastructure as Code (IaC)*. Sin agentes en destino (solo requiere SSH). 
   - Fundamental para escalar el bastionado a decenas de servidores de manera idempotente.

2. **CIS Benchmarks y OpenSCAP:**
   - El *Center for Internet Security (CIS)* provee guías exhaustivas y configuraciones para endurecer Sistemas Operativos.
   - *OpenSCAP* automatiza la validación de un sistema frente a las reglas del CIS, emitiendo un informe HTML.

3. **AppArmor / SELinux:**
   - Sistemas de Control de Acceso Obligatorio (MAC - Mandatory Access Control).
   - Complementan a los permisos DAC tradicionales (usuario/grupo) al restringir de qué archivos o capacidades puede hacer uso un proceso concreto, mitigando ataques de escalada de privilegios o *zero-days*.

4. **Fail2Ban:**
   - Analizador de logs que bloquea automáticamente direcciones IP temporales o permanentes que muestran intentos repetidos de acceso fallido, integrándose con Iptables.

5. **Sistemas de Backup corporativo:**
   - Herramientas como Bacula, Veeam o BorgBackup. Esenciales como última línea de defensa ante incidentes como el *Ransomware*.

## Ejercicios Prácticos Propuestos

### Ejercicio 1: Auditoría inicial y cumplimiento (OpenSCAP)
- **Objetivo:** Conocer el estado basal de seguridad del sistema antes y después del bastionado.
- **Desarrollo:** Instalar OpenSCAP en un servidor limpio recién instalado (Ubuntu/RHEL). Lanzar un escaneo aplicando un perfil de seguridad institucional (ej. Perfil PCI-DSS o CIS). Analizar el reporte HTML resultante y elegir 5 fallos indicados para solucionarlos manualmente.

### Ejercicio 2: Hardening Automatizado con Ansible
- **Objetivo:** Aprender a desplegar políticas de seguridad a gran escala.
- **Desarrollo:** El alumnado escribirá un *Playbook* de Ansible (*Role*) de endurecimiento base para sus servidores Linux. Este playbook deberá automatizar: desactivación de accesos root vía SSH (`PermitRootLogin no`), cambio de puerto SSH, configuración del firewall UFW cerrando todo por defecto, aplicación de *sysctl* contra ataques de red (ej. prevención SYN flood, desactivar ruteo ICMP), e inhabilitación de módulos no usados como IPv6 o USB-storage.

### Ejercicio 3: Restricción de Procesos con AppArmor/SELinux
- **Objetivo:** Confinar servicios críticos para minimizar el daño si son vulnerados.
- **Desarrollo:** En un sistema Ubuntu/Debian con AppArmor activado (o SELinux en Fedora/RHEL), instalar un servidor web Nginx o base de datos MySQL. Visualizar su estado de confinamiento y crear/modificar un perfil de AppArmor (*complain mode* vs *enforce mode*) forzando a que el servidor Nginx no pueda acceder a directorios como `/etc` o a archivos que no pertenezcan al document root (`/var/www/html`), mitigando vulnerabilidades tipo Local File Inclusion (LFI).

### Ejercicio 4: Mitigación de Fuerza Bruta y Backup
- **Objetivo:** Respuesta activa contra ataques e implementación de contingencias.
- **Desarrollo:** Instalar y configurar Fail2Ban para proteger el acceso a un servidor FTP o SSH expuesto. Realizar una prueba de fuerza bruta con Hydra o Medusa y constatar cómo el firewall bloquea temporalmente la IP atacante. Posteriormente, configurar una política de copias de seguridad de `/etc` y bases de datos utilizando *rsync* enviando la copia de forma cifrada a un servidor remoto, simulando un esquema de respaldo externo (off-site backup).
