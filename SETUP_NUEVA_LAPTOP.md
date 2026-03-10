# 🚀 GUÍA COMPLETA DE SETUP EN NUEVA LAPTOP
## Sistema HAPI FHIR con Autenticación JWT y Frontend Flutter

**Fecha de Actualización**: 10 de Marzo, 2026  
**Repositorio**: https://github.com/UlisesBGZ/HapiFhir-Springboot  
**Tiempo Estimado**: 1-2 horas (dependiendo de velocidad de internet)

---

## 🤖 DOCUMENTACIÓN PARA LA NUEVA IA - LEER PRIMERO

**⚠️ IMPORTANTE**: Antes de empezar el setup, la nueva IA debe leer estos archivos para entender el proyecto:

### **📄 Opción 1: Inicio Rápido (5 minutos)** ⭐ RECOMENDADO

1. **[.github/copilot-instructions.md](.github/copilot-instructions.md)** ← Se lee automáticamente por GitHub Copilot
2. **[PROMPT_PARA_NUEVA_IA.md](PROMPT_PARA_NUEVA_IA.md)** ← Copiar TODO el contenido y pegar en chat de Copilot

### **📄 Opción 2: Contexto Completo (30 minutos)**

1. **[LEEME_DOCUMENTACION.md](LEEME_DOCUMENTACION.md)** - Índice de toda la documentación
2. **[CONTEXTO_PARA_NUEVA_SESION.md](CONTEXTO_PARA_NUEVA_SESION.md)** - Contexto técnico completo (29 KB)
3. **[DESARROLLO_COMPLETO.md](DESARROLLO_COMPLETO.md)** - Historia detallada del desarrollo (57 KB)

### **📄 Documentación por Tema Específico**

- **Setup**: [CHECKLIST_TRANSFERENCIA.md](CHECKLIST_TRANSFERENCIA.md)
- **Autenticación**: [AUTHENTICATION.md](AUTHENTICATION.md) + [AUTH_INTEGRATION_GUIDE.md](AUTH_INTEGRATION_GUIDE.md)
- **Tests**: [TESTING.md](TESTING.md)
- **Git/GitHub**: [GUIA_GITHUB.md](GUIA_GITHUB.md)
- **VS Code**: [GUIA_TRANSFERIR_VSCODE.md](GUIA_TRANSFERIR_VSCODE.md)
- **Sistema Completo**: [README_SISTEMA_COMPLETO.md](README_SISTEMA_COMPLETO.md)
- **Configuración Servidor**: [SERVIDOR_CONFIGURADO.md](SERVIDOR_CONFIGURADO.md)
- **Bitácora Académica**: [BITACORA_METODOLOGIA.md](BITACORA_METODOLOGIA.md)

### **💬 Prompt para GitHub Copilot Chat**

```
Hola, necesito que me ayudes con este proyecto.

Por favor lee estos archivos:
1. .github/copilot-instructions.md
2. PROMPT_PARA_NUEVA_IA.md
3. CONTEXTO_PARA_NUEVA_SESION.md

Después dame un resumen de:
- Stack tecnológico
- Endpoints principales
- Cómo ejecutar el proyecto
- Cómo ejecutar tests
- Configuraciones importantes
```

---

## 📋 TABLA DE CONTENIDOS

0. [Documentación para la Nueva IA - Leer Primero](#-documentación-para-la-nueva-ia---leer-primero)
1. [Prerrequisitos - Instalación de Software](#1-prerrequisitos---instalación-de-software)
2. [Clonar Repositorio desde GitHub](#2-clonar-repositorio-desde-github)
3. [Configurar Backend (Spring Boot)](#3-configurar-backend-spring-boot)
4. [Configurar Frontend (Flutter)](#4-configurar-frontend-flutter)
5. [Configurar Base de Datos (Docker)](#5-configurar-base-de-datos-docker)
6. [Actualizar IP de Red (Solo para móvil)](#6-actualizar-ip-de-red-solo-para-móvil)
7. [Ejecutar el Sistema Completo](#7-ejecutar-el-sistema-completo)
8. [Verificar Funcionamiento](#8-verificar-funcionamiento)
9. [Ejecutar Tests](#9-ejecutar-tests)
10. [Solución de Problemas](#10-solución-de-problemas)

---

## 1. PRERREQUISITOS - INSTALACIÓN DE SOFTWARE

### 1.1. Java JDK 17 o Superior

**¿Por qué lo necesitas?**  
Spring Boot y HAPI FHIR requieren Java para ejecutar el backend.

**Pasos de Instalación**:

1. **Descargar Java 17**:
   - Ir a: https://adoptium.net/
   - Descargar: "Temurin 17 (LTS)" para Windows
   - Versión: `.msi` installer (recomendado)

2. **Instalar**:
   - Ejecutar el archivo `.msi` descargado
   - ✅ Marcar: "Add to PATH"
   - ✅ Marcar: "Set JAVA_HOME variable"
   - Click "Next" hasta finalizar

3. **Verificar Instalación**:
   ```powershell
   # Abrir PowerShell y ejecutar:
   java -version
   ```
   
   **Salida esperada**:
   ```
   openjdk version "17.0.x" 2024-xx-xx
   OpenJDK Runtime Environment Temurin-17.0.x
   OpenJDK 64-Bit Server VM Temurin-17.0.x
   ```

4. **Si NO funciona (no detecta comando)**:
   - Agregar manualmente a PATH:
   ```
   Variable: JAVA_HOME
   Valor: C:\Program Files\Eclipse Adoptium\jdk-17.x.x-hotspot
   
   Variable: Path
   Agregar: %JAVA_HOME%\bin
   ```
   - Reiniciar PowerShell
   - Volver a verificar con `java -version`

---

### 1.2. Flutter SDK 3.38 o Superior

**¿Por qué lo necesitas?**  
El frontend está desarrollado en Flutter y necesitas el SDK para ejecutarlo.

**Pasos de Instalación**:

1. **Descargar Flutter**:
   - Ir a: https://docs.flutter.dev/get-started/install/windows
   - Descargar: "flutter_windows_X.X.X-stable.zip"
   - Tamaño aproximado: ~1 GB

2. **Extraer Flutter**:
   - Extraer el ZIP en: `C:\src\flutter` (recomendado)
   - **NO** extraer en `C:\Program Files\` (problemas de permisos)
   - Ruta final: `C:\src\flutter\bin\flutter.bat`

3. **Agregar a PATH**:
   ```
   Variable: Path
   Agregar: C:\src\flutter\bin
   ```

4. **Verificar Instalación**:
   ```powershell
   # Cerrar y reabrir PowerShell
   flutter --version
   ```
   
   **Salida esperada**:
   ```
   Flutter 3.38.7 • channel stable
   Framework • revision xxxxx
   Engine • revision xxxxx
   Tools • Dart 3.10.7
   ```

5. **Ejecutar Flutter Doctor** (Importante):
   ```powershell
   flutter doctor
   ```
   
   **Salida esperada**:
   ```
   [✓] Flutter (Channel stable, 3.38.7)
   [✓] Windows Version (Installed version of Windows is version 10 or higher)
   [✓] Chrome - develop for the web
   [!] Android toolchain - develop for Android devices
       ⚠ Android SDK no encontrado (opcional si solo quieres web)
   [✓] VS Code (version X.X.X)
   [✓] Connected device (1 available)
   [✓] Network resources
   ```

6. **Si flutter doctor marca problemas**:
   
   **Problema: "cmdline-tools component is missing"**
   ```powershell
   # NO es necesario si solo usarás web
   # Si quieres Android, ejecutar:
   flutter doctor --android-licenses
   ```
   
   **Problema: "Chrome not found"**
   ```powershell
   # Instalar Google Chrome
   # Reiniciar y ejecutar: flutter doctor
   ```

---

### 1.3. Docker Desktop

**¿Por qué lo necesitas?**  
PostgreSQL 16 (base de datos) corre en un contenedor Docker.

**Pasos de Instalación**:

1. **Descargar Docker Desktop**:
   - Ir a: https://www.docker.com/products/docker-desktop/
   - Descargar: "Docker Desktop for Windows"
   - Tamaño aproximado: ~500 MB

2. **Requisitos Previos**:
   - Windows 10 64-bit: Pro, Enterprise, or Education (Build 19041 or higher)
   - O Windows 11
   - WSL 2 habilitado (Docker lo habilita automáticamente)

3. **Instalar Docker Desktop**:
   - Ejecutar el instalador
   - ✅ Marcar: "Use WSL 2 instead of Hyper-V" (recomendado)
   - Esperar a que termine (puede tardar 5-10 minutos)
   - **Reiniciar la computadora** (requerido)

4. **Iniciar Docker Desktop**:
   - Abrir Docker Desktop desde el menú inicio
   - Esperar a que muestre: "Docker Desktop is running"
   - Aceptar términos de servicio si aparece

5. **Verificar Instalación**:
   ```powershell
   docker --version
   ```
   
   **Salida esperada**:
   ```
   Docker version 20.10.x, build xxxxx
   ```
   
   ```powershell
   docker-compose --version
   ```
   
   **Salida esperada**:
   ```
   Docker Compose version v2.x.x
   ```

6. **Verificar que Docker está corriendo**:
   ```powershell
   docker ps
   ```
   
   **Salida esperada**: Tabla vacía (sin errores)
   ```
   CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
   ```

---

### 1.4. Git (Recomendado)

**¿Por qué lo necesitas?**  
Para clonar el repositorio desde GitHub y sincronizar cambios.

**Pasos de Instalación**:

1. **Descargar Git**:
   - Ir a: https://git-scm.com/download/win
   - Descargar: "64-bit Git for Windows Setup"

2. **Instalar Git**:
   - Ejecutar el instalador
   - **Importante**: En la pantalla "Adjusting your PATH environment":
     - ✅ Seleccionar: "Git from the command line and also from 3rd-party software"
   - Dejar todas las demás opciones por defecto
   - Click "Next" hasta finalizar

3. **Verificar Instalación**:
   ```powershell
   git --version
   ```
   
   **Salida esperada**:
   ```
   git version 2.x.x.windows.x
   ```

4. **Configurar Git** (Primera vez):
   ```powershell
   git config --global user.name "Tu Nombre"
   git config --global user.email "tu@email.com"
   ```

---

### 1.5. Visual Studio Code (Opcional pero Recomendado)

**¿Por qué lo necesitas?**  
Editor de código con soporte para Java, Flutter, y terminales integradas.

**Pasos de Instalación**:

1. **Descargar VS Code**:
   - Ir a: https://code.visualstudio.com/
   - Descargar: "Windows x64 User Installer"

2. **Instalar VS Code**:
   - Ejecutar el instalador
   - ✅ Marcar: "Add to PATH"
   - ✅ Marcar: "Add 'Open with Code' action to Windows Explorer context menu"
   - Click "Next" hasta finalizar

3. **Extensiones Recomendadas** (instalar después de abrir el proyecto):
   - Extension Pack for Java
   - Spring Boot Extension Pack
   - Flutter
   - Dart
   - GitHub Copilot (opcional)
   - Docker

---

## 📊 RESUMEN DE PRERREQUISITOS

Antes de continuar, verifica que TODOS estos comandos funcionen:

```powershell
java -version      # Java 17+
flutter --version  # Flutter 3.38+
docker --version   # Docker 20+
git --version      # Git 2.x+
```

**Si TODOS funcionan**: ✅ Continúa a la Sección 2  
**Si alguno falla**: ⚠️ Revisa su instalación antes de continuar

---

## 2. CLONAR REPOSITORIO DESDE GITHUB

### 2.1. Crear Carpeta de Trabajo

```powershell
# Abrir PowerShell
# Navegar al Desktop
cd $env:USERPROFILE\Desktop

# Verificar que estás en Desktop
pwd
# Debe mostrar: C:\Users\TU_USUARIO\Desktop
```

---

### 2.2. Clonar Repositorio

```powershell
# Clonar el proyecto
git clone https://github.com/UlisesBGZ/HapiFhir-Springboot.git

# Salida esperada:
# Cloning into 'HapiFhir-Springboot'...
# remote: Enumerating objects: 9952, done.
# remote: Counting objects: 100% (9952/9952), done.
# remote: Compressing objects: 100% (3511/3511), done.
# remote: Total 9952 (delta 3770), reused 9952 (delta 3770)
# Receiving objects: 100% (9952/9952), 6.19 MiB | 1.50 MiB/s, done.
# Resolving deltas: 100% (3770/3770), done.
```

**Tiempo estimado**: 2-5 minutos dependiendo de tu conexión a internet.

---

### 2.3. Verificar Clonación Exitosa

```powershell
# Entrar al directorio
cd HapiFhir-Springboot

# Verificar estructura
ls

# Debes ver estas carpetas y archivos:
# .github/
# .mvn/
# flutter_frontend/
# src/
# docker-compose.yml
# mvnw.cmd
# pom.xml
# README.md
# [múltiples archivos .md de documentación]
```

---

### 2.4. Verificar Archivos Críticos

```powershell
# Verificar Maven Wrapper (CRÍTICO)
Test-Path .mvn\wrapper\maven-wrapper.jar
# Debe mostrar: True

# Verificar tamaño del Maven Wrapper
(Get-Item .mvn\wrapper\maven-wrapper.jar).Length / 1KB
# Debe mostrar: ~63 KB (61.5 KB aprox)

# Verificar Flutter pubspec
Test-Path flutter_frontend\pubspec.yaml
# Debe mostrar: True

# Verificar Docker Compose
Test-Path docker-compose.yml
# Debe mostrar: True
```

**Si todos muestran `True`**: ✅ Clonación exitosa  
**Si alguno muestra `False`**: ❌ Re-clonar el repositorio

---

## 3. CONFIGURAR BACKEND (SPRING BOOT)

### 3.1. Instalar Dependencias de Maven

**¿Qué hace este comando?**  
Descarga todas las librerías Java necesarias (Spring Boot, HAPI FHIR, JWT, etc.) y compila el backend.

```powershell
# Asegúrate de estar en la raíz del proyecto
cd C:\Users\TU_USUARIO\Desktop\HapiFhir-Springboot

# Ejecutar Maven wrapper (primera vez tomará tiempo)
.\mvnw.cmd clean install

# Salida esperada (proceso largo):
# [INFO] Scanning for projects...
# [INFO] ------------------------------------------------------------------------
# [INFO] Building hapi-fhir-jpaserver-starter X.X.X
# [INFO] ------------------------------------------------------------------------
# Downloading from central: https://repo.maven.apache.org/...
# Downloaded from central: ... (X KB at X KB/s)
# [... muchas líneas de descarga ...]
# 
# [INFO] --- maven-compiler-plugin:X.X.X:compile ---
# [INFO] Compiling XXX source files to target\classes
#
# [INFO] --- maven-surefire-plugin:X.X.X:test ---
# [INFO] Running ca.uhn.fhir.jpa.starter.auth.AuthControllerTest
# [INFO] Tests run: 12, Failures: 0, Errors: 0, Skipped: 0
# [INFO] Running ca.uhn.fhir.jpa.starter.auth.UserControllerTest
# [INFO] Tests run: 11, Failures: 0, Errors: 0, Skipped: 0
#
# [INFO] --- maven-jar-plugin:X.X.X:jar ---
# [INFO] Building jar: target\ROOT.war
# [INFO] ------------------------------------------------------------------------
# [INFO] BUILD SUCCESS
# [INFO] ------------------------------------------------------------------------
# [INFO] Total time: 3:45 min
# [INFO] Finished at: 2026-03-10T10:30:00-06:00
# [INFO] ------------------------------------------------------------------------
```

**Tiempo estimado**: 3-10 minutos (primera vez)
- Descarga de dependencias: ~200 MB
- Compilación: ~1-2 minutos
- Tests: ~30 segundos

**⚠️ Si aparecen errores**:

**Error: "JAVA_HOME is not set"**
```powershell
# Configurar JAVA_HOME temporalmente
$env:JAVA_HOME = "C:\Program Files\Eclipse Adoptium\jdk-17.x.x-hotspot"
.\mvnw.cmd clean install
```

**Error: "mvnw.cmd is not recognized"**
```powershell
# Verificar que estás en la raíz del proyecto
pwd
# Si no, navegar:
cd C:\Users\TU_USUARIO\Desktop\HapiFhir-Springboot
```

**Error: Tests failing**
```powershell
# Omitir tests por ahora (no recomendado):
.\mvnw.cmd clean install -DskipTests
```

---

### 3.2. Verificar Build Exitoso

```powershell
# Verificar que se creó el archivo WAR
Test-Path target\ROOT.war
# Debe mostrar: True

# Ver tamaño del WAR
(Get-Item target\ROOT.war).Length / 1MB
# Debe mostrar: ~80-100 MB
```

---

## 4. CONFIGURAR FRONTEND (FLUTTER)

### 4.1. Instalar Dependencias de Flutter

**¿Qué hace este comando?**  
Descarga todas las librerías Dart/Flutter necesarias (http, provider, Material Design, etc.).

```powershell
# Navegar a la carpeta Flutter
cd flutter_frontend

# Instalar dependencias
flutter pub get

# Salida esperada:
# Resolving dependencies...
# Downloading packages...
#   + async 2.11.0
#   + collection 1.18.0
#   + flutter 0.0.0 from sdk flutter
#   + http 1.1.0
#   + intl 0.18.1
#   + provider 6.1.1
#   [... muchas más librerías ...]
# Changed 50 dependencies!
```

**Tiempo estimado**: 1-3 minutos
- Descarga de paquetes: ~50-100 MB

**⚠️ Si aparecen errores**:

**Error: "Flutter SDK not found"**
```powershell
# Verificar Flutter
flutter --version

# Si no funciona, agregar a PATH:
# C:\src\flutter\bin
```

**Error: "pubspec.yaml not found"**
```powershell
# Verificar que estás en flutter_frontend
pwd
# Debe mostrar: ...\HapiFhir-Springboot\flutter_frontend

# Si no, navegar:
cd C:\Users\TU_USUARIO\Desktop\HapiFhir-Springboot\flutter_frontend
```

---

### 4.2. Verificar Dependencias Instaladas

```powershell
# Verificar que se creó .dart_tool
Test-Path .dart_tool
# Debe mostrar: True

# Verificar que pubspec.lock existe
Test-Path pubspec.lock
# Debe mostrar: True

# Regresar a la raíz del proyecto
cd ..
```

---

## 5. CONFIGURAR BASE DE DATOS (DOCKER)

### 5.1. Verificar Docker Desktop Corriendo

```powershell
# Verificar que Docker está activo
docker ps

# Salida esperada: tabla vacía (sin errores)
# CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

**Si aparece error "Cannot connect to Docker daemon"**:
1. Abrir Docker Desktop manualmente
2. Esperar a que muestre "Docker Desktop is running"
3. Reintentar `docker ps`

---

### 5.2. Levantar PostgreSQL con Docker Compose

**¿Qué hace este comando?**  
Inicia un contenedor Docker con PostgreSQL 16 configurado para HAPI FHIR.

```powershell
# Asegúrate de estar en la raíz del proyecto
cd C:\Users\TU_USUARIO\Desktop\HapiFhir-Springboot

# Levantar Docker Compose en segundo plano
docker-compose up -d

# Salida esperada:
# Creating network "hapi-fhir-jpaserver-starter_default" with the default driver
# Creating volume "hapi-fhir-jpaserver-starter_postgres-data" with default driver
# Pulling postgres (postgres:16)...
# [... descarga de imagen ...]
# Creating hapi-fhir-jpaserver-starter_postgres_1 ... done
```

**Tiempo estimado**: 2-5 minutos (primera vez)
- Descarga de imagen PostgreSQL: ~100 MB

---

### 5.3. Verificar PostgreSQL Corriendo

```powershell
# Ver contenedores activos
docker ps

# Salida esperada:
# CONTAINER ID   IMAGE         COMMAND                  CREATED         STATUS         PORTS                    NAMES
# abc123def456   postgres:16   "docker-entrypoint.s…"   10 seconds ago  Up 8 seconds   0.0.0.0:5432->5432/tcp   hapi-fhir-jpaserver-starter_postgres_1
```

**Verificar detalles específicos**:
- ✅ STATUS: "Up X seconds/minutes"
- ✅ PORTS: "0.0.0.0:5432->5432/tcp"
- ✅ IMAGE: "postgres:16"

```powershell
# Ver logs de PostgreSQL (opcional)
docker logs hapi-fhir-jpaserver-starter_postgres_1

# Debe mostrar al final:
# ... database system is ready to accept connections
```

---

### 5.4. Verificar Conexión a Base de Datos (Opcional)

```powershell
# Conectar a PostgreSQL dentro del contenedor
docker exec -it hapi-fhir-jpaserver-starter_postgres_1 psql -U admin -d fhirdb

# Si funciona, verás:
# psql (16.x)
# Type "help" for help.
# fhirdb=#

# Listar tablas (debería estar vacía por ahora)
\dt

# Salir de PostgreSQL
\q
```

---

## 6. ACTUALIZAR IP DE RED (SOLO PARA MÓVIL)

**⚠️ IMPORTANTE**: Este paso es **SOLO necesario** si vas a usar la app en un **dispositivo Android/iOS físico**.

**Si solo usarás el navegador (web)**: ⏭️ Salta a la Sección 7

---

### 6.1. ¿Por Qué Actualizar la IP?

El frontend Flutter necesita saber la IP de tu laptop para conectarse al backend cuando ejecutas la app en un dispositivo móvil físico:

- **Web (navegador)**: Usa `localhost:8080` ✅ No requiere configuración
- **Móvil (dispositivo físico)**: Usa `192.168.X.X:8080` ⚠️ Requiere tu IP de red local

---

### 6.2. Obtener Tu IP de Red

```powershell
# Ver tu IP local
ipconfig | Select-String "IPv4"

# Salida esperada (busca la IP de tu red WiFi/Ethernet):
#    IPv4 Address. . . . . . . . . . . : 192.168.1.10
#    IPv4 Address. . . . . . . . . . . : 192.168.21.5  ← Esta es tu IP local
```

**Anota tu IP**: `192.168.X.X`

---

### 6.3. Ejecutar Script de Actualización

```powershell
# Navegar a carpeta Flutter
cd flutter_frontend

# Ejecutar script de actualización
.\update-ip.ps1

# Salida esperada:
# ===========================================
# 🔍 Buscando dirección IP de red local...
# ===========================================
# 
# ✅ IP encontrada: 192.168.21.5
# 
# ===========================================
# 📝 Actualizando configuración de API...
# ===========================================
# 
# Actualizando de 192.168.1.10 a 192.168.21.5...
# ✅ lib/config/api_config.dart actualizado
# ✅ lib/services/fhir_service.dart actualizado
# 
# ===========================================
# ✅ Configuración actualizada exitosamente
# ===========================================
```

---

### 6.4. Verificar Actualización (Opcional)

```powershell
# Ver el archivo de configuración
cat lib\config\api_config.dart | Select-String "192.168"

# Debe mostrar tu nueva IP:
#   static const String _mobileBaseUrl = 'http://192.168.21.5:8080';
```

```powershell
# Regresar a raíz del proyecto
cd ..
```

---

## 7. EJECUTAR EL SISTEMA COMPLETO

### 7.1. Abrir 3 Terminales PowerShell

**Terminal 1**: Backend (Spring Boot)  
**Terminal 2**: Frontend (Flutter Web)  
**Terminal 3**: Comandos adicionales / verificación

**En VS Code**:
1. Abrir VS Code: `code .` (desde la raíz del proyecto)
2. Abrir Terminal: `Ctrl + Ñ` o View → Terminal
3. Click en "+" para abrir más terminales

**O usar PowerShell nativo**:
1. Abrir 3 ventanas de PowerShell
2. En cada una: `cd C:\Users\TU_USUARIO\Desktop\HapiFhir-Springboot`

---

### 7.2. Terminal 1 - Iniciar Backend

```powershell
# En Terminal 1
cd C:\Users\TU_USUARIO\Desktop\HapiFhir-Springboot

# Iniciar backend con perfil Boot
.\mvnw.cmd spring-boot:run -Pboot

# Salida esperada (proceso largo):
# [INFO] Scanning for projects...
# [INFO] ------------------------------------------------------------------------
# [INFO] Building hapi-fhir-jpaserver-starter X.X.X
# [INFO] ------------------------------------------------------------------------
# [INFO] 
# [INFO] >>> spring-boot-maven-plugin:3.5.9:run (default-cli) @ hapi-fhir-jpaserver-starter >>>
# [INFO] 
# [... muchas líneas de inicialización ...]
#
#   .   ____          _            __ _ _
#  /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
# ( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
#  \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
#   '  |____| .__|_| |_|_| |_\__, | / / / /
#  =========|_|==============|___/=/_/_/_/
#  :: Spring Boot ::                (v3.5.9)
#
# 2026-03-10T10:45:00.123-06:00  INFO 12345 --- [main] ca.uhn.fhir.jpa.starter.Application : Starting Application...
# [... muchas líneas más ...]
#
# 2026-03-10T10:45:15.456-06:00  INFO 12345 --- [main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http)
# 2026-03-10T10:45:15.789-06:00  INFO 12345 --- [main] ca.uhn.fhir.jpa.starter.Application : Started Application in 15.666 seconds
```

**⚠️ ESPERAR A VER**: `Started Application in X seconds`

**Tiempo estimado**: 15-30 segundos

**Indicadores de éxito**:
- ✅ "Tomcat started on port(s): 8080 (http)"
- ✅ "Started Application in X seconds"
- ✅ No aparecen líneas con "ERROR" o "FATAL"

**⚠️ Si aparecen errores**:

**Error: "Port 8080 already in use"**
```powershell
# Matar proceso en puerto 8080
Get-Process -Id (Get-NetTCPConnection -LocalPort 8080).OwningProcess | Stop-Process -Force

# Reintentar
.\mvnw.cmd spring-boot:run -Pboot
```

**Error: "Could not connect to database"**
```powershell
# Verificar que Docker esté corriendo
docker ps

# Si no aparece PostgreSQL:
docker-compose up -d

# Esperar 10 segundos y reintentar
.\mvnw.cmd spring-boot:run -Pboot
```

---

### 7.3. Verificar Backend Funcionando

**Mientras el backend está corriendo (no cerrar Terminal 1)**:

```powershell
# En Terminal 3 (o nueva terminal)
# Probar endpoint de salud
curl http://localhost:8080/fhir/metadata

# O abrir en navegador:
# http://localhost:8080/fhir/metadata
# 
# Debe mostrar JSON con información del servidor FHIR
```

---

### 7.4. Terminal 2 - Iniciar Frontend

```powershell
# En Terminal 2
cd C:\Users\TU_USUARIO\Desktop\HapiFhir-Springboot\flutter_frontend

# Iniciar Flutter en Chrome
flutter run -d chrome

# Salida esperada:
# Launching lib\main.dart on Chrome in debug mode...
# Waiting for connection from debug service on Chrome...
# [... compilación ...]
# Syncing files to device Chrome...                          X,XXX ms
# 
# Flutter run key commands.
# r Hot reload. 🔥🔥🔥
# R Hot restart.
# h List all available interactive commands.
# d Detach (terminate "flutter run" but leave application running).
# c Clear the screen
# q Quit (terminate the application on the device).
# 
# 💪 Running with sound null safety 💪
# 
# An Observatory debugger and profiler on Chrome is available at: http://127.0.0.1:XXXXX/
# The Flutter DevTools debugger and profiler on Chrome is available at: http://127.0.0.1:XXXXX/
# 
# Application finished.
```

**Se abrirá automáticamente un navegador Chrome** con la aplicación.

**Tiempo estimado**: 30-60 segundos (primera vez)

**⚠️ Si aparecen errores**:

**Error: "No devices found"**
```powershell
# Ver dispositivos disponibles
flutter devices

# Si no aparece Chrome:
# Instalar Google Chrome
# Reintentar: flutter run -d chrome
```

**Error: "build failed"**
```powershell
# Limpiar y reconstruir
flutter clean
flutter pub get
flutter run -d chrome
```

---

## 8. VERIFICAR FUNCIONAMIENTO

### 8.1. Verificar Backend (http://localhost:8080)

**Abrir navegador** y probar estos endpoints:

#### 8.1.1. Metadata FHIR
```
URL: http://localhost:8080/fhir/metadata
Método: GET
```

**Resultado esperado**: JSON con metadatos del servidor FHIR.

---

#### 8.1.2. Login (Autenticación)
```
URL: http://localhost:8080/api/auth/login
Método: POST
Headers: Content-Type: application/json
Body:
{
  "username": "admin",
  "password": "admin123"
}
```

**Resultado esperado**:
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "username": "admin",
  "role": "ADMIN"
}
```

**Probar con cURL** (en Terminal 3):
```powershell
curl -X POST http://localhost:8080/api/auth/login `
  -H "Content-Type: application/json" `
  -d '{\"username\":\"admin\",\"password\":\"admin123\"}'
```

---

#### 8.1.3. Listar Usuarios (Requiere Token)
```
URL: http://localhost:8080/api/users
Método: GET
Headers: Authorization: Bearer <TOKEN_DEL_PASO_ANTERIOR>
```

**Resultado esperado**:
```json
[
  {
    "id": 1,
    "username": "admin",
    "role": "ADMIN",
    "active": true
  }
]
```

---

### 8.2. Verificar Frontend (Aplicación Flutter)

**La aplicación debe estar abierta en Chrome**.

#### 8.2.1. Pantalla de Login

**Verificar elementos visuales**:
- ✅ Gradiente morado → azul de fondo
- ✅ Logo/título "Hospital FHIR System"
- ✅ Campo "Usuario"
- ✅ Campo "Contraseña"
- ✅ Botón "Iniciar Sesión"

**Probar animaciones**:
- Los elementos deben aparecer con fade + slide desde abajo
- Duración: ~1.2 segundos

---

#### 8.2.2. Login Exitoso

**Credenciales**:
```
Usuario: admin
Contraseña: admin123
```

**Click en "Iniciar Sesión"**

**Resultado esperado**:
1. Botón muestra "Cargando..." con spinner
2. Transición a pantalla Home (~300ms)
3. **NO** debe aparecer mensaje de error

---

#### 8.2.3. Pantalla Home

**Verificar elementos**:
- ✅ AppBar con título "Sistema Hospitalario"
- ✅ Botón de logout (icono de salida)
- ✅ Tarjetas con animación de escala:
  - "Pacientes" (icono de persona)
  - "Citas" (icono de calendario)
  - "Especialistas" (icono de estetoscopio)
  - "Configuración" (icono de engranaje)

**Probar animaciones**:
- Las tarjetas aparecen con efecto de escala escalonado
- Duración total: ~1.5 segundos

---

#### 8.2.4. Pantalla de Pacientes

**Click en tarjeta "Pacientes"**

**Resultado esperado**:
1. Transición a pantalla Patients
2. Se muestra lista de pacientes o mensaje "Cargando..."
3. Cada paciente muestra:
   - Nombre completo
   - Género
   - Fecha de nacimiento
   - ID del paciente

**Si aparece lista vacía**: Es normal si la base de datos está vacía.

---

#### 8.2.5. Pantalla de Citas

**Regresar a Home** → **Click en "Citas"**

**Resultado esperado**:
1. Transición a pantalla Appointments
2. Se muestra lista de citas o mensaje "Cargando..."
3. Cada cita muestra:
   - Paciente
   - Especialista
   - Fecha y hora
   - Estado

---

#### 8.2.6. Logout

**Click en botón de logout** (icono de salida en AppBar)

**Resultado esperado**:
1. Transición a pantalla Login
2. Campos vacíos
3. Token eliminado (no puede volver atrás con navegador)

---

### 8.3. Verificar Base de Datos

```powershell
# En Terminal 3
# Conectar a PostgreSQL
docker exec -it hapi-fhir-jpaserver-starter_postgres_1 psql -U admin -d fhirdb

# Listar tablas
\dt

# Debe mostrar múltiples tablas de HAPI FHIR:
# hfj_resource
# hfj_res_ver
# hfj_spidx_string
# hfj_spidx_token
# [... muchas más tablas ...]
# users (tabla de autenticación personalizada)

# Ver usuarios
SELECT * FROM users;

# Debe mostrar al menos el usuario admin

# Salir
\q
```

---

## 9. EJECUTAR TESTS

### 9.1. Tests del Backend

```powershell
# En Terminal 3 (o nueva terminal)
cd C:\Users\TU_USUARIO\Desktop\HapiFhir-Springboot

# Ejecutar TODOS los tests
.\mvnw.cmd test

# O ejecutar solo tests de autenticación
.\mvnw.cmd test -Dtest="Auth*,User*"

# Salida esperada:
# [INFO] -------------------------------------------------------
# [INFO]  T E S T S
# [INFO] -------------------------------------------------------
# [INFO] Running ca.uhn.fhir.jpa.starter.auth.AuthControllerTest
# [INFO] Tests run: 12, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 2.345 s
# [INFO] Running ca.uhn.fhir.jpa.starter.auth.UserControllerTest
# [INFO] Tests run: 11, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 1.234 s
# [INFO] 
# [INFO] Results:
# [INFO] 
# [INFO] Tests run: 23, Failures: 0, Errors: 0, Skipped: 0
# [INFO]
# [INFO] ------------------------------------------------------------------------
# [INFO] BUILD SUCCESS
# [INFO] ------------------------------------------------------------------------
```

**Indicadores de éxito**:
- ✅ Tests run: 23
- ✅ Failures: 0
- ✅ Errors: 0
- ✅ BUILD SUCCESS

**Tiempo estimado**: 30-60 segundos

---

### 9.2. Tests del Frontend

```powershell
# Navegar a carpeta Flutter
cd flutter_frontend

# Ejecutar tests
flutter test

# Salida esperada:
# 00:01 +0: loading C:\...\flutter_frontend\test\services\auth_service_test.dart
# 00:02 +12: (tearDownAll)
# 00:02 +12: All tests passed!
# 00:03 +0: loading C:\...\flutter_frontend\test\services\fhir_service_test.dart
# 00:04 +11: (tearDownAll)
# 00:04 +11: All tests passed!
# 00:05 +0: loading C:\...\flutter_frontend\test\widget_test.dart
# 00:06 +2: (tearDownAll)
# 00:06 +2: All tests passed!
# 
# 00:06 +25: All tests passed!
```

**Indicadores de éxito**:
- ✅ +25: All tests passed!
- ✅ No aparecen líneas con "FAILED" o "ERROR"

**Tiempo estimado**: 10-20 segundos

---

### 9.3. Resumen de Tests

**Backend**: 23 tests
- AuthControllerTest: 12 tests
  - Login exitoso
  - Login con credenciales incorrectas
  - Signup exitoso
  - Signup con usuario duplicado
  - Validar token válido
  - Validar token inválido
  - Crear admin
  - etc.

- UserControllerTest: 11 tests
  - Obtener todos los usuarios
  - Obtener usuario por ID
  - Eliminar usuario
  - Toggle user status
  - Acceso sin permisos
  - etc.

**Frontend**: 25 tests
- auth_service_test: 12 tests
  - Login exitoso
  - Login fallido
  - Signup exitoso
  - Validar token
  - etc.

- fhir_service_test: 11 tests
  - Obtener pacientes
  - Obtener citas
  - Manejo de errores
  - etc.

- widget_test: 2 tests
  - Widgets básicos

**Total**: 48 tests ✅

---

## 10. SOLUCIÓN DE PROBLEMAS

### 10.1. Backend No Inicia

**Problema**: Error "Port 8080 already in use"

**Solución**:
```powershell
# Encontrar proceso usando puerto 8080
Get-Process -Id (Get-NetTCPConnection -LocalPort 8080).OwningProcess

# Matar proceso
Get-Process -Id (Get-NetTCPConnection -LocalPort 8080).OwningProcess | Stop-Process -Force

# O cambiar puerto en application.yaml:
# server:
#   port: 8081
```

---

**Problema**: "Could not connect to database"

**Solución**:
```powershell
# Verificar Docker corriendo
docker ps

# Si PostgreSQL no aparece:
docker-compose down
docker-compose up -d

# Esperar 10 segundos
Start-Sleep -Seconds 10

# Verificar logs
docker logs hapi-fhir-jpaserver-starter_postgres_1

# Reiniciar backend
.\mvnw.cmd spring-boot:run -Pboot
```

---

**Problema**: Tests fallan

**Solución**:
```powershell
# Limpiar y recompilar
.\mvnw.cmd clean install -DskipTests

# Ejecutar tests individualmente
.\mvnw.cmd test -Dtest=AuthControllerTest

# Si persiste, verificar logs:
cat target\surefire-reports\*.txt
```

---

### 10.2. Frontend No Inicia

**Problema**: "No devices found"

**Solución**:
```powershell
# Ver dispositivos disponibles
flutter devices

# Si Chrome no aparece:
# 1. Instalar Google Chrome
# 2. Reiniciar PowerShell
# 3. Ejecutar: flutter doctor
# 4. Reintentar: flutter run -d chrome
```

---

**Problema**: Error de compilación

**Solución**:
```powershell
cd flutter_frontend

# Limpiar caché
flutter clean

# Reinstalar dependencias
flutter pub get

# Reintentar
flutter run -d chrome
```

---

**Problema**: "Failed to connect to backend"

**Solución**:
```powershell
# Verificar backend corriendo
curl http://localhost:8080/fhir/metadata

# Si no responde:
# 1. Ir a Terminal 1 (backend)
# 2. Verificar que muestra "Started Application"
# 3. Si no, revisar Sección 10.1
```

---

### 10.3. Docker No Funciona

**Problema**: "Cannot connect to Docker daemon"

**Solución**:
1. Abrir Docker Desktop manualmente
2. Esperar a que muestre "Docker Desktop is running"
3. Reintentar: `docker ps`

---

**Problema**: PostgreSQL no se levanta

**Solución**:
```powershell
# Ver logs de error
docker logs hapi-fhir-jpaserver-starter_postgres_1

# Eliminar contenedor y volúmenes
docker-compose down -v

# Recrear
docker-compose up -d

# Esperar 10 segundos
Start-Sleep -Seconds 10

# Verificar
docker ps
```

---

### 10.4. Maven Wrapper No Funciona

**Problema**: "mvnw.cmd is not recognized"

**Solución**:
```powershell
# Verificar que existe
Test-Path mvnw.cmd

# Si muestra False:
# Re-clonar repositorio
cd ..
Remove-Item -Recurse -Force HapiFhir-Springboot
git clone https://github.com/UlisesBGZ/HapiFhir-Springboot.git
```

---

**Problema**: "maven-wrapper.jar not found"

**Solución**:
```powershell
# Verificar que existe
Test-Path .mvn\wrapper\maven-wrapper.jar

# Ver tamaño
(Get-Item .mvn\wrapper\maven-wrapper.jar).Length / 1KB

# Si es 0 KB o no existe:
# Re-clonar repositorio (el archivo está en GitHub)
```

---

### 10.5. IP de Red No Funciona en Móvil

**Problema**: App móvil no se conecta al backend

**Solución**:
```powershell
# Verificar IP actual
ipconfig | Select-String "IPv4"

# Actualizar IP
cd flutter_frontend
.\update-ip.ps1

# Verificar actualización
cat lib\config\api_config.dart | Select-String "192.168"

# Rebuild app
flutter clean
flutter pub get
flutter run
```

---

**Problema**: "Connection refused" en móvil

**Solución**:
1. Verificar que laptop y móvil están en **la misma red WiFi**
2. Desactivar **firewall de Windows temporalmente**:
   ```powershell
   # Abrir PowerShell como Administrador
   # Agregar regla para puerto 8080
   New-NetFirewallRule -DisplayName "HAPI FHIR Backend" -Direction Inbound -LocalPort 8080 -Protocol TCP -Action Allow
   ```
3. Verificar que backend está escuchando en todas las interfaces:
   ```yaml
   # En application.yaml:
   server:
     address: 0.0.0.0  # Escuchar en todas las interfaces
   ```

---

## 📊 CHECKLIST FINAL DE VERIFICACIÓN

Antes de considerar el setup completo, verifica TODOS estos puntos:

### Prerrequisitos Instalados
- [ ] Java 17+ (`java -version` funciona)
- [ ] Flutter 3.38+ (`flutter --version` funciona)
- [ ] Docker 20+ (`docker --version` funciona)
- [ ] Git (`git --version` funciona)

### Repositorio Clonado
- [ ] Repositorio clonado desde GitHub
- [ ] Maven wrapper existe (`.mvn\wrapper\maven-wrapper.jar` = 63 KB)
- [ ] Flutter pubspec existe (`flutter_frontend\pubspec.yaml`)
- [ ] Docker compose existe (`docker-compose.yml`)

### Dependencias Instaladas
- [ ] Backend compilado (`.\mvnw.cmd clean install` exitoso)
- [ ] Archivo WAR creado (`target\ROOT.war` existe)
- [ ] Frontend configurado (`flutter pub get` exitoso)
- [ ] Carpeta `.dart_tool` creada

### Servicios Corriendo
- [ ] Docker Desktop activo
- [ ] PostgreSQL corriendo (`docker ps` muestra postgres:16)
- [ ] Backend corriendo (Terminal 1: "Started Application")
- [ ] Frontend corriendo (Terminal 2: navegador abierto)

### Funcionalidad Verificada
- [ ] Metadata FHIR accesible (`http://localhost:8080/fhir/metadata`)
- [ ] Login funciona (admin / admin123)
- [ ] Pantalla Home carga correctamente
- [ ] Pantalla Pacientes accesible
- [ ] Pantalla Citas accesible
- [ ] Logout funciona

### Tests Pasando
- [ ] Backend tests: 23/23 ✅
- [ ] Frontend tests: 25/25 ✅
- [ ] Total: 48/48 ✅

### Configuración Específica (Si aplica)
- [ ] IP actualizada para móvil (`.\update-ip.ps1` ejecutado)
- [ ] App móvil se conecta al backend
- [ ] Firewall configurado para puerto 8080

---

## 🎉 ¡SETUP COMPLETO!

Si TODOS los checkboxes anteriores están marcados: **✅ El proyecto está completamente configurado y funcional**.

---

## 📚 DOCUMENTACIÓN ADICIONAL

Para más información, consulta estos archivos:

- **[CONTEXTO_PARA_NUEVA_SESION.md](CONTEXTO_PARA_NUEVA_SESION.md)**: Contexto técnico completo del proyecto
- **[DESARROLLO_COMPLETO.md](DESARROLLO_COMPLETO.md)**: Historia detallada del desarrollo
- **[TESTING.md](TESTING.md)**: Guía completa de testing
- **[AUTHENTICATION.md](AUTHENTICATION.md)**: Detalles del sistema de autenticación
- **[GUIA_GITHUB.md](GUIA_GITHUB.md)**: Cómo sincronizar cambios con GitHub
- **[BITACORA_METODOLOGIA.md](BITACORA_METODOLOGIA.md)**: Bitácora académica del proyecto

**Todos los archivos de documentación**: [LEEME_DOCUMENTACION.md](LEEME_DOCUMENTACION.md)

---

## 🆘 SOPORTE

Si encuentras problemas no cubiertos en esta guía:

1. **Revisar [Sección 10](#10-solución-de-problemas)**: Solución de Problemas
2. **Consultar [DESARROLLO_COMPLETO.md](DESARROLLO_COMPLETO.md)**: Sección "Troubleshooting"
3. **Verificar logs**:
   - Backend: En la Terminal 1 (stdout)
   - PostgreSQL: `docker logs hapi-fhir-jpaserver-starter_postgres_1`
   - Frontend: En la Terminal 2 (stdout)

---

## 📝 NOTAS FINALES

### Comandos Rápidos de Referencia

**Iniciar Sistema**:
```powershell
# Terminal 1: Backend
.\mvnw.cmd spring-boot:run -Pboot

# Terminal 2: Frontend
cd flutter_frontend
flutter run -d chrome

# Si Docker no está corriendo:
docker-compose up -d
```

**Detener Sistema**:
```powershell
# Terminal 1: Ctrl + C (backend)
# Terminal 2: q (Flutter) o Ctrl + C
# Docker:
docker-compose down
```

**Limpiar y Reconstruir**:
```powershell
# Backend
.\mvnw.cmd clean install

# Frontend
cd flutter_frontend
flutter clean
flutter pub get
```

**Ver Logs**:
```powershell
# PostgreSQL
docker logs hapi-fhir-jpaserver-starter_postgres_1

# Seguir logs en tiempo real
docker logs -f hapi-fhir-jpaserver-starter_postgres_1
```

---

### Credenciales de Desarrollo

**Usuario Admin**:
```
Username: admin
Password: admin123
```

**Base de Datos PostgreSQL**:
```
Host: localhost
Port: 5432
Database: fhirdb
Username: admin
Password: admin
```

**JWT Secret** (hardcoded en desarrollo):
```
Ver: src/main/resources/application.yaml
Clave: jwt.secret
⚠️ Cambiar en producción
```

---

### URLs de Acceso

**Backend**:
- Base: `http://localhost:8080`
- FHIR Metadata: `http://localhost:8080/fhir/metadata`
- Login: `http://localhost:8080/api/auth/login`
- Users: `http://localhost:8080/api/users`
- Pacientes FHIR: `http://localhost:8080/fhir/Patient?_count=10`

**Frontend**:
- Web: `http://localhost:XXXXX` (puerto asignado por Flutter)

**Base de Datos**:
- PostgreSQL: `localhost:5432`

---

### Próximos Pasos Recomendados

1. **Explorar la API**:
   - Usar Postman/Insomnia para probar endpoints
   - Ver ejemplos en AUTHENTICATION.md

2. **Personalizar Configuración**:
   - Cambiar puerto del backend (application.yaml)
   - Agregar más usuarios admin
   - Configurar CORS específico

3. **Desarrollo Continuo**:
   - Sincronizar cambios con `git pull`/`git push`
   - Ejecutar tests antes de commit
   - Ver GUIA_GITHUB.md para workflows

4. **Despliegue Futuro**:
   - Considerar HTTPS
   - Configurar variables de entorno (.env)
   - Setup de CI/CD con GitHub Actions

---

## 🤖 DOCUMENTACIÓN PARA NUEVA IA (GitHub Copilot)

### ¿Cómo dar contexto a una nueva IA en la nueva laptop?

Cuando abras el proyecto en VS Code en la nueva laptop, la IA (GitHub Copilot) necesitará entender el proyecto. Aquí está el orden recomendado de archivos para que la IA lea:

### **Opción 1: Inicio Rápido (5 minutos)** ⚡ RECOMENDADO

```
📄 Archivos a leer:
1. .github/copilot-instructions.md  ← Se lee AUTOMÁTICAMENTE por Copilot
2. PROMPT_PARA_NUEVA_IA.md          ← Copiar y pegar en el chat
```

**Enlaces directos**:
- **[.github/copilot-instructions.md](.github/copilot-instructions.md)**
- **[PROMPT_PARA_NUEVA_IA.md](PROMPT_PARA_NUEVA_IA.md)**

**Cómo usarlo**:
1. Abrir VS Code en el proyecto
2. GitHub Copilot lee automáticamente `.github/copilot-instructions.md`
3. Abrir `PROMPT_PARA_NUEVA_IA.md`
4. Copiar TODO el contenido
5. Pegar en el chat de GitHub Copilot
6. La IA ya tiene contexto completo

**Ventajas**:
- ✅ 5 minutos de lectura
- ✅ Contexto esencial inmediato
- ✅ Listo para trabajar

---

### **Opción 2: Contexto Completo (30-45 minutos)** 📚

```
📄 Archivos a leer EN ORDEN:
1. LEEME_DOCUMENTACION.md           ← Índice de toda la documentación (5 min)
2. CONTEXTO_PARA_NUEVA_SESION.md    ← Contexto técnico completo (15 min)
3. DESARROLLO_COMPLETO.md           ← Historia del desarrollo (20 min)
```

**Enlaces directos**:
- **[LEEME_DOCUMENTACION.md](LEEME_DOCUMENTACION.md)**
- **[CONTEXTO_PARA_NUEVA_SESION.md](CONTEXTO_PARA_NUEVA_SESION.md)**
- **[DESARROLLO_COMPLETO.md](DESARROLLO_COMPLETO.md)**

**Cómo usarlo**:
```
En el chat de GitHub Copilot, escribe:

"Lee estos archivos y dame un resumen del proyecto:
1. LEEME_DOCUMENTACION.md
2. CONTEXTO_PARA_NUEVA_SESION.md
3. DESARROLLO_COMPLETO.md

Después explícame la arquitectura del sistema."
```

**Ventajas**:
- ✅ Comprensión profunda del proyecto
- ✅ Conoce el historial de decisiones técnicas
- ✅ Entiende problemas resueltos anteriormente

---

### **Opción 3: Por Tema Específico** 🎯

Si la IA necesita ayuda con algo específico, indícale que lea:

#### **Para Setup/Configuración**:
- **[CHECKLIST_TRANSFERENCIA.md](CHECKLIST_TRANSFERENCIA.md)** ← Pasos de configuración
- **[SETUP_NUEVA_LAPTOP.md](SETUP_NUEVA_LAPTOP.md)** ← Esta guía completa

#### **Para Entender Autenticación JWT**:
- **[AUTHENTICATION.md](AUTHENTICATION.md)**
- **[AUTH_INTEGRATION_GUIDE.md](AUTH_INTEGRATION_GUIDE.md)**
- Ver: [src/main/java/ca/uhn/fhir/jpa/starter/auth/](src/main/java/ca/uhn/fhir/jpa/starter/auth/)

#### **Para Ejecutar/Crear Tests**:
- **[TESTING.md](TESTING.md)**
- Ver: [src/test/java/ca/uhn/fhir/jpa/starter/auth/](src/test/java/ca/uhn/fhir/jpa/starter/auth/)
- Ver: [flutter_frontend/test/](flutter_frontend/test/)

#### **Para Usar Git/GitHub**:
- **[GUIA_GITHUB.md](GUIA_GITHUB.md)**
- Ver: [.gitignore](.gitignore) (entiende qué se sube y qué no)

#### **Para Entender Frontend Flutter**:
- Ver: [flutter_frontend/lib/config/api_config.dart](flutter_frontend/lib/config/api_config.dart) (IP dinámica)
- Ver: [flutter_frontend/lib/services/](flutter_frontend/lib/services/) (auth_service, fhir_service)
- Ver: [flutter_frontend/lib/screens/](flutter_frontend/lib/screens/) (UI con animaciones)

---

### **Prompt Recomendado para la Nueva IA**

Abre GitHub Copilot Chat y escribe:

```
Hola, soy nuevo en este proyecto. Necesito que me ayudes a entenderlo.

Por favor lee estos archivos en orden:
1. .github/copilot-instructions.md
2. PROMPT_PARA_NUEVA_IA.md
3. CONTEXTO_PARA_NUEVA_SESION.md

Después responde:
1. ¿Cuál es el stack tecnológico del proyecto?
2. ¿Cuáles son los endpoints principales?
3. ¿Cómo está estructurado el sistema de autenticación?
4. ¿Qué comandos necesito para ejecutar el proyecto?
5. ¿Dónde están los tests y cómo ejecutarlos?

También necesito que estés atento para ayudarme con:
- Configuración de la nueva laptop
- Problemas que puedan surgir
- Explicación de código existente
- Mejores prácticas del proyecto
```

---

### **Lista Completa de Archivos de Documentación**

```
📚 Documentación del Proyecto (15 archivos, ~250 KB):

ESENCIALES (Leer primero):
```
  - **[.github/copilot-instructions.md](.github/copilot-instructions.md)** (5 KB) - Auto-leído por Copilot
  - **[PROMPT_PARA_NUEVA_IA.md](PROMPT_PARA_NUEVA_IA.md)** (9 KB) - Prompt listo para usar
  - **[SETUP_NUEVA_LAPTOP.md](SETUP_NUEVA_LAPTOP.md)** (50 KB) - Esta guía completa
  - **[CONTEXTO_PARA_NUEVA_SESION.md](CONTEXTO_PARA_NUEVA_SESION.md)** (29 KB) - Contexto técnico
```

REFERENCIA RÁPIDA:
```
  - **[LEEME_DOCUMENTACION.md](LEEME_DOCUMENTACION.md)** (6 KB) - Índice de documentos
  - **[README.md](README.md)** (29 KB) - README principal
  - **[CHECKLIST_TRANSFERENCIA.md](CHECKLIST_TRANSFERENCIA.md)** (10 KB) - Checklist de setup
```

DESARROLLO E HISTORIA:
```
  - **[DESARROLLO_COMPLETO.md](DESARROLLO_COMPLETO.md)** (57 KB) - Historia del desarrollo
  - **[BITACORA_METODOLOGIA.md](BITACORA_METODOLOGIA.md)** (60 KB) - Bitácora académica
  - **[README_SISTEMA_COMPLETO.md](README_SISTEMA_COMPLETO.md)** (16 KB) - Sistema completo
```

TÉCNICA ESPECÍFICA:
```
  - **[AUTHENTICATION.md](AUTHENTICATION.md)** (8 KB) - Sistema de autenticación
  - **[AUTH_INTEGRATION_GUIDE.md](AUTH_INTEGRATION_GUIDE.md)** (12 KB) - Guía de integración auth
  - **[TESTING.md](TESTING.md)** (10 KB) - Guía de testing
  - **[SERVIDOR_CONFIGURADO.md](SERVIDOR_CONFIGURADO.md)** (12 KB) - Configuración del servidor
```

GIT Y ENTORNO:
```
  - **[GUIA_GITHUB.md](GUIA_GITHUB.md)** (13 KB) - Git/GitHub workflows
  - **[GUIA_TRANSFERIR_VSCODE.md](GUIA_TRANSFERIR_VSCODE.md)** (12 KB) - Configurar VS Code
```

REPOSITORIO:
```
  - **[AGENTS.md](AGENTS.md)** (3 KB) - Guías para repository
```

**Total**: ~250 KB de documentación estructurada

---

### **Comando para VS Code**

Si quieres abrir el proyecto en VS Code directamente:

```powershell
# Desde la raíz del proyecto
code .
```

Esto abrirá VS Code y GitHub Copilot leerá automáticamente `.github/copilot-instructions.md`.

---

### **Tip Pro**: Configurar GitHub Copilot

1. **Instalar extensión**: GitHub Copilot + GitHub Copilot Chat
2. **Activar en el proyecto**: El archivo `.github/copilot-instructions.md` se lee automáticamente
3. **Usar chat**: `Ctrl + Shift + I` abre GitHub Copilot Chat
4. **Preguntar cualquier cosa**: La IA ya conoce el contexto del proyecto

---

### **Verificación de Contexto de IA**

Para verificar que la IA entendió el proyecto, pregúntale:

```
En GitHub Copilot Chat:

"¿Cuál es el puerto del backend?"
Respuesta esperada: 8080

"¿Cuáles son las credenciales admin?"
Respuesta esperada: admin / admin123

"¿Cuántos tests tiene el proyecto?"
Respuesta esperada: 48 (23 backend + 25 frontend)

"¿Qué base de datos usamos?"
Respuesta esperada: PostgreSQL 16 en Docker

"¿Cómo actualizo la IP para móvil?"
Respuesta esperada: .\update-ip.ps1 en flutter_frontend/
```

Si responde correctamente, la IA tiene el contexto completo. ✅

---

## 📝 RESUMEN PARA NUEVA IA

### Lo Más Importante que la IA Debe Saber:

1. **Stack**: Spring Boot 3.5.9 + HAPI FHIR 8.6.1 + Flutter 3.38.7 + PostgreSQL 16
2. **Autenticación**: JWT personalizada (no SMART on FHIR)
3. **Tests**: 48 tests (todos deben pasar)
4. **Maven Wrapper**: Reparado y funcional (61.5 KB)
5. **IP Dinámica**: Script `update-ip.ps1` para móvil
6. **Comandos Clave**:
   - Backend: `.\mvnw.cmd spring-boot:run -Pboot`
   - Frontend: `flutter run -d chrome`
   - Docker: `docker-compose up -d`
   - Tests: `.\mvnw.cmd test` y `flutter test`

---

**Autor**: Sistema HAPI FHIR con Autenticación JWT  
**Última Actualización**: 10 de Marzo, 2026  
**Versión**: 1.0  
**Repositorio**: https://github.com/UlisesBGZ/HapiFhir-Springboot

---

*Esta guía cubre TODOS los pasos necesarios para configurar y ejecutar el proyecto en una nueva laptop sin omitir detalles. Si encuentras algún paso poco claro o faltante, consulta DESARROLLO_COMPLETO.md o abre un issue en GitHub.*
