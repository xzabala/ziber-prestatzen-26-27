# RA8. Instalación Segura de Sistemas (Minimizando Exposición)

## Descripción General
Este Resultado de Aprendizaje cubre cómo configurar los dispositivos base y la instalación de los propios sistemas operativos de manera que se prevengan ataques físicos y lógicos: BIOS/UEFI seguras, cifrado de ficheros, particionado, alta disponibilidad y honeynets.

## Herramientas y Tecnologías en Profundidad

1. **UEFI Secure Boot / TPM:**
   - La primera línea de defensa a nivel hardware. Secure Boot evita la carga de bootloaders modificados (ej. rootkits). 
   - El TPM (Trusted Platform Module) permite el almacenamiento de claves criptográficas hardware.

2. **LUKS (Linux Unified Key Setup) / BitLocker:**
   - El estándar para el cifrado completo de disco (Full Disk Encryption) en Linux y Windows, mitigando la amenaza de robo físico de hardware.

3. **LVM (Logical Volume Manager):**
   - Abstracción de particionado que permite redimensionar discos en caliente en Linux.
   - En seguridad, permite segmentar puntos de montaje conflictivos (ej. aislar `/var` y asignar atributos `noexec` y `nosuid` a `/tmp`).

4. **Proxmox HA / Pacemaker / Corosync:**
   - Tecnologías que permiten configurar clusters de Alta Disponibilidad. Aseguran la "Disponibilidad", uno de los 3 pilares clásicos de la Ciberseguridad (CIA - Confidencialidad, Integridad, Disponibilidad).

5. **T-Pot / Pentbox (Honeypots):**
   - Sistemas trampa creados para engañar a atacantes. Pentbox es muy sencillo para iniciarse, mientras que T-Pot es una plataforma completa y profesional basada en Docker con ELK para visualización de los ataques sufridos.

## Ejercicios Prácticos Propuestos

### Ejercicio 1: Particionado Seguro y Cifrado Integral (FDE)
- **Objetivo:** Asegurar que los datos sean ilegibles si el servidor es robado físicamente.
- **Desarrollo:** Realizar una instalación manual en máquina virtual de Debian o Ubuntu Server. Durante la instalación de discos, configurar LVM sobre una partición cifrada con LUKS. Además, segmentar lógicamente `/var`, `/home` y `/tmp`, asignando a las dos últimas las opciones de montaje `nodev`, `nosuid` y `noexec` para impedir la ejecución de malware en esos directorios.

### Ejercicio 2: Asegurar el Arranque (Secure Boot y GRUB)
- **Objetivo:** Prevenir que un atacante físico pueda alterar el inicio del sistema operativo para obtener root.
- **Desarrollo:** Configurar la BIOS virtual para habilitar UEFI y Secure Boot. Además, asignar una contraseña al cargador de arranque (GRUB2) en Linux para evitar que un usuario manipule los parámetros de carga del kernel (ej. añadir `init=/bin/bash` para ganar acceso root sin contraseña).

### Ejercicio 3: Implementación de Alta Disponibilidad (HA)
- **Objetivo:** Garantizar la continuidad del servicio ante fallos de hardware.
- **Desarrollo:** Crear un clúster mínimo de dos nodos Proxmox (o simulando máquinas virtuales y DRBD). Desplegar un servicio crítico (como una base de datos o servidor web) en una máquina virtual. Apagar abruptamente el nodo principal y observar cómo el clúster mueve o reinicia la máquina virtual automáticamente en el nodo secundario en cuestión de segundos o minutos.

### Ejercicio 4: Despliegue de una Honeynet
- **Objetivo:** Analizar el comportamiento del atacante mediante el uso del engaño.
- **Desarrollo:** Instalar T-Pot en un servidor aislado o utilizar una versión más ligera como *Cowrie* (honeypot de SSH/Telnet). El alumno debe "exponer" el honeypot (o atacarlo desde Kali Linux) realizando fuerza bruta contra SSH. Posteriormente analizarán los logs de Kibana para ver las contraseñas intentadas, las IPs de origen, y si el malware ha descargado herramientas adicionales.
