# RA6. Diseño de Redes Seguras

## Descripción General
Este Resultado de Aprendizaje trata sobre el diseño de redes de computadores contemplando segmentación física y lógica (VLANs, subnetting), zonas desmilitarizadas (DMZ), túneles VPN (IPSec) y uso de firewalls virtuales y proxys.

## Herramientas y Tecnologías en Profundidad

1. **GNS3 / EVE-NG:**
   - Simuladores/emuladores de red potentes que permiten correr imágenes reales de routers (Cisco, MikroTik) y sistemas operativos.
   - Ideal para probar topologías complejas y protocolos de enrutamiento y seguridad (IPSec).

2. **pfSense / OPNsense:**
   - Cortafuegos de siguiente generación basados en FreeBSD.
   - Ofrecen interfaz web intuitiva, enrutamiento avanzado, NAT, servidores VPN (OpenVPN/IPSec/WireGuard), IDS/IPS y alta disponibilidad (CARP).

3. **Proxmox VE (Virtual Environment):**
   - Plataforma de virtualización basada en Debian/KVM.
   - Muy útil para crear laboratorios completos "dentro de una caja", emulando redes físicas con *Linux Bridges* y *VLAN Tags*.

4. **strongSwan (IPSec) y WireGuard:**
   - *strongSwan* es el estándar *de facto* para configurar VPN IPSec Site-to-Site en servidores Linux.
   - *WireGuard* es una alternativa moderna, rápida y criptográficamente más robusta en muchos casos para túneles y conexiones de clientes.

5. **Squid Proxy:**
   - Servidor Proxy-Cache muy consolidado, utilizado para aplicar políticas de filtrado web, listas blancas/negras y control de ancho de banda.

## Ejercicios Prácticos Propuestos

### Ejercicio 1: Segmentación de red y Subnetting (VLANs)
- **Objetivo:** Eliminar redes planas e aislar dominios de difusión (broadcast).
- **Desarrollo:** En un entorno GNS3 o Cisco Packet Tracer, diseñar una red con múltiples departamentos (ej. IT, Finanzas, Ventas, Invitados). Aplicar *subnetting* eficiente (VLSM) para calcular las subredes de cada área y configurar las VLAN correspondientes en los switches, asignando direccionamiento.

### Ejercicio 2: Implementación de una DMZ con pfSense
- **Objetivo:** Exponer servicios al exterior de forma controlada sin comprometer la red interna (LAN).
- **Desarrollo:** Desplegar una máquina virtual pfSense en Proxmox con tres interfaces de red (WAN, LAN, DMZ). En la DMZ se instalará un servidor web (Nginx). El alumnado deberá configurar reglas de firewall para permitir que tráfico entrante de la WAN acceda al servidor web (Port Forwarding), pero bloqueando explícitamente cualquier inicio de sesión desde la DMZ hacia la LAN.

### Ejercicio 3: Túnel VPN Site-to-Site (IPSec)
- **Objetivo:** Interconectar de forma segura dos sucursales geográficamente separadas a través de internet.
- **Desarrollo:** Utilizar dos instancias de pfSense o routers MikroTik (simulados) que actuarán como *gateways* de dos sedes ("Sede Madrid" y "Sede Bilbao"). Configurar fase 1 y fase 2 de IPSec para encriptar todo el tráfico entre la red LAN 1 y la red LAN 2 de forma transparente para los usuarios.

### Ejercicio 4: Proxy web transparente y restricción de navegación
- **Objetivo:** Controlar el acceso a internet y auditar el uso de la web corporativa.
- **Desarrollo:** Instalar Squid Proxy junto a *SquidGuard* o *E2guardian* en un servidor Ubuntu/Debian. Interceptar el tráfico web y bloquear el acceso a sitios de redes sociales o descargas durante horario laboral. Configurar reglas para que un departamento concreto sí tenga acceso irrestricto.
