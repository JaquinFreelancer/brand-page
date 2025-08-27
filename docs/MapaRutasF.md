# 🗺️ Mapa de rutas Frontend

> **Comentarios:**  
> - Este mapa define las rutas principales de la interfaz web (SPA o MPA), su propósito, accesibilidad, y componentes asociados.
> - Se basa en la estructura y entidades del ERD proporcionado y las mejores prácticas de UX, SEO y seguridad.
> - Indica si la ruta es pública, requiere autenticación, o es solo para administradores/editores.
> - El frontend debe consumir la API backend siguiendo el mapa anterior.

---

## Rutas públicas (accesibles para cualquier visitante)

| Ruta                       | Página/Componente                | Descripción                                         |
|----------------------------|----------------------------------|-----------------------------------------------------|
| `/`                        | HomePage                         | Página principal, servicios, testimonios, contacto, destacados, llamadas a la acción |
| `/servicios`               | ServicesList                     | Listado de servicios                                |
| `/servicios/:slug`         | ServiceDetail                    | Detalle de servicio individual                      |
| `/sobre-nosotros`          | AboutUs                          | Sección "Sobre nosotros", misión, visión            |
| `/equipo`                  | TeamList                         | Listado del equipo                                  |
| `/blog`                    | BlogList                         | Listado/paginación de artículos                     |
| `/blog/categoria/:slug`    | BlogCategoryPosts                | Artículos por categoría                             |
| `/blog/tag/:slug`          | BlogTagPosts                     | Artículos por etiqueta/tag                          |
| `/blog/:slug`              | BlogPostDetail                   | Detalle de post, comentarios, tags, autor           |
| `/contacto`                | ContactForm                      | Formulario de contacto                              |
| `/politica-privacidad`     | PrivacyPolicy                    | Página de política de privacidad                    |
| `/aviso-legal`             | LegalNotice                      | Página de aviso legal                               |
| `/busqueda`                | SearchResults                    | Resultados de búsqueda (servicios, blog, etc.)      |
| `/404`                     | NotFound                         | Página de error no encontrada                       |

---

## Rutas de autenticación y usuario

| Ruta                       | Página/Componente                | Descripción                                        | Acceso    |
|----------------------------|----------------------------------|----------------------------------------------------|-----------|
| `/login`                   | Login                            | Formulario de login                                | Pública   |
| `/logout`                  | LogoutHandler                    | Acción de cierre de sesión                         | Usuarios  |
| `/recuperar-password`      | PasswordResetRequest             | Solicitar recuperación de contraseña               | Pública   |
| `/restablecer-password/:token` | PasswordResetConfirm         | Formulario para restablecer contraseña             | Pública   |
| `/perfil`                  | UserProfile                      | Perfil del usuario, editar datos y contraseña      | Usuarios  |

---

## Rutas administrativas (requieren login y rol adecuado)

| Ruta                       | Página/Componente                | Descripción                                        | Roles      |
|----------------------------|----------------------------------|----------------------------------------------------|------------|
| `/admin`                   | AdminDashboard                   | Panel principal de administración                  | ADMIN, EDITOR |
| `/admin/usuarios`          | UserManagement                   | Gestión de usuarios                                | ADMIN      |
| `/admin/usuarios/nuevo`    | UserCreate                       | Crear usuario                                      | ADMIN      |
| `/admin/usuarios/:id`      | UserEdit                         | Editar usuario                                     | ADMIN      |
| `/admin/paginas`           | PagesManagement                  | Listado y gestión de páginas institucionales        | ADMIN, EDITOR |
| `/admin/paginas/nueva`     | PageCreate                       | Crear página                                       | ADMIN, EDITOR |
| `/admin/paginas/:id`       | PageEdit                         | Editar página                                      | ADMIN, EDITOR |
| `/admin/servicios`         | ServicesManagement               | Gestionar servicios                                | ADMIN, EDITOR |
| `/admin/servicios/nuevo`   | ServiceCreate                    | Crear servicio                                     | ADMIN, EDITOR |
| `/admin/servicios/:id`     | ServiceEdit                      | Editar servicio                                    | ADMIN, EDITOR |
| `/admin/testimonios`       | TestimonialsManagement           | Gestionar testimonios                              | ADMIN, EDITOR |
| `/admin/testimonios/nuevo` | TestimonialCreate                | Crear testimonio                                   | ADMIN, EDITOR |
| `/admin/testimonios/:id`   | TestimonialEdit                  | Editar testimonio                                  | ADMIN, EDITOR |
| `/admin/equipo`            | TeamManagement                   | Gestionar miembros del equipo                      | ADMIN, EDITOR |
| `/admin/equipo/nuevo`      | TeamMemberCreate                 | Crear miembro de equipo                            | ADMIN, EDITOR |
| `/admin/equipo/:id`        | TeamMemberEdit                   | Editar miembro de equipo                           | ADMIN, EDITOR |
| `/admin/blog`              | BlogPostManagement               | Gestionar posts del blog                           | ADMIN, EDITOR |
| `/admin/blog/nuevo`        | BlogPostCreate                   | Crear post                                         | ADMIN, EDITOR |
| `/admin/blog/:id`          | BlogPostEdit                     | Editar post                                        | ADMIN, EDITOR |
| `/admin/blog/categorias`   | BlogCategoryManagement           | Gestionar categorías                               | ADMIN, EDITOR |
| `/admin/blog/categorias/nueva` | BlogCategoryCreate           | Crear categoría                                    | ADMIN, EDITOR |
| `/admin/blog/categorias/:id` | BlogCategoryEdit               | Editar categoría                                   | ADMIN, EDITOR |
| `/admin/blog/tags`         | BlogTagManagement                | Gestionar tags                                     | ADMIN, EDITOR |
| `/admin/blog/tags/nueva`   | BlogTagCreate                    | Crear tag                                          | ADMIN, EDITOR |
| `/admin/blog/tags/:id`     | BlogTagEdit                      | Editar tag                                         | ADMIN, EDITOR |
| `/admin/blog/comentarios`  | BlogCommentsModeration           | Moderar comentarios                                | ADMIN, EDITOR |
| `/admin/contacto`          | ContactFormsManagement           | Ver bandeja de mensajes de contacto                 | ADMIN, EDITOR |
| `/admin/archivos`          | MediaFilesManagement             | Gestionar archivos multimedia                      | ADMIN, EDITOR |
| `/admin/configuracion`     | SiteSettingsManagement           | Configuración del sitio                            | ADMIN      |
| `/admin/analytics`         | AnalyticsDashboard               | Estadísticas y eventos analíticos                  | ADMIN      |

---

## Consideraciones y buenas prácticas

- Todas las rutas administrativas deben requerir autenticación y validación de rol antes de renderizar componentes.
- Las rutas públicas deben ser optimizadas para SEO (títulos, meta, canónicas).
- Manejo centralizado de errores y redirección a `/404` o `/login` según corresponda.
- Uso de guardas de ruta (route guards) para proteger acceso y evitar fugas de datos.
- Internacionalización (i18n) y accesibilidad (a11y) recomendada.
- Lazy loading y code splitting en rutas de administración para rendimiento.

---