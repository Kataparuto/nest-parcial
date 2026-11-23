### 1. Separación de responsabilidades entre Controller y Service

**Archivos:** `tasks.controller.ts` y `tasks.service.ts`

- Se eliminó el acceso directo a MongoDB desde `TasksController`.
- Se trasladó la lógica de creación de tareas a `TasksService`.
- Se centralizó en el servicio la verificación de existencia del usuario asociado a la tarea.
- El controlador ahora delega las operaciones al servicio.

2. Restricción de propiedades en MongoDB

**Archivo:** `task.schema.ts`

- Se modificó la configuración de Mongoose de `strict: false` a `strict: true`.
- Las propiedades no declaradas en el esquema ahora se descartan en las operaciones habituales de Mongoose.

**Motivo:** impedir que se almacenen propiedades no definidas en el modelo de datos.

### 3. Validación de solicitudes mediante DTOs

**Archivos:** `create-task.dto.ts`, `tasks.controller.ts` y `main.ts`

- Se creó `CreateTaskDto` para definir los campos permitidos y sus validaciones.
- Se reemplazó `any` por `CreateTaskDto`.
- Se incorporaron `class-validator` y `class-transformer`.
- Se configuró un `ValidationPipe` global con `whitelist`, `forbidNonWhitelisted` y `transform`.

### 4. Corrección del middleware de autenticación

**Archivo:** `app.module.ts`

- Se modificó la configuración de `AuthMiddleware` para aplicarlo únicamente a `POST /tasks`.
- Se mantuvo el acceso público a `GET /tasks` y `GET /tasks/:id`.

### 5. Configuración del token mediante variables de entorno

**Archivos:** `auth.middleware.ts`, `app.module.ts`, `.env` y `.env.example`

- Se eliminó el token de administrador escrito directamente en el middleware.
- Se incorporó `@nestjs/config` para cargar variables de entorno.
- Se configuró `ADMIN_TOKEN` en `.env`.
- Se actualizó `.env.example` con un valor de ejemplo.
- Se añadió una comprobación para rechazar solicitudes cuando el token no está configurado.
