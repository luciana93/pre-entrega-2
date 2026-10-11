# 2. Configuración del Laboratorio en VirtualBox

## Objetivo

Establecer un entorno de laboratorio seguro en VirtualBox con Kali Linux para prácticas de ciberseguridad, implementando principios fundamentales de seguridad y aislamiento de red.

---

## 🏢 Especificaciones del Entorno

### Hardware Virtual
- **Hipervisor**: VirtualBox
- **Sistema Operativo Guest**: Kali Linux
- **Procesadores**: 2 vCPU
- **RAM**: 2-4 GB
- **Almacenamiento**: 20 GB dinámico
- **Red**: NAT (Network Address Translation)

### Versiones
- **VirtualBox**: Última versión estable
- **Kali Linux**: Rolling Release
- **Kernel**: Linux 6.x

---

## 📋 Etapas de Configuración

### 1. Creación de la Máquina Virtual

#### Pasos Realizados
1. Abierto VirtualBox Manager
2. Click en "Nueva" (New)
3. Configuración de parámetros:
   - Nombre: Kali
   - Tipo: Linux
   - Versión: Debian 64-bit
   - Memoria: 2048 MB (mínimo recomendado)
   - Disco Duro: 20 GB dinámico

#### Evidencia
- Screenshot: `vm-creation.jpg` - Pantalla de creación de VM

---

### 2. Instalación de Kali Linux

#### Proceso
1. Descarga de ISO de Kali Linux desde sitio oficial
2. Montaje de ISO en unidad de CD/DVD virtual
3. Boot desde ISO
4. Instalación completa con:
   - Particionamiento automático
   - Configuración de red DHCP
   - Usuario root durante instalación

#### Verificación
```bash
uname -a  # Verificar kernel y versión
lsb_release -a  # Información de distribución
```

---

### 3. Configuración de Red - Modo NAT

#### Descripción Técnica

**NAT (Network Address Translation)** proporciona:
- **Aislamiento**: La VM no es accesible directamente desde la red externa
- **Seguridad**: Reduce superficie de ataque
- **Control**: El host controla la comunicación
- **Traducción**: Las conexiones salientes usan IP del host

#### Configuración Realizada

1. **Acceso a Settings**:
   - Click derecho en VM → "Propiedades" (Properties)
   - Menú "Red" (Network)

2. **Configuración de Adaptador**:
   - Adaptador 1 habilitado: ✓
   - Conectado a: **NAT**
   - Tipo de controlador: PCnet-PCI II
   - Promiscuous Mode: Deny

#### Equivalente en Línea de Comandos
```bash
# Verificar configuración de red
ip addr show
ip route show
```

#### Evidencia
- Screenshot: `red-nat.jpg` - Settings de VirtualBox mostrando NAT configurado

---

### 4. Actualización del Sistema

#### Importancia
- Parchear vulnerabilidades conocidas
- Actualizar herramientas de seguridad
- Mejorar estabilidad del sistema

#### Comandos Ejecutados

```bash
# Actualizar lista de paquetes
sudo apt update

# Actualizar paquetes del sistema
sudo apt upgrade -y

# Limpiar paquetes innecesarios (opcional)
sudo apt autoremove -y
sudo apt autoclean -y
```

#### Configuración de Repositorios

Se configuraron repositorios oficiales de Kali:
```bash
# /etc/apt/sources.list
deb http://http.kali.org/kali kali-rolling main non-free contrib
deb-src http://http.kali.org/kali kali-rolling main non-free contrib
```

#### Evidencia
- Screenshot: `apt-upgrade.jpg` - Salida de apt upgrade

---

### 5. Creación de Usuario Estándar

#### Principio de Seguridad: Menor Privilegio

**¿Por qué?**
- Usar root diariamente expone el sistema a riesgos
- Usuario estándar limita el daño en caso de compromiso
- Cumple con mejores prácticas de seguridad

#### Procedimiento

```bash
# Crear usuario "prueba" con directorio home
sudo useradd -m -s /bin/bash prueba

# Establecer contraseña
sudo passwd prueba
# Ingresar contraseña: prueba123

# Cambiar a usuario
su - prueba
```

#### Verificación

```bash
# Verificar creación de usuario
cat /etc/passwd | grep prueba

# Salida esperada:
# prueba:x:1002:1002::/home/prueba:/bin/bash

# Verificar ID del usuario
id prueba

# Salida:
# uid=1002(prueba) gid=1002(prueba) groups=1002(prueba)
```

#### Información del Usuario Creado
| Parámetro | Valor |
|-----------|-------|
| Username | prueba |
| UID | 1002 |
| GID | 1002 |
| Home | /home/prueba |
| Shell | /bin/bash |
| Privilegios | Usuario Estándar (no-root) |

#### Evidencia
- Screenshot: `usuario-creado.jpg` - Verificación de /etc/passwd

---

### 6. Demostración de Permisos de Archivo

#### Sistema de Permisos Linux

Formato: `-rw-r--r--`

```
-       rw-      r--      r--
|       |        |        |
|       |        |        +-- Otros (otros usuarios)
|       |        +----------- Grupo
|       +-------------------- Propietario
+----------------------------- Tipo (- = archivo)
```

| Posición | Significado |
|----------|------------|
| - | Archivo regular |
| r | Lectura (read) = 4 |
| w | Escritura (write) = 2 |
| x | Ejecución (execute) = 1 |

#### Procedimiento Realizado

```bash
# Cambiar a usuario "prueba"
su - prueba

# Navegar a directorio writable
cd /tmp

# Crear archivo de prueba
touch archivo_test.txt

# Mostrar permisos con ls -l
ls -l archivo_test.txt
```

#### Resultado

```
-rw-r--r-- 1 prueba prueba 0 oct 11 20:16 archivo_test.txt
```

#### Análisis de Permisos

| Componente | Valor | Significado |
|-----------|-------|-------------|
| Tipo | - | Archivo regular |
| Propietario | rw- | Lectura + Escritura (6) |
| Grupo | r-- | Solo Lectura (4) |
| Otros | r-- | Solo Lectura (4) |
| Notación Octal | 644 | Lectura/Escritura para propietario, Lectura para grupo/otros |

#### Interpretación de Seguridad
- El usuario "prueba" puede **leer y escribir** el archivo
- El grupo puede **solo leer**
- Otros usuarios pueden **solo leer**
- Nadie puede **ejecutar** (no es ejecutable)

#### Evidencia
- Screenshot: `permisos-archivo.jpg` - Salida de `ls -l archivo_test.txt`

---

## 🔒 Crear Snapshot

### Importancia
Un snapshot (instantánea) preserva el estado actual de la VM, permitiendo revertir cambios si es necesario.

### Procedimiento

1. **Con VM Apagada**:
   - Click derecho en VM
   - "Instantáneas" (Snapshots)
   - Click derecho → "Tomar Instantánea" (Take Snapshot)

2. **Detalles del Snapshot**:
   - Nombre: "Clean Install - Hardening applied"
   - Descripción: "Kali Linux con hardening inicial, usuario estándar, permisos configurados"

3. **Resultado**:
   - Snapshot guardado con timestamp
   - Referencia en línea temporal (snapshot tree)

### Utilidad
- **Reversión rápida** si configuración se corrompe
- **Comparación** entre versiones
- **Testing seguro** de cambios sin riesgo

#### Evidencia
- Screenshot: `vm-snapshot.jpg` - VirtualBox mostrando snapshot creado

---

## 📊 Tabla de Configuración Final

| Característica | Configuración |
|----------------|--------------|
| **Nombre VM** | Kali (Hardening Inicial) |
| **Red** | NAT (aislada) |
| **Usuario Admin** | root (raras ocasiones) |
| **Usuario Estándar** | prueba (UID 1002) |
| **Permisos Archivo** | 644 (rw-r--r--) |
| **SO** | Kali Linux Rolling |
| **Actualización** | APT update + upgrade |
| **Snapshot** | Clean Install - Hardening applied |

---

## ✅ Checklist de Configuración

- [x] VM creada en VirtualBox
- [x] Kali Linux instalado
- [x] Red configurada en NAT
- [x] Sistema actualizado (apt upgrade)
- [x] Usuario estándar "prueba" creado
- [x] Permisos de archivo verificados
- [x] Snapshot creado
- [x] Documentación completada

---

## 🎯 Objetivos Alcanzados

✅ Entorno virtual seguro establecido  
✅ Aislamiento de red implementado  
✅ Principio de menor privilegio aplicado  
✅ Sistema actualizado con parches de seguridad  
✅ Permisos de archivo documentados  
✅ Snapshot para recuperación disponible  

---

**Fecha de Configuración**: 11 de Octubre de 2026  
**Estado**: Completado ✓  
**Próximo Paso**: Auditoría de Seguridad con Lynis
