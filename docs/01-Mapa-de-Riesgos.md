# 1. Mapa de Riesgos Personales

## Objetivo

Identificar y analizar amenazas, vulnerabilidades y riesgos asociados con activos digitales personales aplicando el modelo **CIA Triad** (Confidencialidad, Integridad, Disponibilidad).

---

## 📊 Activos Digitales Analizados

### 1. Gmail (Correo Electrónico)

#### Confidencialidad
- **Amenazas**: Phishing, interceptación de contraseña, acceso no autorizado
- **Vulnerabilidades**: Contraseña débil, reutilización de credenciales, recuperación de cuenta insegura
- **Riesgo**: ALTO
- **Controles**: Autenticación de dos factores (2FA), contraseña fuerte, verificación de dispositivos

#### Integridad
- **Amenazas**: Modificación de correos, suplantación de identidad, malware
- **Vulnerabilidades**: Falta de verificación de remitentes, correos no cifrados
- **Riesgo**: MEDIO
- **Controles**: Verificación SPF/DKIM, filtros antiphishing, verificación de identidad

#### Disponibilidad
- **Amenazas**: DDoS en servidores, bloqueo de cuenta, pérdida de datos
- **Vulnerabilidades**: Recuperación de cuenta débil, falta de respaldo
- **Riesgo**: MEDIO
- **Controles**: Respaldos periódicos, números de teléfono de recuperación actualizados, verificación de actividad

---

### 2. Aplicación Bancaria (Banking)

#### Confidencialidad
- **Amenazas**: Phishing, malware, interceptación de datos, robo de credenciales
- **Vulnerabilidades**: Uso de WiFi público sin VPN, dispositivo comprometido, contraseña débil
- **Riesgo**: CRÍTICO
- **Controles**: Conexión VPN, autenticación de dos factores, certificados SSL/TLS

#### Integridad
- **Amenazas**: Modificación de transacciones, inyección de código, man-in-the-middle
- **Vulnerabilidades**: Aplicación sin verificación de integridad, conexión insegura
- **Riesgo**: CRÍTICO
- **Controles**: Verificación de certificados, HTTPS obligatorio, firma digital de transacciones

#### Disponibilidad
- **Amenazas**: DDoS, bloqueo de cuenta, fallo del sistema, pérdida de datos
- **Vulnerabilidades**: Recuperación de cuenta lenta, falta de respaldo de datos
- **Riesgo**: ALTO
- **Controles**: Múltiples canales de acceso (web, app, teléfono), respaldos redundantes

---

### 3. WhatsApp (Mensajería Instantánea)

#### Confidencialidad
- **Amenazas**: Interception, acceso a conversaciones, lectura de mensajes
- **Vulnerabilidades**: Backup sin encriptación, acceso al dispositivo, token de sesión comprometido
- **Riesgo**: ALTO
- **Controles**: Encriptación end-to-end, bloqueo de pantalla, verificación de identidad de contacto

#### Integridad
- **Amenazas**: Modificación de mensajes, suplantación, inyección de contenido
- **Vulnerabilidades**: Falta de verificación de remitente, código fuente no verificado
- **Riesgo**: MEDIO
- **Controles**: Encriptación end-to-end, verificación de clave de seguridad, confirmación de lectura

#### Disponibilidad
- **Amenazas**: Bloqueo de cuenta, pérdida de datos, indisponibilidad del servicio
- **Vulnerabilidades**: Recuperación de cuenta débil, falta de respaldo local
- **Riesgo**: MEDIO
- **Controles**: Múltiples métodos de recuperación, exportación de chats, respaldos en la nube

---

## 🔍 Matriz de Riesgos

| Activo | Confidencialidad | Integridad | Disponibilidad | Riesgo General |
|--------|------------------|-----------|-----------------|----------------|
| Gmail | ALTO | MEDIO | MEDIO | **ALTO** |
| Aplicación Bancaria | CRÍTICO | CRÍTICO | ALTO | **CRÍTICO** |
| WhatsApp | ALTO | MEDIO | MEDIO | **ALTO** |

---

## 📋 Recomendaciones por Activo

### Gmail
1. Habilitar autenticación de dos factores (2FA) inmediatamente
2. Usar contraseña única y fuerte (mínimo 16 caracteres)
3. Revisar dispositivos conectados mensualmente
4. Usar contraseñas de aplicación para apps de terceros
5. Configurar recuperación de cuenta con múltiples canales

### Aplicación Bancaria
1. **CRÍTICO**: Usar siempre conexión VPN en redes públicas
2. Habilitar autenticación biométrica (huella digital, reconocimiento facial)
3. Actualizar aplicación regularmente
4. Verificar HTTPS y certificados válidos
5. Usar tokens de seguridad hardware si está disponible
6. Revisar transacciones diariamente
7. Nunca compartir OTP o códigos de verificación

### WhatsApp
1. Habilitar bloqueo de pantalla con biometría
2. Hacer respaldos encriptados regularmente
3. Verificar clave de seguridad de contactos importantes
4. No descargar archivos de fuentes desconocidas
5. Actualizar aplicación a versión más reciente
6. Desactivar visibilidad de última conexión si es posible

---

## 🛡️ Medidas de Seguridad General

### Controles Técnicos
- Encriptación de discos duros
- Software antivirus/antimalware actualizado
- Firewall habilitado
- VPN para conexiones públicas
- Autenticación multifactor (MFA)

### Controles Administrativos
- Política de contraseñas fuerte
- Cambio regular de contraseñas
- Auditoría de actividad de cuentas
- Limitación de privilegios (principio de menor privilegio)
- Documentación de incidentes

### Controles Físicos
- Bloqueo de dispositivos
- Uso de biometría
- Protección de lugares donde se trabaja
- Protección contra robo

---

## 📌 Conclusión

Los activos digitales analizados presentan riesgos significativos, especialmente la aplicación bancaria que requiere controles robustos. La implementación de autenticación multifactor, contraseñas fuertes, y prácticas seguras de navegación son esenciales para mitigar estos riesgos.

La Confidencialidad es el aspecto más crítico en todos los activos, seguido por Disponibilidad e Integridad.

---

**Fecha de Análisis**: 11 de Octubre de 2026  
**Clasificación**: Análisis de Riesgos - Nivel Educativo
