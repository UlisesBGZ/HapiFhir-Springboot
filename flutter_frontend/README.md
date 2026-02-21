# Sistema Hospitalario con HAPI FHIR

Sistema completo de gestión hospitalaria con autenticación JWT, gestión de usuarios y recursos FHIR.

##  Inicio Rápido

**Levantar el servidor:**
```bash
docker-compose up --build -d
```

**Levantar el frontend:**
```bash
cd flutter_frontend
flutter pub get
flutter run -d chrome
```

##  Credenciales por Defecto

- Usuario: `admin`
- Contraseña: `admin123`

##  API Endpoints

**Autenticación:**
- POST `/api/auth/login` - Iniciar sesión
- POST `/api/auth/signup` - Registrar usuario

**Usuarios (Admin):**
- GET `/api/users` - Listar usuarios
- DELETE `/api/users/{id}` - Eliminar usuario

**FHIR:**
- GET/POST `/fhir/Patient` - Gestión de pacientes
- Más endpoints según estándar HL7 FHIR R4

##  Documentación

Ver [AGENTS.md](AGENTS.md) para guía completa de desarrollo.

##  Arquitectura

- **Backend**: Spring Boot + HAPI FHIR + JWT Auth
- **Frontend**: Flutter Web
- **Base de Datos**: PostgreSQL (2 datasources: fhirdb + authdb)
