# Pre Entrega 2 - Laboratorio Seguro de Ciberseguridad

## Descripción

Este repositorio contiene la documentación completa del **Laboratorio Seguro de Ciberseguridad**, un proyecto educativo que implementa principios fundamentales de seguridad informática en un entorno virtualizado.

El proyecto incluye:

1. **Mapa de Riesgos Personales** - Análisis de amenazas y vulnerabilidades aplicadas a activos digitales personales
2. **Laboratorio de Seguridad en VirtualBox** - Configuración e hardening de una máquina virtual Kali Linux
3. **Auditoría de Seguridad** - Evaluación de la seguridad del sistema utilizando herramientas profesionales

---

## Contenidos

### 📋 Documentación

- **[01-Mapa-de-Riesgos.md](./docs/01-Mapa-de-Riesgos.md)** - Análisis de confidencialidad, integridad y disponibilidad de activos digitales
- **[02-Lab-Setup.md](./docs/02-Lab-Setup.md)** - Configuración del laboratorio en VirtualBox
- **[03-Hardening.md](./docs/03-Hardening.md)** - Proceso de endurecimiento del sistema
- **[04-Auditoría.md](./docs/04-Auditoría.md)** - Resultados de auditoría de seguridad

### 📸 Evidencias

Las capturas de pantalla de cada etapa del proyecto se encuentran en la carpeta `/screenshots`:

- `vm-snapshot.jpg` - Snapshot "Clean Install - Hardening applied"
- `red-nat.jpg` - Configuración de red en modo NAT
- `usuario-creado.jpg` - Verificación de creación de usuario estándar
- `permisos-archivo.jpg` - Demostración de permisos de archivo (ls -l)
- `apt-upgrade.jpg` - Actualización de paquetes del sistema

---

## 🏗️ Estructura del Proyecto

```
Pre-entrega-2/
├── README.md
├── docs/
│   ├── 01-Mapa-de-Riesgos.md
│   ├── 02-Lab-Setup.md
│   ├── 03-Hardening.md
│   └── 04-Auditoría.md
├── screenshots/
│   ├── vm-snapshot.jpg
│   ├── red-nat.jpg
│   ├── usuario-creado.jpg
│   ├── permisos-archivo.jpg
│   └── apt-upgrade.jpg
└── scripts/
    └── setup-notes.txt
```

---

## 🔐 Conceptos Clave

### CIA Triad (Triada de Seguridad)

- **Confidencialidad**: Protección de información contra acceso no autorizado
- **Integridad**: Asegurar que la información no sea modificada sin autorización
- **Disponibilidad**: Garantizar acceso a recursos cuando se necesitan

### Principio de Menor Privilegio

Se implementó mediante la creación de usuarios estándar (no root) para ejecutar tareas diarias, limitando el riesgo de exposición ante vulnerabilidades.

### Hardening del Sistema

Proceso de endurecimiento que incluye:
- Configuración de red segura (NAT)
- Actualización de paquetes del sistema
- Configuración correcta de permisos de archivos
- Auditoría de seguridad con Lynis

---

## 🛠️ Herramientas Utilizadas

- **VirtualBox** - Hipervisor para virtualización
- **Kali Linux** - Distribución Linux especializada en seguridad
- **Lynis** - Herramienta de auditoría de seguridad
- **APT** - Gestor de paquetes de Debian/Kali

---

## 📝 Procedimiento Realizado

### 1. Creación de Snapshot
Se creó un snapshot de VirtualBox named "Clean Install - Hardening applied" para preservar el estado base del sistema después del hardening.

### 2. Configuración de Red
Se configuró la VM en modo **NAT** para:
- Aislar el laboratorio de la red principal
- Permitir comunicación saliente controlada
- Mantener seguridad de la red host

### 3. Creación de Usuario Estándar
```bash
sudo useradd -m -s /bin/bash prueba
sudo passwd prueba
```
Se verificó con: `cat /etc/passwd | grep prueba`

### 4. Actualización del Sistema
```bash
sudo apt update && sudo apt upgrade -y
```

### 5. Demostración de Permisos
Se creó archivo de prueba y se mostraron permisos con `ls -l`:
```
-rw-r--r-- 1 prueba prueba 0 oct 11 20:16 archivo_test.txt
```

### 6. Auditoría de Seguridad
Se ejecutó Lynis para evaluar la postura de seguridad del sistema:
```bash
sudo ./lynis audit system
```

---

## 📊 Resultados

### Mapa de Riesgos
- **3 activos analizados**: Gmail, Aplicación Bancaria, WhatsApp
- **Amenazas identificadas**: Phishing, malware, interceptación, pérdida de disponibilidad
- **Controles implementados**: Autenticación, encriptación, backups

### Laboratorio
- **Snapshot**: Creado exitosamente
- **Red**: Configurada en modo NAT
- **Usuario**: prueba (UID 1002, no-root)
- **Permisos**: Verificados y documentados
- **Auditoría**: Completada con Lynis

---

## 🎯 Objetivos Alcanzados

✅ Análisis de riesgos de activos digitales personales  
✅ Configuración segura de máquina virtual en VirtualBox  
✅ Implementación del principio de menor privilegio  
✅ Hardening del sistema operativo  
✅ Auditoría de seguridad del laboratorio  
✅ Documentación completa del proceso  

---

## 📚 Referencias

- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)
- [CIS Controls](https://www.cisecurity.org/controls)
- [Kali Linux Documentation](https://www.kali.org/docs/)
- [Lynis Security Audit Tool](https://cisofy.com/lynis/)

---

**Autor**: Luciana  
**Fecha**: 11 de Octubre de 2026  
**Institución**: Trabajo Académico de Ciberseguridad
