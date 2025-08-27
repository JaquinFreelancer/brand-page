# 🛣️ Mapa de rutas Backend (API RESTful)

> **Comentarios:**  
> - Este mapa describe las rutas principales de la API, sus métodos, parámetros relevantes y protección por roles.  
> - Basado en el modelo relacional y entidades normalizadas del ERD proporcionado.
> - Roles soportados: `ADMIN`, `EDITOR`, `VIEWER` (usuarios autenticados), y `guest` (no autenticado).
> - Autenticación JWT, validación de permisos y seguridad en cada endpoint administrativo.

---

## Rutas públicas (sin autenticación)

| Método | Ruta                             | Descripción                                      | Roles       |
|--------|----------------------------------|--------------------------------------------------|-------------|
| GET    | /api/pages                       | Listar páginas públicas                          | Todos       |
| GET    | /api/pages/:slug                 | Ver detalle de página                            | Todos       |
| GET    | /api/services                    | Listar servicios activos                         | Todos       |
| GET    | /api/services/:slug              | Detalle de un servicio                           | Todos       |
| GET    | /api/testimonials                | Listar testimonios activos                       | Todos       |
| GET    | /api/team                        | Listar miembros del equipo activos               | Todos       |
| GET    | /api/blog                        | Listar posts publicados (paginado, filtros)      | Todos       |
| GET    | /api/blog/:slug                  | Detalle de post                                  | Todos       |
| GET    | /api/blog/categories             | Listar categorías activas                        | Todos       |
| GET    | /api/blog/tags                   | Listar tags                                      | Todos       |
| GET    | /api/blog/category/:slug         | Listar posts por categoría                       | Todos       |
| GET    | /api/blog/tag/:slug              | Listar posts por tag                             | Todos       |
| GET    | /api/blog/:slug/comments         | Listar comentarios aprobados del post            | Todos       |
| GET    | /api/site-settings/public        | Configuración pública del sitio                  | Todos       |
| GET    | /api/media/:id                   | Descargar/ver archivo multimedia                 | Todos       |
| POST   | /api/contact                     | Enviar formulario de contacto                    | Todos       |
| POST   | /api/blog/:slug/comments         | Comentar en post (moderación)                    | Todos       |

---

## Rutas de autenticación y usuario

| Método | Ruta                             | Descripción                                      | Roles             |
|--------|----------------------------------|--------------------------------------------------|-------------------|
| POST   | /api/auth/login                  | Login y obtención de token JWT                   | Todos             |
| POST   | /api/auth/logout                 | Logout (invalidar sesión/token)                  | Usuarios          |
| POST   | /api/auth/refresh                | Refrescar token JWT                              | Usuarios          |
| GET    | /api/auth/me                     | Obtener datos del usuario                        | Usuarios          |
| PUT    | /api/auth/profile                | Editar perfil                                    | Usuarios          |
| PUT    | /api/auth/change-password        | Cambiar contraseña                               | Usuarios          |
| POST   | /api/auth/password-reset         | Solicitar recuperación de contraseña             | Todos             |
| POST   | /api/auth/password-reset/confirm | Confirmar recuperación de contraseña             | Todos             |

---

## Rutas administrativas protegidas (ADMIN, EDITOR)

### Usuarios (solo ADMIN)

| Método | Ruta                       | Descripción                         | Roles   |
|--------|----------------------------|-------------------------------------|---------|
| GET    | /api/users                 | Listar usuarios                     | ADMIN   |
| POST   | /api/users                 | Crear usuario                       | ADMIN   |
| GET    | /api/users/:id             | Obtener usuario                     | ADMIN   |
| PUT    | /api/users/:id             | Editar usuario                      | ADMIN   |
| DELETE | /api/users/:id             | Eliminar usuario                    | ADMIN   |
| PUT    | /api/users/:id/activate    | Activar/desactivar usuario          | ADMIN   |
| PUT    | /api/users/:id/role        | Actualizar rol de usuario           | ADMIN   |

### Páginas

| Método | Ruta                       | Descripción                         | Roles           |
|--------|----------------------------|-------------------------------------|-----------------|
| POST   | /api/pages                 | Crear página                        | ADMIN, EDITOR   |
| PUT    | /api/pages/:id             | Editar página                       | ADMIN, EDITOR   |
| DELETE | /api/pages/:id             | Eliminar página                     | ADMIN, EDITOR   |

### Servicios

| Método | Ruta                       | Descripción                         | Roles           |
|--------|----------------------------|-------------------------------------|-----------------|
| POST   | /api/services              | Crear servicio                      | ADMIN, EDITOR   |
| PUT    | /api/services/:id          | Editar servicio                     | ADMIN, EDITOR   |
| DELETE | /api/services/:id          | Eliminar servicio                   | ADMIN, EDITOR   |

### Testimonios

| Método | Ruta                       | Descripción                         | Roles           |
|--------|----------------------------|-------------------------------------|-----------------|
| POST   | /api/testimonials          | Crear testimonio                    | ADMIN, EDITOR   |
| PUT    | /api/testimonials/:id      | Editar testimonio                   | ADMIN, EDITOR   |
| DELETE | /api/testimonials/:id      | Eliminar testimonio                 | ADMIN, EDITOR   |

### Equipo

| Método | Ruta                       | Descripción                         | Roles           |
|--------|----------------------------|-------------------------------------|-----------------|
| POST   | /api/team                  | Crear miembro                       | ADMIN, EDITOR   |
| PUT    | /api/team/:id              | Editar miembro                      | ADMIN, EDITOR   |
| DELETE | /api/team/:id              | Eliminar miembro                    | ADMIN, EDITOR   |

### Blog: Posts, Categorías y Tags

| Método | Ruta                               | Descripción                         | Roles           |
|--------|------------------------------------|-------------------------------------|-----------------|
| POST   | /api/blog                          | Crear post                          | ADMIN, EDITOR   |
| PUT    | /api/blog/:id                      | Editar post                         | ADMIN, EDITOR   |
| DELETE | /api/blog/:id                      | Eliminar post                       | ADMIN, EDITOR   |
| PUT    | /api/blog/:id/publish              | Publicar/despublicar post           | ADMIN, EDITOR   |
| POST   | /api/blog/categories               | Crear categoría                     | ADMIN, EDITOR   |
| PUT    | /api/blog/categories/:id           | Editar categoría                    | ADMIN, EDITOR   |
| DELETE | /api/blog/categories/:id           | Eliminar categoría                  | ADMIN, EDITOR   |
| POST   | /api/blog/tags                     | Crear tag                           | ADMIN, EDITOR   |
| PUT    | /api/blog/tags/:id                 | Editar tag                          | ADMIN, EDITOR   |
| DELETE | /api/blog/tags/:id                 | Eliminar tag                        | ADMIN, EDITOR   |

### Blog: Moderación de Comentarios

| Método | Ruta                               | Descripción                         | Roles           |
|--------|------------------------------------|-------------------------------------|-----------------|
| GET    | /api/blog/comments/moderation      | Listar comentarios pendientes       | ADMIN, EDITOR   |
| PUT    | /api/blog/comments/:id/approve     | Aprobar comentario                  | ADMIN, EDITOR   |
| PUT    | /api/blog/comments/:id/reject      | Rechazar comentario                 | ADMIN, EDITOR   |
| DELETE | /api/blog/comments/:id             | Eliminar comentario                 | ADMIN, EDITOR   |

### Contacto

| Método | Ruta                               | Descripción                         | Roles           |
|--------|------------------------------------|-------------------------------------|-----------------|
| GET    | /api/contact-forms                 | Listar mensajes recibidos           | ADMIN, EDITOR   |
| GET    | /api/contact-forms/:id             | Ver mensaje recibido                | ADMIN, EDITOR   |
| PUT    | /api/contact-forms/:id/reply       | Marcar como respondido              | ADMIN, EDITOR   |
| DELETE | /api/contact-forms/:id             | Eliminar mensaje                    | ADMIN, EDITOR   |

### Archivos multimedia

| Método | Ruta                               | Descripción                         | Roles               |
|--------|------------------------------------|-------------------------------------|---------------------|
| POST   | /api/media                         | Subir archivo                       | ADMIN, EDITOR       |
| GET    | /api/media                         | Listar archivos                     | ADMIN, EDITOR       |
| DELETE | /api/media/:id                     | Eliminar archivo                    | ADMIN, EDITOR       |

### Configuración del sitio

| Método | Ruta                               | Descripción                         | Roles           |
|--------|------------------------------------|-------------------------------------|-----------------|
| GET    | /api/site-settings                 | Listar configuración completa       | ADMIN           |
| POST   | /api/site-settings                 | Crear configuración                 | ADMIN           |
| PUT    | /api/site-settings/:id             | Editar configuración                | ADMIN           |
| DELETE | /api/site-settings/:id             | Eliminar configuración              | ADMIN           |

### Analytics

| Método | Ruta                               | Descripción                         | Roles           |
|--------|------------------------------------|-------------------------------------|-----------------|
| GET    | /api/analytics/events              | Listar eventos (filtros, paginación)| ADMIN           |

---

## Notas de seguridad y buenas prácticas

- Autenticación JWT, refresh tokens y expiración configurable.
- Rate limiting y CAPTCHA en rutas críticas (/api/contact, login, registro).
- Validación y sanitización de datos de entrada.
- Logs de acceso y acciones administrativas.
- Protección por roles (principio de menor privilegio).
- CORS y cabeceras seguras.
- Prevención de ataques XSS, CSRF, SQL Injection.

---