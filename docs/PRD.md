# PRD · enlace-portafolio

## 1. Problema
Los desarrolladores, diseñadores y profesionales digitales suelen tener su trabajo disperso entre múltiples plataformas (GitHub, LinkedIn, Behance, CV en PDF, demos desplegadas y redes sociales). Compartir varios enlaces por separado dificulta presentar una identidad profesional clara ante reclutadores o clientes, y construir un sitio web desde cero requiere tiempo de diseño y mantenimiento continuo.

**Solución propuesta:** Una aplicación web que permite centralizar proyectos destacados, enlaces profesionales y datos de perfil en una única página pública personalizable accesible mediante una URL corta y directa.

---

## 2. Usuarios
- **Creador / Profesional (Usuario autenticado):** Persona que crea una cuenta para configurar su perfil público, agregar o editar sus enlaces y proyectos destacados, y compartir su URL personal.
- **Visitante / Reclutador (Usuario público):** Persona que accede al enlace público del portafolio sin necesidad de iniciar sesión para revisar la biografía, experiencia, proyectos y medios de contacto del creador.

---

## 3. Alcance

### Incluido en el MVP (Dentro del alcance)
- Registro, inicio y cierre de sesión de usuarios.
- Edición de perfil básico (nombre, titular profesional, biografía, avatar y nombre de usuario/slug único).
- Gestión completa (crear, leer, actualizar, ordenar y eliminar) de enlaces y tarjetas de proyectos.
- Vista pública del portafolio renderizada dinámicamente según el `slug` del usuario (por ejemplo, `/u/nombre-usuario`).
- Diseño responsivo adaptable a dispositivos móviles y escritorio.

### Fuera del alcance (Versiones futuras)
- Analíticas detalladas de clics por país o dispositivo.
- Conexión con dominios propios personalizados.
- Suscripciones de pago o planes premium.

---

## 4. Requisitos

### Requisitos Funcionales (RF)
- **RF-01 (Autenticación):** El sistema debe permitir el registro e inicio de sesión seguro de cada creador para proteger la edición de su portafolio.
- **RF-02 (Perfil único):** Cada usuario debe contar con un identificador único (`username` / `slug`) que genere su ruta pública sin colisiones.
- **RF-03 (Gestión de enlaces y proyectos):** El usuario autenticado debe poder agregar título, URL, descripción breve y orden de visualización a cada elemento de su portafolio.
- **RF-04 (Visibilidad):** El usuario debe poder activar o desactivar elementos individuales sin eliminarlos permanentemente.
- **RF-05 (Consulta pública):** Cualquier visitante debe poder visualizar el portafolio publicado en modo solo lectura sin requerir autenticación.

### Requisitos No Funcionales (RNF)
- **RNF-01 (Arquitectura):** El código fuente en `src/` debe organizarse por dominio de negocio (*Screaming Architecture*) separando rutas, lógica de aplicación y acceso a datos.
- **RNF-02 (Calidad y tipado):** El proyecto debe compilar sin errores en TypeScript estricto y superar las pruebas unitarias, de integración (PostgreSQL) y E2E (Playwright) en CI.
- **RNF-03 (Rendimiento y usabilidad):** La vista pública del portafolio debe cargar de forma rápida y ser legible en pantallas móviles y de escritorio.

---

## 5. Lista de funcionalidades y estructura en `src/`

Cada funcionalidad principal del producto se organizará en su propia carpeta de dominio dentro de `src/`:

| Funcionalidad | Descripción breve | Carpeta en `src/` |
| :--- | :--- | :--- |
| **Autenticación y sesión** | Registro de cuentas, inicio/cierre de sesión y validación de permisos del creador. | `src/auth/` |
| **Gestión de perfil** | Edición de datos personales, biografía, avatar y configuración del `slug` público. | `src/profiles/` |
| **Enlaces y proyectos (Entidad principal)** | API REST y lógica CRUD para crear, editar, reordenar y ocultar enlaces o proyectos del portafolio. | `src/links/` |
| **Vista pública del portafolio** | Pantalla pública que consulta el perfil y los elementos activos mediante el `slug` del usuario. | `src/portfolio/` |
| **Utilidades y base de datos compartida** | Conexión a PostgreSQL, middlewares, validaciones comunes y tipos compartidos. | `src/shared/` |