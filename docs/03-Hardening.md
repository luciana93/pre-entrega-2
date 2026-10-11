# 3. Hardening del Sistema

## Objetivo

Documentar e implementar medidas de endurecimiento (hardening) del sistema operativo Kali Linux para aumentar su postura de seguridad y reducir la superficie de ataque.

---

## 🛡️ ¿Qué es Hardening?

El endurecimiento de sistemas es el proceso de eliminar vulnerabilidades de un servidor, máquina o aplicación para reducir su exposición a ataques.

### Principios Fundamentales

1. **Defensa en Profundidad** - Múltiples capas de seguridad
2. **Principio de Menor Privilegio** - Solo acceso necesario
3. **Minimización** - Deshabilitar servicios innecesarios
4. **Monitoreo** - Detectar actividad sospechosa
5. **Actualización** - Mantener parches de seguridad

---

## 📋 Medidas de Hardening Implementadas

### 1. Configuración de Red Segura

#### NAT (Network Address Translation)
```
┌─────────────────────────────────────┐
│         Red Externa / Internet      │
└──────────────────┬──────────────────┘
                   │
           ┌───────▼────────┐
           │   NAT Gateway   │
           │  (Host VirtualBox)
           └───────┬────────┘
                   │
┌──────────────────┴──────────────────┐
│    VM (Kali Linux) - Aislada       │
│    IP Interna: 10.0.2.x             │
└─────────────────────────────────────┘
```

**Beneficios**:
- VM no es accesible directamente desde afuera
- Comunicación saliente controlada
- Ataques externos no pueden acceder a VM

**Configuración**:
```
Adaptador de Red: NAT
Modo Promiscuo: Deny
```

### 2. Actualización de Paquetes del Sistema

#### Comandos Ejecutados
```bash
# 1. Actualizar índice de paquetes
sudo apt update

# 2. Upgradar paquetes con actualizaciones de seguridad
sudo apt upgrade -y

# 3. Limpiar paquetes deprecated
sudo apt autoremove -y
sudo apt autoclean -y
```

#### Componentes Actualizados
- Kernel del sistema
- Herramientas de seguridad
- Librerías del sistema
- Utilidades del SO

#### Importancia
- Parchea vulnerabilidades conocidas (CVEs)
- Mejora estabilidad y rendimiento
- Actualiza definiciones de firmas de malware
- Implementa parches de seguridad

### 3. Gestión de Usuarios y Acceso

#### Principio de Menor Privilegio

**Implementación**:
```bash
# Usuario estándar (no root)
useradd -m -s /bin/bash prueba

# Asignación de contraseña
passwd prueba
```

**Ventajas**:
- Limita impacto de vulnerabilidades explotadas por usuario estándar
- Fuerza uso de `sudo` para tareas administrativas (auditable)
- Aislamiento de sesiones de usuario

#### Usuarios del Sistema
```bash
# Verificar usuarios existentes
cat /etc/passwd

# Estructura de /etc/passwd:
# username:x:uid:gid:gecos:home:shell
```

#### Archivo de Sudoers
```bash
# Ver permisos de sudoers
sudo visudo

# Usuario "prueba" puede usar sudo si está en grupo sudo
# Configuración:
# %sudo ALL=(ALL:ALL) ALL
```

### 4. Configuración de Permisos de Archivo

#### Sistema de Permisos Linux (Modelo DAC)

**Niveles de Acceso**:
```
-rw-r--r--
│ ││ ││ ││
│ ││ ││ └┴─ Otros (o) = 4
│ ││ └┴──── Grupo (g) = 4
│ └┴─────── Propietario (u) = 6
└────────── Tipo de archivo
```

**Notación Octal**:
- 4 = Lectura (r)
- 2 = Escritura (w)
- 1 = Ejecución (x)

#### Permisos Verificados

**Archivo de Prueba**:
```bash
# Creación
touch archivo_test.txt

# Verificación
ls -l archivo_test.txt

# Resultado
-rw-r--r-- 1 prueba prueba 0 oct 11 20:16 archivo_test.txt
```

**Análisis**:
- Propietario (prueba): 6 (rw-) - Lectura + Escritura
- Grupo (prueba): 4 (r--) - Solo lectura
- Otros: 4 (r--) - Solo lectura
- Permisos Totales: 644

#### Mejores Prácticas de Permisos

| Archivo/Directorio | Permisos | Justificación |
|-------------------|----------|--------------|
| Archivos regulares | 644 | Propietario rw-, Otros ro |
| Directorios | 755 | Propietario rwx, Otros rx |
| Scripts ejecutables | 755 | Permite ejecución |
| Archivos sensibles | 600 | Solo propietario |
| Directorios personales | 700 | Solo propietario |

#### Comandos de Configuración
```bash
# Cambiar permisos
chmod 644 archivo.txt

# Cambiar propietario
chown usuario:grupo archivo.txt

# Cambiar recursivamente
chmod -R 755 /var/www/
chown -R usuario:grupo /home/usuario/
```

### 5. Configuración de Repositorios

#### Importancia
- Garantiza paquetes seguros y verificados
- Acceso a actualizaciones oficiales
- Previene instalación de paquetes maliciosos

#### Repositorios Configurados

**Archivo: /etc/apt/sources.list**
```
deb http://http.kali.org/kali kali-rolling main non-free contrib
deb-src http://http.kali.org/kali kali-rolling main non-free contrib
```

**Secciones**:
- **main**: Paquetes soportados por Kali
- **contrib**: Paquetes que dependen de no-free
- **non-free**: Software no libre

**Ramas**:
- **kali-rolling**: Última versión (rolling release)

#### Verificación
```bash
# Ver repositorios configurados
cat /etc/apt/sources.list

# Listar repos habilitados
grep -r "^deb" /etc/apt/sources.list*
```

### 6. Deshabilitación de Servicios Innecesarios

#### Principio
Minimizar servicios en ejecución = Menor superficie de ataque

#### Servicios de Kali (Típicos)
```bash
# Listar servicios
systemctl list-units --type=service --state=running

# Deshabilitar servicio
sudo systemctl disable bluetooth

# Detener servicio
sudo systemctl stop bluetooth

# Verificar estado
sudo systemctl status bluetooth
```

### 7. Configuración de Firewall

#### UFW (Uncomplicated Firewall)
```bash
# Habilitar firewall
sudo ufw enable

# Mostrar estado
sudo ufw status

# Permitir puerto 22 (SSH)
sudo ufw allow 22/tcp

# Denegar puerto (ej: 23)
sudo ufw deny 23/tcp

# Ver reglas
sudo ufw status numbered
```

**Política por Defecto**:
- INPUT: DENY (rechazar entrada)
- OUTPUT: ALLOW (permitir salida)
- FORWARD: DENY (no enrutamiento)

### 8. Auditoría de Seguridad

#### Herramienta: Lynis
```bash
# Instalación
git clone https://github.com/CISOfy/lynis
cd lynis

# Ejecución
sudo ./lynis audit system

# Salida completa a archivo
sudo ./lynis audit system > lynis_report.txt
```

---

## 📊 Resumen de Medidas Implementadas

| Medida | Estado | Impacto |
|--------|--------|--------|
| NAT Network | ✓ Implementado | ALTO - Aislamiento |
| APT Update/Upgrade | ✓ Completado | CRÍTICO - Parches |
| Usuario Estándar | ✓ Creado | ALTO - Menor Privilegio |
| Permisos de Archivo | ✓ Verificados | MEDIO - Acceso Controlado |
| Repositorios | ✓ Configurados | MEDIO - Paquetes Seguros |
| Snapshot | ✓ Creado | MEDIO - Recuperación |

---

## 🔍 Verificación de Hardening

### Comandos de Control

```bash
# 1. Verificar actualizaciones pendientes
apt list --upgradable

# 2. Mostrar usuarios del sistema
cat /etc/passwd | grep -v nologin

# 3. Ver permisos de directorios críticos
ls -la /etc/ | head -20

# 4. Verificar servicios activos
systemctl list-units --state=running --type=service

# 5. Revisar logs de seguridad
sudo tail -f /var/log/auth.log

# 6. Estado del firewall
sudo ufw status verbose

# 7. Conexiones de red
sudo netstat -an | grep LISTEN
```

---

## 🎯 Checklist de Hardening

- [x] Red configurada en NAT
- [x] Sistema actualizado (kernel + paquetes)
- [x] Usuario estándar creado (no-root)
- [x] Permisos de archivo documentados
- [x] Repositorios oficiales configurados
- [x] Snapshot creado
- [x] Servicios innecesarios identificados
- [x] Auditoría de seguridad planificada

---

## 📈 Impacto de Medidas

### Antes de Hardening
- Sistema sin parches
- Usuario root por defecto
- Servicios potencialmente innecesarios
- Configuración genérica

### Después de Hardening
- ✅ Sistema actualizado y parchado
- ✅ Menor privilegio implementado
- ✅ Servicios minimizados
- ✅ Configuración endurecida
- ✅ Auditoría de seguridad lista

---

## 🔗 Relación con CIA Triad

### Confidencialidad ↑
- Permisos de archivo restrictos
- Acceso basado en roles
- NAT aislamiento

### Integridad ↑
- Permisos de escritura limitados
- Verificación de paquetes
- Auditoría de cambios

### Disponibilidad ↑
- Snapshot para recuperación rápida
- Parches de estabilidad
- Monitoreo de servicios

---

**Fecha de Implementación**: 11 de Octubre de 2026  
**Estado**: Completado ✓  
**Próximo Paso**: Auditoría con Lynis y análisis de resultados
