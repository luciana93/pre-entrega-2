# Instrucciones para Completar el Repositorio

## 📋 Estado Actual

El repositorio "Pre entrega 2" está **80% completado**. Falta agregar las capturas de pantalla en la carpeta `/screenshots/`.

---

## ✅ Completado

- ✓ README.md principal
- ✓ Documentación técnica completa (4 documentos MD)
- ✓ Estructura de directorios profesional
- ✓ Archivo .gitignore
- ✓ Toda la teoría y procedimientos documentados

---

## 📸 Pasos para Completar

### Paso 1: Crear Carpeta de Screenshots

```bash
mkdir -p screenshots
```

### Paso 2: Agregar las Capturas

Descarga o mueve tus imágenes a la carpeta `screenshots/`:

**Archivos esperados:**

1. `vm-snapshot.jpg` - Screenshot del snapshot "Clean Install - Hardening applied"
2. `red-nat.jpg` - Screenshot de configuración NAT en Settings
3. `usuario-creado.jpg` - Screenshot verificación de usuario con `cat /etc/passwd`
4. `permisos-archivo.jpg` - Screenshot de `ls -l archivo_test.txt`
5. `apt-upgrade.jpg` - Screenshot de `apt upgrade` completado
6. `vm-creation.jpg` (opcional) - Screenshot de creación de VM

**Comando para copiar:**
```bash
# Si las imágenes están en Downloads
cp ~/Downloads/*.jpg screenshots/

# Verificar
ls -la screenshots/
```

### Paso 3: Verificar Estructura

```bash
tree Pre-entrega-2/
# o si no está instalado 'tree':
find . -type f | head -20
```

**Estructura esperada:**
```
Pre-entrega-2/
├── README.md                 ← Archivo principal
├── .gitignore               ← Ignorar archivos
├── INSTRUCCIONES.md         ← Este archivo
├── docs/
│   ├── 01-Mapa-de-Riesgos.md
│   ├── 02-Lab-Setup.md
│   ├── 03-Hardening.md
│   └── 04-Auditoría.md
└── screenshots/
    ├── vm-snapshot.jpg
    ├── red-nat.jpg
    ├── usuario-creado.jpg
    ├── permisos-archivo.jpg
    ├── apt-upgrade.jpg
    └── vm-creation.jpg (opcional)
```

---

## 🚀 Subir a GitHub

### Paso 1: Crear Repositorio en GitHub

1. Ir a https://github.com/new
2. Repository name: `Pre-entrega-2`
3. Description: "Laboratorio Seguro de Ciberseguridad - Análisis de Riesgos y Hardening"
4. Seleccionar **Public** o **Private** según requieras
5. Click "Create repository"

### Paso 2: Inicializar Git Localmente

```bash
# Navegar a la carpeta del proyecto
cd Pre-entrega-2

# Inicializar repositorio git
git init

# Configurar usuario de git (si no está configurado)
git config user.name "Tu Nombre"
git config user.email "tu@email.com"

# Agregar todos los archivos
git add .

# Verificar qué se va a commitear
git status

# Realizar primer commit
git commit -m "Inicial: Documentación completa del laboratorio de ciberseguridad"

# Cambiar rama principal a main (opcional pero recomendado)
git branch -M main

# Agregar remoto (URL del repo que creaste en GitHub)
git remote add origin https://github.com/TuUsuario/Pre-entrega-2.git

# Hacer push al repositorio remoto
git push -u origin main
```

### Paso 3: Verificar en GitHub

- Ir a tu repositorio en GitHub
- Verificar que todos los archivos estén presentes
- Verificar que las imágenes se muestren en los documentos MD

---

## 📝 Links en Documentos

Los documentos MD hacen referencia a las imágenes. Asegúrate de que estén en la carpeta `screenshots/` con los nombres exactos.

**Ejemplo en Markdown**:
```markdown
![Screenshot](../screenshots/vm-snapshot.jpg)
```

---

## 🔧 Comandos Git Útiles

```bash
# Ver estado actual
git status

# Ver historial de commits
git log --oneline

# Agregar cambios después de editar
git add .
git commit -m "Descripción del cambio"
git push

# Ver archivos tracked
git ls-files

# Ver tamaño del repo
du -sh .git/
```

---

## ⚠️ Notas Importantes

### Tamaño de Archivos

- Cada imagen JPG: ~1-3 MB
- GitHub tiene límite de 100 MB por archivo
- Si las imágenes son muy grandes (>50 MB), considera comprimirlas

**Comprimir imagen**:
```bash
convert image.jpg -quality 85 image-compressed.jpg
```

### Gitignore

El archivo `.gitignore` excluye archivos no necesarios como:
- Archivos de sistema (.DS_Store)
- Archivos temporales
- Archivos de credenciales
- Logs

No es necesario editarlo a menos que agregues más tipos de archivos.

---

## 📞 Soporte

Si encuentras problemas:

1. **Git no reconoce cambios**: 
   ```bash
   git add -A
   git status
   ```

2. **Error de autenticación con GitHub**:
   - Usar token de acceso en lugar de contraseña
   - O configurar SSH keys

3. **Imagen no muestra en GitHub**:
   - Verificar que la ruta sea relativa: `../screenshots/image.jpg`
   - Verificar que el archivo existe y tiene extensión correcta

---

## ✨ Resultado Final

Una vez completado, tendrás un repositorio profesional en GitHub con:

- ✅ Documentación técnica completa
- ✅ Evidencias visuales (screenshots)
- ✅ Estructura organizada
- ✅ Versionado con Git
- ✅ Accesible para el profesor

**Acceso**: Comparte el URL del repositorio con tu profesor

---

**Última actualización**: 11 de Octubre de 2026
