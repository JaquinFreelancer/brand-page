# 📋 Casos de Uso

> **Comentarios:**  
> - Estos casos de uso cubren todas las funcionalidades y roles principales según el ERD, flujos de backend y frontend, y buenas prácticas de seguridad.
> - Se especifican los actores, escenarios principales y alternativos, y restricciones relevantes.
> - Roles: `ADMIN`, `EDITOR`, `VIEWER` (usuario autenticado), `Visitante` (no autenticado).
> - Incluye mención de validaciones, seguridad y notificaciones.

---

## Caso de Uso: Navegación Pública

**Actor Principal:** Visitante  
**Escenario Principal:**  
1. El visitante accede al sitio y navega por las páginas públicas (inicio, servicios, equipo, sobre nosotros, blog).
2. Puede ver detalles de servicios, miembros del equipo, testimonios y artículos del blog.
3. Puede buscar información o filtrar artículos por categoría/tag.
4. Puede acceder a políticas legales y de privacidad.

**Restricciones:**  
- El contenido mostrado debe estar publicado y activo.
- Optimización SEO y rendimiento.

---

## Caso de Uso: Enviar Formulario de Contacto

**Actor Principal:** Visitante  
**Escenario Principal:**  
1. El visitante completa el formulario de contacto.
2. El sistema valida campos obligatorios y formato.
3. El sistema verifica CAPTCHA y aplica rate limiting.
4. El mensaje es almacenado y se envía notificación por email al staff.
5. El visitante recibe confirmación de envío.

**Escenarios Alternativos:**  
- Si falla la validación/CAPTCHA, se informa al usuario.
- Si hay error de envío, el visitante es notificado.

**Restricciones:**  
- Almacenamiento de IP y user agent para trazabilidad y seguridad.
- No exponer emails internos ni lógica sensible.

---

## Caso de Uso: Comentario en el Blog

**Actor Principal:** Visitante  
**Escenario Principal:**  
1. El visitante visualiza un post y envía un comentario.
2. El sistema valida los datos (nombre, email, contenido, CAPTCHA).
3. El comentario queda pendiente de moderación.
4. El visitante es informado de la recepción.

**Escenarios Alternativos:**  
- Si el comentario es spam o inválido, se rechaza.
- Si el comentario es aprobado, se muestra públicamente.

**Restricciones:**  
- Validación anti-spam, XSS y almacenamiento seguro.

---

## Caso de Uso: Autenticación y Gestión de Cuenta

**Actor Principal:** Usuario (ADMIN, EDITOR, VIEWER)  
**Escenario Principal:**  
1. El usuario accede a la página de login, ingresa sus credenciales.
2. El sistema valida y genera un token de sesión.
3. El usuario puede ver y editar su perfil, cambiar contraseña, cerrar sesión y recuperar acceso por email.

**Escenarios Alternativos:**  
- Si la autenticación falla, se informa al usuario.
- Si la cuenta está inactiva, se bloquea el acceso.

**Restricciones:**  
- Hash bcrypt, tokens JWT, logs de login, protección contra fuerza bruta.

---

## Caso de Uso: Administración de Usuarios

**Actor Principal:** ADMIN  
**Escenario Principal:**  
1. El ADMIN accede al panel de gestión de usuarios.
2. Puede crear, editar, activar/desactivar, eliminar usuarios, y asignar roles.
3. Puede ver el historial de actividad y fechas de último login.

**Restricciones:**  
- Solo ADMIN puede gestionar usuarios y roles.
- Auditoría y logs obligatorios.

---

## Caso de Uso: Gestión de Contenido Institucional

**Actor Principal:** ADMIN o EDITOR  
**Escenario Principal:**  
1. El usuario autenticado accede al panel para gestionar páginas, servicios, testimonios, equipo.
2. Puede crear, editar, eliminar y publicar/despublicar cada tipo de contenido.
3. El sistema registra el usuario que crea/edita y las fechas.

**Restricciones:**  
- Validación de estados (`DRAFT`, `PUBLISHED`, `ARCHIVED`).
- Permisos según rol, logs de cambios.

---

## Caso de Uso: Gestión y Moderación del Blog

**Actor Principal:** ADMIN o EDITOR  
**Escenario Principal:**  
1. Puede crear, editar, eliminar posts, categorías y tags.
2. Puede programar publicaciones y destacar posts.
3. Modera comentarios (aprobar, rechazar, eliminar).

**Restricciones:**  
- Solo posts en estado `PUBLISHED` son públicos.
- Moderación obligatoria para comentarios de visitantes.

---

## Caso de Uso: Gestión de Archivos Multimedia

**Actor Principal:** ADMIN o EDITOR  
**Escenario Principal:**  
1. Puede subir, listar y eliminar archivos multimedia desde el panel.
2. El sistema valida tipo y tamaño, y almacena metadatos (autor, fecha, uso).

**Restricciones:**  
- Control de acceso, antivirus, validación de MIME y tamaño.

---

## Caso de Uso: Configuración y Analítica del Sitio

**Actor Principal:** ADMIN  
**Escenario Principal:**  
1. Accede al panel de configuración y puede ajustar parámetros generales del sitio.
2. Consulta eventos de analítica y estadísticas de uso.

**Restricciones:**  
- Solo ADMIN accede a configuración avanzada y analítica.
- Logs de cambios y acceso.

---

## Caso de Uso: Visualización de Información Personalizada

**Actor Principal:** Cualquier usuario  
**Escenario Principal:**  
1. El usuario puede buscar servicios, artículos y testimonios usando filtros y búsqueda.
2. El sistema devuelve resultados relevantes y ordenados por prioridad/configuración.

**Restricciones:**  
- Seguridad en los filtros y paginación.
- No exponer datos sensibles en frontend.

---

## Buenas Prácticas y Seguridad (aplica a todos los casos)

- Validación y sanitización de entrada/salida.
- Logs de acciones críticas.
- Acceso a funcionalidades restringido por rol.
- Manejo de errores amigable y sin filtraciones de información.
- Cumplimiento de normativas de privacidad y protección de datos.

---