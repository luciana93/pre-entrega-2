# 4. Auditoría de Seguridad del Sistema

## Objetivo

Evaluar la postura de seguridad del laboratorio Kali Linux mediante auditoría automatizada con Lynis, identificando vulnerabilidades, riesgos de seguridad y recomendaciones de hardening.

---

## 🔧 Lynis - Security Auditing Tool

### ¿Qué es Lynis?

**Lynis** es una herramienta de auditoría de seguridad y endurecimiento del sistema de código abierto, desarrollada por **CISOfy**.

**Características**:
- Auditoría automatizada de sistemas Linux/Unix
- Identificación de vulnerabilidades de seguridad
- Evaluación de cumplimiento de normas (CIS Controls)
- Generación de reportes detallados
- Recomendaciones de hardening

**Sitio Oficial**: https://cisofy.com/lynis/

---

## 📥 Instalación y Configuración

### Instalación desde GitHub

```bash
# Clonar repositorio oficial
git clone https://github.com/CISOfy/lynis

# Navegar al directorio
cd lynis

# Verificar contenido
ls -la
```

**Estructura de Directorios**:
```
lynis/
├── lynis          # Script principal ejecutable
├── README         # Documentación
├── LICENSE        # Licencia (GPL v3)
├── plugins/       # Plugins de extensión
├── include/       # Módulos de componentes
└── db/           # Base de datos de referencias
```

### Permisos de Ejecución

```bash
# Dar permisos de ejecución al script principal
chmod +x lynis

# Verificar permisos
ls -l lynis
# -rwxr-xr-x 1 user user 47K Oct 11 20:30 lynis
```

---

## 🏃 Ejecución de Auditoría

### Comando Principal

```bash
# Auditoría completa del sistema
sudo ./lynis audit system

# Con modo quiet (menos salida)
sudo ./lynis audit system --quiet

# Guardando en archivo
sudo ./lynis audit system > lynis_audit_report.txt
sudo ./lynis audit system --quiet > lynis_audit_report.txt 2>&1
```

### Opciones Útiles

| Opción | Descripción |
|--------|------------|
| `audit system` | Auditoría completa |
| `--quiet` | Reduce salida de pantalla |
| `--debug` | Modo debug con información adicional |
| `--help` | Muestra ayuda |
| `--version` | Muestra versión |

---

## 📊 Áreas de Evaluación de Lynis

Lynis realiza auditorías en múltiples categorías:

### 1. **Bootloader & Kernel (Gestor de Arranque)**
- Verificación de GRUB/LILO
- Protección de bootloader
- Kernel hardening

### 2. **Filesystem (Sistema de Archivos)**
- Permisos de particiones
- Filesystems montados
- Puntos de montaje críticos

### 3. **Storage (Almacenamiento)**
- Encriptación de discos
- Integridad de datos
- Backups

### 4. **USB Devices (Dispositivos USB)**
- Control de dispositivos USB
- Restricciones de montaje

### 5. **Memory & Processes (Memoria y Procesos)**
- Address Space Layout Randomization (ASLR)
- Memory protection
- Procesos ejecutándose

### 6. **Nameservers (Servidores DNS)**
- Configuración de resolución
- Validación DNSSEC

### 7. **Networking (Red)**
- Interfaces de red
- Firewall configurado
- Servicios de red expuestos
- Port scanning

### 8. **Printers (Impresoras)**
- Servicios de impresión
- Configuración de CUPS

### 9. **Software (Aplicaciones)**
- Auditing tools disponibles
- Versiones de software

### 10. **SSH (Secure Shell)**
- Configuración de SSH daemon
- Autenticación
- Protocolos habilitados

### 11. **SNMP (Simple Network Management)**
- Community strings
- Configuración SNMP

### 12. **Databases (Bases de Datos)**
- Servicios de BD
- Configuración de seguridad

### 13. **LDAP (Lightweight Directory Access)**
- Servicio LDAP
- Configuración de autenticación

### 14. **NFS (Network File System)**
- Exports NFS
- Restricciones de acceso

### 15. **File Integrity (Integridad de Archivos)**
- AIDE/Tripwire
- Monitoreo de cambios

### 16. **Malware Scanning (Detección de Malware)**
- ClamAV
- Rootkit detection (rkhunter, chkrootkit)

### 17. **Logging & Monitoring (Registro y Monitoreo)**
- Syslog configurado
- Auditoria del sistema
- Log rotation

### 18. **File Permissions (Permisos de Archivo)**
- Permisos de archivos críticos
- Umask configurado
- SUID/SGID binarios

### 19. **User Accounts (Cuentas de Usuario)**
- Usuarios activos
- Contraseñas débiles
- Umask del usuario

### 20. **PAM (Pluggable Authentication)**
- Módulos de autenticación
- Políticas de contraseñas

### 21. **Sudo (Ejecución Privilegiada)**
- Configuración de sudoers
- Logging de sudo

### 22. **Session (Sesiones)**
- Timeouts de sesión
- Limpieza de sesiones

### 23. **Specific Tools (Herramientas Específicas)**
- Herramientas de seguridad
- Compiladores disponibles

---

## 📈 Interpretación de Resultados

### Estructura de Salida

```
[L] = Línea informativa (valor informativo)
[Y] = Sí (verificación pasada)
[N] = No (verificación fallida)
[?] = Desconocido (no pudo ser determinado)
[!] = Atención (elemento importante/warning)
[+] = Sugerencia (recomendación)
[-] = Información general
```

### Ejemplo de Salida

```
[+] System Tools
    [L] Scanning for available security tools...
    [L] systemd is installed (systemctl binary found)
    [L] Filesystem tools available
    [Y] Firewall software in use: ufw

[+] SSH Support
    [L] OpenSSH is installed
    [Y] SSH daemon is running
    [-] Configuration:
        - SSH protocol version: 2
        - Port: 22
        
[+] File Integrity
    [L] Checking file integrity tools...
    [N] aide is not installed (highly recommended!)

[+] Recommendations
    [+] Harden the system by installing aide, aide-common
        [L] Link: https://cisofy.com/controls/aide/
```

### Scoring de Lynis

Lynis genera un **score de seguridad** en una escala de 0-100:

| Rango | Evaluación |
|-------|-----------|
| 0-20 | Muy Bajo |
| 21-40 | Bajo |
| 41-60 | Medio |
| 61-80 | Bueno |
| 81-100 | Excelente |

---

## 🎯 Interpretación de Hallazgos Comunes

### Warnings Típicos en Kali Linux Mínimo

```
[!] No firewall actively in use or configured
    Recommendation: Enable UFW or configure iptables
    Risk Level: HIGH

[!] No swap memory found
    Recommendation: Configure swap partition
    Risk Level: MEDIUM

[!] SSH server is running with default settings
    Recommendation: Harden SSH configuration
    Risk Level: MEDIUM

[!] No intrusion detection system found
    Recommendation: Install Fail2Ban or similar
    Risk Level: MEDIUM

[+] File integrity software is not installed
    Recommendation: Install AIDE or Samhain
    Risk Level: LOW (for lab environment)
```

---

## 📋 Acciones Correctivas Recomendadas

### Prioridad CRÍTICA

```bash
# 1. Habilitar firewall
sudo ufw enable

# 2. Configurar SSH seguro
sudo nano /etc/ssh/sshd_config
# Cambiar: PermitRootLogin no
# Cambiar: PasswordAuthentication no
# Cambiar: PubkeyAuthentication yes
sudo systemctl restart sshd
```

### Prioridad ALTA

```bash
# 1. Instalar herramientas de integridad de archivos
sudo apt install aide aide-common

# 2. Instalar herramienta de prevención de fuerza bruta
sudo apt install fail2ban

# 3. Instalar detección de rootkits
sudo apt install chkrootkit rkhunter
```

### Prioridad MEDIA

```bash
# 1. Instalar Lynis para auditorías periódicas
# (Ya instalado)

# 2. Configurar logs de auditoría
sudo apt install auditd

# 3. Instalar herramienta de monitoreo
sudo apt install aide
```

---

## 📊 Reporte de Auditoría Esperado

### Secciones del Reporte

1. **Información del Sistema**
   - Nombre del host
   - Kernel version
   - OS y distribución
   - Uptime

2. **Resumen de Auditoría**
   - Tests ejecutados
   - Score total
   - Fecha de auditoría

3. **Hallazgos Positivos**
   - Elementos correctamente configurados
   - Medidas de seguridad implementadas

4. **Hallazgos Negativos**
   - Vulnerabilidades identificadas
   - Servicios innecesarios
   - Configuraciones débiles

5. **Recomendaciones**
   - Acciones correctivas
   - Prioridad de implementación
   - Enlaces a documentación

---

## 🔄 Auditoría Periódica

### Programación Recomendada

```bash
# Crear script de auditoría automática
cat > /opt/audit_lynis.sh << 'EOF'
#!/bin/bash
DATE=$(date +%Y%m%d_%H%M%S)
REPORT="/var/log/lynis_audit_${DATE}.txt"
sudo /path/to/lynis/lynis audit system > $REPORT
echo "Auditoría completada: $REPORT"
EOF

# Hacerlo ejecutable
chmod +x /opt/audit_lynis.sh

# Agregar a crontab para ejecución semanal
# crontab -e
# 0 2 * * 0 /opt/audit_lynis.sh  (Cada domingo a las 2 AM)
```

---

## 📌 Conclusiones de Auditoría

### Para Laboratorio Educativo

**Esperado**: Score entre 60-75 (Bueno)

**Razón**: Un entorno de laboratorio por naturaleza es menos endurecido que un servidor de producción.

### Elementos Críticos Verificados

✅ Usuario estándar (no root)  
✅ Permisos de archivo apropiados  
✅ Red aislada (NAT)  
✅ Sistema actualizado  
✅ Documentación de proceso  

### Mejoras Futuras

Para mayor hardening:
1. Habilitar firewall (UFW/iptables)
2. Configurar AIDE para integridad de archivos
3. Instalar Fail2Ban para protección de fuerza bruta
4. Configurar auditaría del sistema
5. Implementar detección de intrusiones

---

## 📖 Referencias

- **Lynis GitHub**: https://github.com/CISOfy/lynis
- **OWASP Linux Hardening**: https://cheatsheetseries.owasp.org/
- **CIS Controls**: https://www.cisecurity.org/controls
- **NIST Framework**: https://www.nist.gov/cyberframework

---

**Fecha de Auditoría**: 11 de Octubre de 2026  
**Herramienta**: Lynis (v3.x)  
**Propósito**: Evaluación de Laboratorio Educativo  
**Estado**: Completado ✓
