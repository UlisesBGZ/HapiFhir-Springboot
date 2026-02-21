# 🏥 Sistema Hospitalario Completo - HAPI FHIR + Flutter

## 🎯 **Sistema Integrado de Información Hospitalaria**

Solución completa con:
- ✅ **Backend:** Spring Boot + HAPI FHIR Server (HL7 FHIR R4)
- ✅ **Base de Datos:** PostgreSQL 16
- ✅ **Autenticación:** JWT + Spring Security
- ✅ **Frontend:** Flutter (iOS/Android)

---

## 🚀 **Inicio Rápido (5 Minutos)**

### **Opción 1: Script Automatizado (Windows)**

```powershell
# Ejecuta este script y todo se configurará automáticamente
.\start-system.bat
```

### **Opción 2: Manual**

```powershell
# 1. Iniciar PostgreSQL
docker start hapi-fhir-postgres

# 2. Compilar backend
.\mvnw.cmd clean package -DskipTests

# 3. Iniciar servidor
java -jar target/ROOT.war

# 4. En otra terminal, iniciar Flutter
cd flutter_frontend
flutter pub get
flutter run
```

---

## 📱 **Credenciales de Acceso**

**Usuario Administrador (creado automáticamente):**
```
Username: admin
Password: admin123
```

---

## ✨ **Características Implementadas**

### **Backend**
- ✅ Servidor HAPI FHIR R4 completo
- ✅ Persistencia en PostgreSQL
- ✅ Sistema de autenticación con JWT
- ✅ Roles y permisos (Admin/User/Doctor/Nurse)
- ✅ API REST para autenticación
- ✅ CORS configurado para Flutter
- ✅ Inicialización automática de admin
- ✅ 147 resource providers FHIR

### **Frontend (Flutter)**
- ✅ Pantalla de Login con validación
- ✅ Registro de usuarios
- ✅ Creación de administradores
- ✅ Gestión de sesión persistente
- ✅ Home personalizado por rol
- ✅ Logout
- ✅ Manejo de errores
- ✅ UI Material Design 3

---

## 📊 **Endpoints de API**

### **Autenticación** (`/api/auth`)

| Endpoint | Método | Descripción | Auth |
|----------|--------|-------------|------|
| `/api/auth/login` | POST | Iniciar sesión | No |
| `/api/auth/signup` | POST | Crear usuario | No |
| `/api/auth/create-admin` | POST | Crear admin | No |
| `/api/auth/check` | GET | Verificar token | Sí |

### **FHIR API** (`/fhir`)

| Endpoint | Método | Descripción |
|----------|--------|-------------|
| `/fhir/metadata` | GET | CapabilityStatement |
| `/fhir/Patient` | GET, POST, PUT, DELETE | Pacientes |
| `/fhir/Observation` | GET, POST | Observaciones |
| `/fhir/Practitioner` | GET, POST | Profesionales |
| `/fhir/Appointment` | GET, POST | Citas |

---

## 📁 **Estructura del Proyecto**

```
hapi-fhir-jpaserver-starter/
├── src/main/java/ca/uhn/fhir/jpa/starter/
│   ├── auth/                          # 🔐 Sistema de autenticación
│   │   ├── config/
│   │   │   └── DataInitializer.java   # Crea admin al iniciar
│   │   ├── controller/
│   │   │   └── AuthController.java    # API REST de auth
│   │   ├── dto/
│   │   │   ├── LoginRequest.java
│   │   │   ├── SignupRequest.java
│   │   │   └── JwtResponse.java
│   │   ├── model/
│   │   │   ├── User.java              # Entidad de usuario
│   │   │   └── Role.java              # Enum de roles
│   │   ├── repository/
│   │   │   └── UserRepository.java    # JPA Repository
│   │   ├── security/
│   │   │   ├── SecurityConfig.java    # Spring Security
│   │   │   ├── JwtTokenProvider.java  # Generador de JWT
│   │   │   ├── JwtAuthenticationFilter.java
│   │   │   └── CustomUserDetailsService.java
│   │   └── service/
│   │       └── UserService.java       # Lógica de negocio
│   └── Application.java               # Main class
│
├── flutter_frontend/                  # 📱 App móvil Flutter
│   ├── lib/
│   │   ├── config/
│   │   │   └── api_config.dart        # Configuración API
│   │   ├── models/
│   │   │   ├── user.dart
│   │   │   └── auth_models.dart
│   │   ├── providers/
│   │   │   └── auth_provider.dart     # State management
│   │   ├── screens/
│   │   │   ├── login_screen.dart
│   │   │   ├── signup_screen.dart
│   │   │   └── home_screen.dart
│   │   ├── services/
│   │   │   └── auth_service.dart
│   │   └── main.dart
│   ├── pubspec.yaml
│   └── README.md                      # Docs de Flutter
│
├── pom.xml                            # Dependencias Maven
├── docker-compose.yml                 # PostgreSQL + HAPI
├── start-system.bat                   # 🚀 Script de inicio
├── SERVIDOR_CONFIGURADO.md            # Estado del servidor
├── AUTH_INTEGRATION_GUIDE.md          # 📖 Guía completa
└── README_SISTEMA_COMPLETO.md         # Este archivo
```

---

## 🔧 **Tecnologías Utilizadas**

### **Backend**
- Java 17
- Spring Boot 3.5.9
- HAPI FHIR 8.6.1
- Spring Security 6.x
- JWT (JJWT 0.12.6)
- PostgreSQL 16
- Hibernate/JPA
- Maven

### **Frontend**
- Flutter 3.x
- Dart 3.x
- Provider (State Management)
- HTTP package
- SharedPreferences
- Material Design 3

---

## 📖 **Documentación Detallada**

1. **[SERVIDOR_CONFIGURADO.md](SERVIDOR_CONFIGURADO.md)**
   - Estado del servidor HAPI FHIR
   - URLs y endpoints
   - Troubleshooting

2. **[AUTH_INTEGRATION_GUIDE.md](AUTH_INTEGRATION_GUIDE.md)** ⭐
   - Guía completa paso a paso
   - Pruebas de funcionalidad
   - Solución de problemas
   - Arquitectura del sistema

3. **[flutter_frontend/README.md](flutter_frontend/README.md)**
   - Documentación específica de Flutter
   - Configuración de la app
   - Builds y deployment

---

## 🧪 **Pruebas Completas**

### **Test 1: Backend REST API**

```powershell
# Login
$body = @{username='admin'; password='admin123'} | ConvertTo-Json
$response = Invoke-WebRequest -Uri "http://localhost:8080/api/auth/login" `
    -Method POST -Body $body -ContentType "application/json"
$token = ($response.Content | ConvertFrom-Json).token

# Usar token para acceder a FHIR
Invoke-WebRequest -Uri "http://localhost:8080/fhir/Patient" `
    -Headers @{Authorization="Bearer $token"}
```

### **Test 2: Flutter App**

1. Abrir app en emulador/dispositivo
2. Login con `admin` / `admin123`
3. Verificar que muestra Home con roles ADMIN y USER
4. Crear nuevo usuario desde "Regístrate"
5. Logout y login con nuevo usuario

---

## 🔐 **Seguridad**

### **Características Implementadas**

- ✅ Contraseñas hasheadas con BCrypt
- ✅ Tokens JWT con expiración (24h)
- ✅ CORS configurado correctamente
- ✅ Roles y permisos
- ✅ Validación de entrada en backend y frontend
- ✅ Session management segura

### **⚠️ Para Producción**

- [ ] Cambiar JWT secret en production
- [ ] Habilitar HTTPS/TLS
- [ ] Configurar CORS específicos (no `*`)
- [ ] Implementar rate limiting
- [ ] Agregar refresh tokens
- [ ] Audit logging
- [ ] Two-factor authentication

---

## 🗄️ **Base de Datos**

### **Tablas Creadas Automáticamente**

**Autenticación:**
- `app_users` - Usuarios del sistema
- `user_roles` - Roles asignados

**HAPI FHIR (300+ tablas):**
- `hfj_resource` - Recursos FHIR
- `hfj_res_ver` - Versiones de recursos
- `hfj_spidx_*` - Índices de búsqueda
- Y muchas más...

### **Verificar Datos**

```powershell
docker exec -it hapi-fhir-postgres psql -U fhiruser -d fhirdb

# Ver usuarios
SELECT username, email, first_name FROM app_users;

# Ver roles
SELECT u.username, r.role FROM app_users u 
JOIN user_roles r ON u.id = r.user_id;
```

---

## 🐛 **Solución de Problemas Comunes**

### **1. Backend no compila**

```powershell
# Limpiar y recompilar
.\mvnw.cmd clean install -U
```

### **2. Flutter no conecta al backend**

```dart
// En lib/config/api_config.dart
// Para Android Emulator:
static const String baseUrl = 'http://10.0.2.2:8080';

// Para iOS Simulator:
static const String baseUrl = 'http://localhost:8080';

// Para dispositivo físico (tu IP):
static const String baseUrl = 'http://192.168.1.X:8080';
```

### **3. PostgreSQL no arranca**

```powershell
# Ver logs
docker logs hapi-fhir-postgres

# Recrear contenedor
docker rm -f hapi-fhir-postgres
docker run -d --name hapi-fhir-postgres `
  -e POSTGRES_DB=fhirdb `
  -e POSTGRES_USER=fhiruser `
  -e POSTGRES_PASSWORD=fhirpass `
  -p 5432:5432 `
  postgres:16-alpine
```

### **4. Admin no se crea**

Verifica los logs del servidor. Deberías ver:
```
✅ Usuario admin creado exitosamente
   Username: admin
   Password: admin123
```

---

## 📊 **Monitoreo**

### **Health Checks**

```
GET http://localhost:8080/actuator/health
GET http://localhost:8080/actuator/health/liveness
GET http://localhost:8080/actuator/health/readiness
```

### **Métricas**

```
GET http://localhost:8080/actuator/metrics
```

---

## 🎯 **Roadmap**

### **Fase 1: Autenticación ✅ COMPLETADA**
- [x] Login/Logout
- [x] Registro de usuarios
- [x] Creación de admins
- [x] JWT tokens
- [x] Roles y permisos

### **Fase 2: Gestión de Pacientes (Próximo)**
- [ ] CRUD de pacientes en Flutter
- [ ] Búsqueda avanzada
- [ ] Filtros y ordenamiento
- [ ] Paginación

### **Fase 3: Citas Médicas**
- [ ] Programar citas
- [ ] Calendario
- [ ] Notificaciones

### **Fase 4: Historial Médico**
- [ ] Observaciones
- [ ] Diagnósticos
- [ ] Medicaciones
- [ ] Documentos adjuntos

---

## 👥 **Roles del Sistema**

| Rol | Permisos | Descripción |
|-----|----------|-------------|
| **ADMIN** | Completo | Gestión total del sistema |
| **USER** | Básico | Usuario estándar |
| **DOCTOR** | Médico | Acceso a pacientes y citas |
| **NURSE** | Enfermería | Registro de observaciones |

---

## 🌐 **URLs del Sistema**

### **Backend**
- Web UI: http://localhost:8080
- FHIR API: http://localhost:8080/fhir
- Auth API: http://localhost:8080/api/auth
- Metadata: http://localhost:8080/fhir/metadata
- Health: http://localhost:8080/actuator/health

### **Base de Datos**
- Host: localhost
- Port: 5432
- Database: fhirdb
- User: fhiruser

---

## 🔄 **Flujo de Autenticación**

```
┌─────────┐         ┌──────────┐         ┌──────────┐         ┌──────────┐
│ Flutter │         │  Spring  │         │   JWT    │         │PostgreSQL│
│   App   │         │  Backend │         │ Provider │         │   DB     │
└────┬────┘         └─────┬────┘         └─────┬────┘         └─────┬────┘
     │                    │                    │                    │
     │  POST /login       │                    │                    │
     ├───────────────────>│                    │                    │
     │  {username,pwd}    │                    │                    │
     │                    │ Validar usuario    │                    │
     │                    ├───────────────────────────────────────>│
     │                    │                    │                    │
     │                    │<───────────────────────────────────────┤
     │                    │   User found       │                    │
     │                    │                    │                    │
     │                    │  Generar JWT       │                    │
     │                    ├───────────────────>│                    │
     │                    │                    │                    │
     │                    │<───────────────────┤                    │
     │                    │   JWT Token        │                    │
     │                    │                    │                    │
     │<───────────────────┤                    │                    │
     │  {token, user}     │                    │                    │
     │                    │                    │                    │
     │  Guardar token     │                    │                    │
     │  en localStorage   │                    │                    │
     │                    │                    │                    │
     │  GET /fhir/Patient │                    │                    │
     │  Authorization:    │                    │                    │
     │  Bearer {token}    │                    │                    │
     ├───────────────────>│                    │                    │
     │                    │  Validar token     │                    │
     │                    ├───────────────────>│                    │
     │                    │                    │                    │
     │                    │<───────────────────┤                    │
     │                    │   Token válido     │                    │
     │                    │                    │                    │
     │<───────────────────┤                    │                    │
     │  Patients data     │                    │                    │
     │                    │                    │                    │
```

---

## 🎓 **Para Desarrolladores**

### **Agregar Nuevo Endpoint Protegido**

```java
@RestController
@RequestMapping("/api/patients")
public class PatientController {
    
    @GetMapping
    @PreAuthorize("hasRole('USER')")  // Solo usuarios autenticados
    public ResponseEntity<?> getPatients() {
        // ...
    }
    
    @PostMapping
    @PreAuthorize("hasRole('ADMIN')")  // Solo administradores
    public ResponseEntity<?> createPatient() {
        // ...
    }
}
```

### **Agregar Nueva Pantalla en Flutter**

1. Crear archivo en `lib/screens/nueva_screen.dart`
2. Implementar `StatefulWidget` o `StatelessWidget`
3. Agregar navegación desde otra pantalla
4. Usar `Provider` para acceder al estado

---

## 📞 **Soporte**

Para preguntas o problemas:

1. Revisa [AUTH_INTEGRATION_GUIDE.md](AUTH_INTEGRATION_GUIDE.md)
2. Verifica logs del servidor
3. Consulta la documentación de HAPI FHIR
4. Revisa los issues en GitHub

---

## 📄 **Licencia**

Este proyecto es parte del Sistema Hospitalario HAPI FHIR.

---

## ✅ **Checklist de Verificación**

Antes de considerar el sistema completo, verifica:

- [x] PostgreSQL corriendo
- [x] Backend compilado exitosamente
- [x] Servidor iniciado sin errores
- [x] Admin creado automáticamente
- [x] Login funciona desde API
- [x] Flutter app compila
- [x] Flutter conecta al backend
- [x] Login funciona desde Flutter
- [x] Registro de usuarios funciona
- [x] Creación de admins funciona
- [x] Home muestra datos correctos
- [x] Logout funciona
- [x] Sesión persiste al cerrar/abrir app

---

**🎉 ¡Sistema Completo y Funcionando!**

```
Backend:     ✅ Spring Boot + HAPI FHIR + JWT
Database:    ✅ PostgreSQL con autenticación y FHIR
Frontend:    ✅ Flutter con Login, Registro y Home
Docs:        ✅ Guías completas y troubleshooting
Automation:  ✅ Scripts de inicio rápido
```

**Desarrollado con ❤️ para el Sistema Hospitalario**
