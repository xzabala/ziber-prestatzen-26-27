# RA5. Administración de Credenciales y PKI

## Descripción General
Este Resultado de Aprendizaje cubre la administración de credenciales de acceso aplicando requisitos de funcionamiento y seguridad, profundizando en Infraestructuras de Clave Pública (PKI), firmas electrónicas, RADIUS y NAC (Network Access Control).

## Herramientas y Tecnologías en Profundidad

1. **Easy-RSA / OpenSSL:**
   - Herramientas en línea de comandos para la generación manual de certificados X.509.
   - Easy-RSA facilita la gestión de una Autoridad Certificadora (CA) simple, muy útil para despliegues rápidos como VPNs.

2. **EJBCA (Enterprise JavaBeans Certificate Authority):**
   - Una de las soluciones PKI *Open Source* más completas para entornos empresariales reales.
   - Permite manejar CA raíz, CAs intermedias, validadores OCSP y listas de revocación (CRL).

3. **FreeRADIUS:**
   - El servidor RADIUS (Remote Authentication Dial-In User Service) de código abierto más utilizado.
   - Vital para centralizar la autenticación de dispositivos de red (switches, APs WiFi) contra directorios activos o bases de datos LDAP.

4. **PacketFence:**
   - Solución avanzada de Network Access Control (NAC).
   - Permite descubrir, perfilar, aislar y corregir endpoints conectados a la red antes de darles acceso total.

5. **Kerberos:**
   - Protocolo de autenticación en red basado en tickets, fundamental para *Single Sign-On (SSO)* en dominios empresariales.

## Ejercicios Prácticos Propuestos

### Ejercicio 1: Creación de una Jerarquía PKI y emisión de certificados web
- **Objetivo:** Entender la cadena de confianza en la que se basa Internet.
- **Desarrollo:** El alumnado usará OpenSSL o XCA (interfaz gráfica) para crear una **Root CA** autogenerada. Luego, crearán una **Sub-CA** firmada por la raíz, y emitirán certificados para servidores web (Apache/Nginx). 
- **Resolución:** Deberán importar la Root CA en los navegadores cliente para que la página HTTPS no muestre errores de seguridad. Realizarán también la revocación de un certificado (CRL).

### Ejercicio 2: Autenticación centralizada de red con RADIUS (IEEE 802.1X)
- **Objetivo:** Evitar que cualquier dispositivo se conecte libremente a los puertos físicos de la red.
- **Desarrollo:** Montar un servidor *FreeRADIUS*. Configurar un switch (simulado en GNS3/Packet Tracer o hardware real si lo hay) para que los puertos exijan autenticación 802.1X. El usuario debe autenticarse desde su PC cliente (Windows/Linux) usando un supplicant con usuario/contraseña o certificado antes de obtener IP.

### Ejercicio 3: Despliegue de un NAC con PacketFence
- **Objetivo:** Implementar control de acceso a nivel de red y portal cautivo.
- **Desarrollo:** Despliegue de una máquina virtual con PacketFence conectada a una red de laboratorio. Configurar un portal cautivo donde los dispositivos "invitados" deban registrarse. Asignar VLANs dinámicas (VLAN de aislamiento o VLAN de producción) según el cumplimiento de seguridad del dispositivo (ej. si tiene antivirus).

### Ejercicio 4: Autenticación SSH con Certificados
- **Objetivo:** Sustituir la tediosa gestión de claves públicas SSH estáticas por certificados de corta duración.
- **Desarrollo:** Configurar OpenSSH como Autoridad Certificadora. El servidor se configura para confiar en la CA. Se firma la clave pública del alumno con una validez de 24 horas. El alumno accederá al servidor sin contraseña durante ese periodo de tiempo.
