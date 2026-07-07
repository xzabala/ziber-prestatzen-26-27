## RA4. Configura sistemas de control de acceso y autenticación de personas preservando la

### Contenidos
Configuración de sistemas de control de acceso y autenticación de personas.
– Mecanismos de autenticación. Tipos de factores.
– Técnicas de autenticación: contraseñas, certificados digitales, tokens, contraseñas de un solo
uso (OTP), características biométricas, combinaciones de las anteriores, etc.

---

# RA4. Control de Acceso y Autenticación

## Descripción General
Este Resultado de Aprendizaje se enfoca en configurar sistemas de control de acceso y autenticación de personas preservando la confidencialidad y privacidad de los datos, cubriendo MFA, biometría, tokens y protocolos basados en contraseñas y tarjetas inteligentes.

## Herramientas y Tecnologías en Profundidad

1. **Pluggable Authentication Modules (PAM) en Linux:**
   - Framework subyacente de autenticación en sistemas Linux.
   - Permite apilar módulos (ej. `pam_tally2` o `pam_faillock` para bloqueo de cuentas tras fallos, `pam_pwquality` para robustez de contraseñas).

2. **Google Authenticator (`libpam-google-authenticator`):**
   - Implementa algoritmos TOTP (Time-based One-Time Password).
   - Se integra directamente con el subsistema PAM de Linux para forzar MFA en SSH o inicios de sesión locales.

3. **Active Directory (Windows Server):**
   - Políticas de contraseñas finas (Fine-Grained Password Policies - FGPP) para aplicar diferentes requisitos según el grupo de usuarios.
   - Windows Hello for Business para autenticación sin contraseña (PIN, biometría).

4. **KeePassXC / Vaultwarden:**
   - KeePassXC como ejemplo de bóveda de contraseñas *offline* (archivo cifrado).
   - Vaultwarden (implementación ligera de Bitwarden en Rust) ideal para montar con Docker y gestionar contraseñas en equipo.

5. **John the Ripper / Hashcat:**
   - Herramientas ofensivas para *cracking* de contraseñas.
   - Esenciales para enseñar (mediante la práctica) por qué las contraseñas cortas o sin salting son vulnerables.

## Ejercicios Prácticos Propuestos

### Ejercicio 1: Auditoría de contraseñas y aplicación de políticas de robustez (Linux/Windows)
- **Objetivo:** Demostrar la vulnerabilidad de las contraseñas débiles y mitigarlo.
- **Desarrollo:** El alumnado extraerá los hashes de un sistema vulnerable (copia de `/etc/shadow` o volcado SAM) y usará *John The Ripper* o *Hashcat* con diccionarios conocidos (ej. `rockyou.txt`).
- **Resolución:** Configurar `pam_pwquality` en Linux para exigir longitud de 12 caracteres, mayúsculas, números y símbolos, y configurar la política de bloqueo temporal tras 3 intentos fallidos.

### Ejercicio 2: Implementación de MFA en accesos remotos (SSH)
- **Objetivo:** Securizar un servicio expuesto añadiendo un segundo factor.
- **Desarrollo:** Instalar el paquete `libpam-google-authenticator` en un servidor Ubuntu/Debian. Modificar `/etc/pam.d/sshd` y `/etc/ssh/sshd_config` para requerir el código OTP en los inicios de sesión por SSH. El alumnado debe vincularlo con su móvil usando Authy o Google Authenticator.

### Ejercicio 3: Despliegue de un Gestor de Contraseñas Corporativo
- **Objetivo:** Concienciar sobre el uso de credenciales únicas y compartición segura.
- **Desarrollo:** Utilizando *Docker* o *Podman*, el alumnado desplegará una instancia de *Vaultwarden*. Deberán configurar HTTPS (requisito de Bitwarden), crear organizaciones, invitar a otros compañeros de clase y compartir credenciales en colecciones seguras.

### Ejercicio 4: Emulación de autenticación con Smartcards/Tokens
- **Objetivo:** Entender la autenticación multifactor basada en posesión física (algo que tengo).
- **Desarrollo:** Utilizar simuladores de tarjetas inteligentes (Smartcards) o tokens USB virtuales para configurar el inicio de sesión en un entorno Active Directory simulado. Si hay hardware disponible (YubiKey), configurar acceso a cuentas Linux con el módulo de Yubico.
