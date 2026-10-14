# Proyectos Profesionales

Este documento contiene el detalle de proyectos para usar como fuente de verdad en CV, LinkedIn, portfolio, entrevistas y prompts de IA.

## Automatizacion editorial / IA

### Insider Automation - Editorial AI Workflow

Sistema de automatizacion editorial para Insider Latam que convierte comunicados y notas de prensa recibidos por Gmail (cuerpo, adjuntos, documentos de Google Docs, imagenes y videos) en borradores periodisticos de WordPress listos para revision humana.

Contexto:

- Cliente/proyecto: Insider Latam.
- Sitio relacionado: insiderlatam.com.
- Periodo: mayo 2026 - actualidad (relacion con Insider Latam desde octubre 2024).
- Estado: POC funcional en staging, validado con una muestra real del cliente. La publicacion definitiva no se automatiza.
- Objetivo: reducir el trabajo manual de lectura, resumen, contextualizacion y preparacion inicial de contenidos editoriales, sin perder control editorial.

Evolucion:

1. Mayo 2026 - POC con Zapier: Gmail -> Zapier -> Gemini -> borrador. Sirvio para validar calidad editorial, seleccion de imagen y el contrato de salida JSON con bajo costo.
2. Agosto 2026 - actualidad: reescritura sobre Google Apps Script + Gemini API, siguiendo la alternativa prevista en el POC para ganar control, trazabilidad y menor costo operativo. Mas de 260 commits, 71 servicios `.gs`, 71 suites de tests locales y 8 ADRs.

Flujo principal:

```text
Gmail (etiqueta PUBLICAR_TEST) -> Apps Script -> Drive/Docs (fuentes) -> Gemini API -> validaciones editoriales -> WordPress REST API (draft) -> Revision humana
                                          \-> Google Sheets (configuracion, prompts versionados, log y trazabilidad por lote)
WordPress plugin "Insider Automation Control" -> ControlApi (Apps Script Web App) -> corridas, reintentos, historial y diagnostico
```

Responsabilidades y funcionalidades:

- Arquitectura modular en Apps Script con servicios separados para Gmail, adjuntos, Drive/Docs, fuentes, prompts, Gemini, validacion editorial, imagenes, WordPress, logging y orquestacion.
- Orquestacion reanudable por lotes: la cola se congela al inicio, se procesan hasta 5 casos por invocacion, el avance se persiste en Google Sheets (`BATCH_RUNS`, `BATCH_QUEUE`) y las continuaciones se programan con triggers temporales y watchdog para superar los limites de ejecucion de Apps Script.
- Idempotencia por intento (`attemptKey`): cada intento autorizado crea como maximo un borrador; una reanudacion recupera el draft existente en lugar de duplicarlo.
- Procesamiento multifuente: cuerpo del email, hilo conversacional hasta el mensaje ancla, adjuntos PDF/DOCX, Google Docs enlazados, articulos HTTPS aprobados y medios audiovisuales en Drive/YouTube.
- Separacion entre fuentes factuales y candidatas visuales: una imagen no se convierte en fuente de hechos por estar embebida en el correo.
- Seleccion de imagen destacada multiorigen, con huella SHA-256 para garantizar que el archivo enviado a WordPress sea el mismo que evaluo Gemini.
- Prompts editoriales y terminologia mantenidos en Google Sheets, versionados y modificables sin desplegar codigo.
- Reglas editoriales y de estilo de la casa (manual de estilo Insider) aplicadas mediante servicios de validacion, reparacion de estructura, fidelidad de citas y auditoria final.
- Deteccion de contenido duplicado y fuentes repetidas.
- Metricas de consumo de Gemini y trazabilidad completa por lote.
- Plugin WordPress de control (v0.2.0): panel para iniciar o reanudar corridas, autorizar reintentos, revisar historial sanitizado y diagnosticar la conexion. Las llamadas salen desde PHP con secreto compartido, capability y nonce; el panel nunca recibe secretos, cuerpos de correos ni IDs de Gmail.
- Tests locales en Node que cargan el codigo de Apps Script con dobles de los servicios de Google, ejecutados antes de cada `clasp push`.

Resultados verificables (uso interno; no publicar las cifras en CV ni LinkedIn sin acuerdo del cliente):

- Validacion editorial sobre una muestra del cliente (15 de septiembre de 2026, `gemini-3.5-flash-lite`): 20 casos, 16 `SUCCESS`, 4 `WARNING`, 0 `ERROR`.
- Primera corrida reanudable real (16 de septiembre de 2026): 22 casos terminales, 22 `SUCCESS`, sin intervencion adicional del operador.

Reglas de calidad y seguridad editorial:

- La automatizacion crea borradores, nunca publicaciones definitivas.
- No inventar informacion ni completar datos ausentes en las fuentes; los faltantes se informan como advertencias.
- Los errores editoriales generan warnings; los errores tecnicos quedan registrados.
- Ninguna credencial se almacena en Git; las reglas de seguridad quedan separadas del prompt editorial.

Stack:

Google Apps Script, clasp, Gemini API (`gemini-3.5-flash-lite`), Gmail API, Google Drive, Google Docs, Google Sheets, WordPress REST API, plugin WordPress (PHP), Node.js para tests, analisis multimodal, salidas JSON estructuradas, ADRs y human-in-the-loop editorial. POC inicial con Zapier.

Version para LinkedIn/CV:

Disene y construi un sistema de automatizacion editorial con IA para Insider Latam que transforma comunicados recibidos por Gmail, con sus adjuntos, Google Docs, imagenes y videos, en borradores de WordPress listos para revision humana. Tras validar el concepto con un POC en Zapier, lo reescribi sobre Google Apps Script y Gemini API con orquestacion reanudable por lotes, idempotencia por intento, prompts versionados en Google Sheets, seleccion de imagen destacada con verificacion SHA-256, reglas de estilo editorial y un plugin WordPress de control. Los editores mantienen el control de cada publicacion.

Version corta:

Workflow editorial con IA (Google Apps Script, Gemini API, Gmail, Drive, Sheets y WordPress REST API) que convierte comunicados y adjuntos en borradores revisables, con orquestacion reanudable, idempotencia, prompts versionados, seleccion de imagen y revision humana obligatoria.

Valor profesional y comercial:

- Demuestra el camino completo de una idea de IA aplicada: POC barato para validar, decision explicita de rearquitectura y sistema con contratos, tests, ADRs y evidencia de resultados.
- Combina integraciones, prompting, analisis multimodal, contratos de salida, confiabilidad (reanudacion, idempotencia) y criterio editorial.
- Es un muy buen caso para entrevistas sobre IA aplicada, manejo de limites de plataforma, human-in-the-loop y diseno incremental.
- Puede presentarse comercialmente como automatizacion de operaciones de contenido para medios, agencias y equipos de marketing.
- Hasta contar con uso productivo y mediciones, no afirmar porcentajes de ahorro de tiempo ni publicacion autonoma.

## WordPress

### SEO Content Locker

Plugin personalizado para WordPress orientado a monetizacion, captacion de leads y control de acceso a contenido premium.

Contexto:

- Cliente/proyecto: IntermarketFlow.
- Sitio: intermarketflow.com.
- Periodo: freelance, agosto 2025 - actualidad.
- Dominio: analisis intermarket, tecnico y macroeconomico aplicado a mercados financieros.

Resumen:

Desarrolle una primera version funcional de SEO Content Locker, un plugin que permite bloquear secciones de articulos mediante shortcode, mostrar un modal de suscripcion, validar usuarios por email, restaurar sesiones existentes y limitar abusos mediante control por IP, expiracion temporal de acceso y Google reCAPTCHA.

La solucion integra Mailchimp API v3 para registrar automaticamente contactos en una audiencia, aplicar etiquetas dinamicas segun el tipo de contenido y mantener trazabilidad del origen del lead. Tambien incluye un panel administrativo en WordPress para gestionar leads, consultar registros bloqueados por IP duplicada, exportar datos en CSV, modificar fechas de expiracion, eliminar registros y configurar credenciales de Mailchimp y reCAPTCHA.

Responsabilidades y funcionalidades:

- Desarrollo de shortcode `[lock]` para proteger contenido parcial dentro de posts.
- Inyeccion automatica de modal de captura en entradas individuales.
- Flujo frontend con JavaScript para validar email, consentimiento, reCAPTCHA y estado de acceso.
- Persistencia local del email con `localStorage` para restaurar sesiones.
- Endpoints AJAX para registro de leads y verificacion de estado.
- Seguridad mediante WordPress nonces, sanitizacion de datos y control de permisos.
- Tablas personalizadas para leads principales e intentos con IP duplicada.
- Sistema de acceso temporal con fecha de expiracion configurable.
- Deteccion de multiples registros desde una misma IP.
- Geolocalizacion basica por IP usando `ip-api.com`.
- Integracion con Mailchimp API v3 usando `wp_remote_request`.
- Alta o actualizacion de contactos en Mailchimp mediante metodo PUT.
- Aplicacion automatica de etiquetas como `SUSCRIPTION_SYSTEM`, `ARTICLE` o `NEWSLETTER`.
- Integracion con Google reCAPTCHA para proteccion anti-spam.
- Panel administrativo con `WP_List_Table` para busqueda, paginacion, ordenamiento y acciones por lead.
- Exportacion CSV compatible con Excel.
- Acciones administrativas para expirar leads, editar fecha de expiracion y eliminar registros.
- Paginas de configuracion para Mailchimp y reCAPTCHA.
- Logging por evento en el directorio de uploads de WordPress.
- Notificaciones por email usando `wp_mail`.
- Arquitectura modular con namespaces, autoload manual, servicios y repositorios.

Evolucion 2026 (v1.1.x):

- Refactor incremental hacia namespaces, autoload por classmap, servicios (`MailchimpService`, `LeadRegistrationService`, `LeadAccessService`), repositorios y un `Notifier` en capa de aplicacion, eliminando helpers procedurales.
- Proteccion anti-bot por capas: Google reCAPTCHA v3 en todos los formularios publicos y rate limiting separado por IP/formulario, IP global y email.
- Validacion de nonces en todos los endpoints AJAX y acciones administrativas.
- Campo First Name, atributo de landing y tags de origen en Mailchimp para segmentar leads.
- Shortcode para landings, integracion visual con Elementor y redireccion a pagina de agradecimiento.
- Reporte diario por WP-Cron (`seocontentlocker_day_13_report`) con los leads ingresados 13 dias antes, en horario fijo de Argentina e independiente de la zona horaria de WordPress.
- Correccion de fallos de formularios en paginas cacheadas y logging endurecido.

Detalles tecnicos:

El plugin esta organizado con una arquitectura cercana a capas. Los controladores AJAX delegan la logica a servicios como `LeadRegistrationService` y `LeadAccessService`, mientras que el acceso a base de datos queda encapsulado en repositorios como `LeadRepository` y `SameIpRepository`.

El flujo principal registra un lead, valida reCAPTCHA, verifica si el email ya tiene acceso activo, controla si la IP ya fue usada previamente, guarda el registro en la base de datos, consulta el pais de origen, sincroniza el contacto con Mailchimp y dispara eventos internos para logging y notificaciones.

Stack:

PHP, WordPress Plugin API, MySQL, JavaScript vanilla, AJAX, Mailchimp API v3, Google reCAPTCHA v3, rate limiting, WP-Cron, WP_List_Table, wp_remote_request, wp_mail, shortcodes, hooks, nonces, custom database tables, CSV export, Elementor.

Version corta:

Desarrolle y evolucione un plugin WordPress para bloquear contenido SEO-friendly y capturar leads mediante email, con prueba gratuita temporal, control por IP, proteccion anti-bot por capas (reCAPTCHA v3 y rate limiting), restauracion de sesiones, integracion con Mailchimp, panel administrativo, exportacion CSV, reporte diario por WP-Cron, logs y notificaciones automaticas.

### WP2LinkedIn

Plugin WordPress orientado a publicar manualmente entradas de WordPress en una pagina de empresa de LinkedIn.

Contexto:

- Cliente/proyecto: Insider.
- Sitio relacionado: insiderlatam.com.
- Periodo: 2024 - 2026.
- Version actual: 3.1.

Resumen:

El plugin usa OAuth para conectar con LinkedIn, permite seleccionar una organizacion o pagina de empresa, toma el contenido personalizado desde un campo ACF llamado `content_linkedin` y ofrece controles desde el administrador de WordPress para publicar cada post. Esta orientado a WordPress 6.0+ y PHP 7.4+.

Partes principales:

- `wp2linkedin.php`: archivo principal del plugin. Define constantes, carga el bootstrap y registra la activacion.
- `includes/bootstrap.php`: carga clases `WPLP_*` y helpers compartidos.
- `includes/core/`: inicializacion general del plugin y sistema de logs.
- `includes/admin/`: pantallas del administrador, metaboxes, AJAX y columnas del listado de posts.
- `includes/content/`: registro y configuracion del campo de contenido para LinkedIn.
- `includes/linkedin/`: conexion OAuth, obtencion de organizaciones y publicacion en LinkedIn.
- `includes/helpers.php`: funciones compartidas para tokens, requests y contenido.
- `assets/css/admin.css` y `assets/js/admin.js`: estilos y comportamiento del admin.

Flujo general:

- El administrador conecta el sitio con LinkedIn mediante OAuth.
- El plugin guarda y valida el token.
- Se carga la lista de organizaciones disponibles.
- El usuario selecciona una organizacion por defecto.
- En cada post se usa el contenido del campo ACF `content_linkedin`.
- Desde el admin se puede publicar manualmente en LinkedIn.
- Si la publicacion fue exitosa, el plugin marca el post con `_linkedin_posted` y guarda la fecha en `_linkedin_posted_date`.
- Esa marca evita publicaciones duplicadas.

Validaciones:

- Token disponible y no expirado.
- Organizacion configurada.
- Contenido real para LinkedIn.
- Post no publicado previamente.
- Manejo del vencimiento de token: como LinkedIn no provee refresh token para este flujo, el plugin informa al usuario y permite reconectar mediante OAuth.

Mejoras administrativas:

- Registro de errores tecnicos con `WPLP_Logger`.
- Mensajes claros y accionables en el admin.
- Indicadores visuales en el listado de posts para identificar publicaciones realizadas.
- Indicador para saber si el campo de LinkedIn tiene contenido pendiente de publicar.
- Publicacion de contenido junto con la featured image del post.

Evolucion 2026 (v3.x):

- Reestructuracion con autoload PSR-4 y reorganizacion por responsabilidades.
- Pantalla y aviso de reconexion cuando el token de LinkedIn expira.
- Estados editables de publicacion (`pending`, `manual_published`, `scheduled`) para reflejar publicaciones hechas fuera del plugin.
- Columna de estado de LinkedIn en el listado de posts, con tooltips.
- Plugin complementario WP2LinkedIn Status Quick Access para cambiar el estado desde la Edicion rapida.

Version corta:

Plugin administrativo liviano y especifico para conectar WordPress con una pagina de empresa de LinkedIn y publicar posts de forma controlada usando contenido personalizado desde ACF, OAuth, validacion de token, featured image e indicadores editoriales en el listado de posts.

### Welcome Popup Manager

Plugin personalizado para WordPress que permite administrar y mostrar un popup de bienvenida configurable en el frontend del sitio.

Contexto:

- Cliente/proyecto: Insider.
- Sitio relacionado: insiderlatam.com.
- Periodo: 2024 - 2026.

Resumen:

El plugin permite activar o desactivar el popup desde el panel de administracion, definir una imagen, descripcion, enlace asociado, retraso de aparicion y frecuencia de visualizacion mediante reglas como modo automatico o modo manual basado en cookies.

Arquitectura:

- Admin: gestion del menu, assets del panel y registro de campos de configuracion.
- Domain: logica de negocio independiente, settings, sanitizacion y reglas de visualizacion.
- Public: renderizado del popup, carga de assets frontend y vista publica.
- Bootstrap: inicializacion separada para admin y frontend.
- Views: plantillas desacopladas para administracion y popup publico.

Buenas practicas aplicadas:

- Sanitizacion de datos.
- Escape de salida.
- Carga condicional de assets.
- Uso de constantes del plugin.
- Namespacing en PHP.
- Modularizacion por capas.
- Integracion con WordPress Media Library.
- Interaccion frontend para apertura con delay, cierre por boton, click fuera del modal y tecla Escape.
- Persistencia mediante cookies para controlar frecuencia de visualizacion.

Stack:

PHP, WordPress Plugin API, JavaScript, jQuery, HTML, CSS.

Version corta:

Desarrolle Welcome Popup Manager, un plugin personalizado para WordPress que permite crear y administrar popups de bienvenida configurables desde WP Admin, con arquitectura modular, carga condicional de assets, integracion con Media Library, sanitizacion de opciones, delay configurable y control de frecuencia mediante cookies.

### Insider Newsletters

Plugin personalizado para WordPress orientado a centralizar la creacion, administracion y exportacion de newsletters y banners desde el panel de administracion.

Contexto:

- Cliente/proyecto: Insider.
- Sitio relacionado: insiderlatam.com.
- Periodo: 2024 - 2026.

Resumen:

El proyecto permite gestionar newsletters como un Custom Post Type propio, asociar contenidos editoriales y piezas graficas mediante campos personalizados, renderizar el resultado como HTML responsive compatible con clientes de email y exportar el codigo final directamente desde el administrador.

Arquitectura:

- Bootstrap.
- Domain.
- Infrastructure.
- UI/Admin.
- UI/Frontend.

La capa de dominio concentra el modelo, helpers y servicio principal de renderizado de newsletters. Infraestructura gestiona integraciones con WordPress, ACF y logging. La capa de UI implementa experiencia administrativa, columnas personalizadas, filtros de relaciones ACF, accion de exportacion y carga del template frontend.

Funcionalidades:

- Registro de CPTs para newsletters y banners verticales/horizontales.
- Configuracion de campos ACF locales.
- Renderizado de newsletters en HTML basado en tablas para compatibilidad con email clients.
- Exportacion segura del HTML mediante `admin-post`.
- Validaciones con nonces y capacidades de usuario.
- Fallback cuando ACF no esta activo.
- Sistema de logging para diagnostico.
- HTML responsive compatible para integrar con Doppler y enviar newsletters.

Stack:

PHP, WordPress Plugin API, Custom Post Types, Advanced Custom Fields, HTML email responsive, JavaScript administrativo, PSR-4 autoload propio, arquitectura modular orientada a servicios.

Version corta:

Desarrolle un plugin personalizado para WordPress orientado a la gestion integral de newsletters editoriales, con Custom Post Types, campos ACF locales, renderizado HTML responsive compatible con clientes de email y exportacion segura desde el panel administrativo.

### WP Admin Posts Extended

Plugin personalizado para WordPress orientado a mejorar la gestion editorial dentro del panel administrativo.

Contexto:

- Cliente/proyecto: Insider.
- Sitio relacionado: insiderlatam.com.
- Periodo: 2024 - 2026.
- Version actual: 2.5.7.

Resumen:

El proyecto extiende la pantalla nativa de listado de posts agregando filtros avanzados por etiquetas, integracion con filtros existentes de categoria, fecha y busqueda, y exportacion de resultados filtrados a Excel.

Arquitectura:

- Admin Layer: controladores para filtros, exportacion, assets y vistas del panel administrativo.
- Domain Layer: objetos de criterio y contratos que representan la logica de negocio de filtrado.
- Infrastructure Layer: adaptadores concretos para WordPress, incluyendo repositorios y modificadores de queries.
- Bootstrap: registro centralizado de dependencias, hooks y campos ACF.

Funcionalidades:

- Selector multiple de etiquetas con Select2.
- Compatibilidad con filtros nativos de WordPress.
- Exportacion de resultados filtrados a Excel.
- Reportes con fecha, titulo, enlace, estado de publicacion en LinkedIn, fuente, categorias y etiquetas.
- Campo personalizado con ACF para clasificar la fuente del contenido como "Nota original" o "Comunicado de prensa".
- Filtros por autor y por ano (desde 2016 hasta el ano actual).
- Campo ACF `hasVideo` y columna compacta con indicadores visuales para posts con videos de YouTube embebidos.
- Estados de LinkedIn en el Excel (`Pendiente`, `Publicado`, `Publicado manualmente`, `Programado`), alineados con WP2LinkedIn.

Stack:

PHP, WordPress Plugin API, hooks de WordPress, WP_Query, Advanced Custom Fields, Composer, PhpSpreadsheet, Select2, jQuery, CSS personalizado.

Version corta:

Plugin WordPress personalizado para mejorar la gestion editorial del backend, agregando filtros avanzados por etiquetas, integracion con filtros nativos y exportacion de posts filtrados a Excel. Desarrollado en PHP con WordPress Plugin API, Composer, PhpSpreadsheet, ACF y Select2, bajo una arquitectura modular por capas.

### Insider Shorts

Plugin WordPress que toma videos de playlists de YouTube y los muestra como carrusel de shorts embebible mediante shortcode, replicando la experiencia de carruseles de shorts de medios digitales.

Contexto:

- Cliente/proyecto: Insider Latam.
- Periodo: octubre 2026 - actualidad.
- Estado: en desarrollo (etapas de configuracion, sincronizacion de playlists y carrusel frontend completadas).

Funcionalidades:

- Alta de playlists, sincronizacion con YouTube Data API v3 e historial de sincronizaciones.
- Fallback al RSS publico de YouTube cuando no hay API key (hasta 15 videos, sin duracion).
- API key configurable por constante en `wp-config.php` o desde el panel; las llamadas salen del servidor.
- Carrusel con CSS scroll snap y JavaScript vanilla, configurable por breakpoint (desktop, tablet, mobile): autoplay, loop, flechas, puntos, color de acento, vista previa al pasar el mouse y duracion.
- Shortcode `[insider_shorts id="N"]` y desinstalacion limpia opcional.
- Manual de usuario y casos de prueba preparados para el cliente en Google Docs, siguiendo [la guia de documentos de cliente](guia-documentos-cliente.md).

Stack:

PHP 8.1, WordPress 6.4+, YouTube Data API v3, RSS, JavaScript vanilla, CSS scroll snap, shortcodes, Settings API.

Version corta:

Plugin WordPress para mostrar playlists de YouTube como carrusel de shorts administrable, con sincronizacion via YouTube Data API v3, fallback a RSS, configuracion responsive por breakpoint y documentacion de usuario para el cliente.

### World Cup 2026 Widget

Plugin WordPress para mostrar cards de partidos del Mundial 2026 por fecha usando API-Football, desarrollado para insiderlatam.com.

Contexto:

- Cliente/proyecto: Insider Latam.
- Periodo: mayo 2026 - julio 2026.

Funcionalidades:

- Cliente HTTP propio para el endpoint `/fixtures` de API-Football (API-SPORTS).
- Sincronizacion de la temporada completa con cache comun (`FixturesSyncService` + `FixturesRepository` sobre transients), de modo que el frontend navega entre dias sin nuevas llamadas a la API.
- Endpoint REST propio para servir los partidos al frontend.
- Carrusel horizontal con equipos, logos, marcador, estado, fase, estadio y penales.
- Estilos que heredan tipografia y colores del theme.

Stack:

PHP, WordPress Plugin API, WordPress REST API, API-Football v3, transients, shortcodes, JavaScript, CSS.

Version corta:

Plugin WordPress con shortcode para mostrar partidos del Mundial 2026 desde API-Football, con sincronizacion de temporada, cache, endpoint REST propio y carrusel responsive integrado al theme.

### Cannes Festival Medal Tracker

Plugin WordPress para importar, administrar y mostrar el medallero por pais del festival de Cannes Lions para Hispanoamerica.

Contexto:

- Cliente/proyecto: Insider Latam.
- Periodo: mayo 2026 - julio 2026.

Funcionalidades:

- Importacion de resultados desde Excel con PhpSpreadsheet, tolerante a variaciones de encabezados y filas de titulo.
- Normalizacion de premios (Grand Prix, Gold, Silver y Bronze Lion, incluidas variantes Campaign) y filtro de paises hispanoamericanos, incluso en celdas con varios paises.
- Vista previa del procesamiento fila por fila con estado y motivo, y registro de filas ignoradas en logs.
- Tabla propia (`{prefix}_fmb_country_medals`) creada en la activacion.
- Render publico del medallero por pais.

Stack:

PHP, WordPress Plugin API, Composer, PhpSpreadsheet, MySQL (tabla propia), HTML, CSS.

Version corta:

Plugin WordPress para importar desde Excel y publicar el medallero de Cannes Lions por pais, con normalizacion de premios, filtro regional, vista previa auditable y tabla propia.

### Herramientas editoriales menores (Insider Latam, 2026)

Plugins chicos y especificos que resuelven fricciones del trabajo editorial diario. No se destacan individualmente en el CV, pero muestran criterio para resolver necesidades puntuales con bajo costo de mantenimiento:

- BeyondWords Quick Edit: checkbox de generacion de audio de BeyondWords en la Edicion rapida, con migracion del meta legacy.
- Has Video ACF Quick Edit: edicion del campo ACF `hasVideo` desde la Edicion rapida.
- WP2LinkedIn Status Quick Access: edicion del estado de LinkedIn desde la Edicion rapida.
- Remove Fields Quick Edit (Chip Tecnologia): quita campos que generaban confusion en la edicion rapida y por lotes.
- Silence Early Translation Notices: mu-plugin que filtra del `error_log` avisos conocidos e inofensivos (por tipo, archivo y texto) para que queden visibles solo los errores reales.

## React / TypeScript / Full Stack

### Portal Expensas Admins

Aplicacion web administrativa para la gestion integral de consorcios y expensas, usada por administraciones de edificios en su trabajo diario.

Contexto:

- Compania: 404 Crafters.
- Periodo aproximado: mayo 2025 - actualidad.
- Rol: Senior Full Stack Engineer.
- Participacion: definicion general de UI tomando como guia el dashboard de Material UI; segundo contribuidor del repositorio (mas de 1.400 commits propios en un equipo de 4 personas); pipeline de despliegue.

Resumen:

Permite operar modulos vinculados a administraciones, consorcios, unidades funcionales, propietarios, empleados, sueldos, liquidaciones, prorrateos, pagos, ordenes de pago, proveedores, polizas de seguro, juicios, asambleas, amenities, documentos y tickets internos de soporte mediante una interfaz orientada al trabajo diario de administracion.

Arquitectura:

El proyecto esta desarrollado con React, TypeScript, Vite y Material UI, utilizando MUI X DataGrid para vistas tabulares avanzadas y editables, React Router para navegacion, i18next para internacionalizacion y Apollo GraphQL para comunicacion con backend.

La aplicacion sigue una arquitectura basada en Clean Architecture, CQRS y Presenter Pattern:

```text
Component -> Presenter.handleX() -> Core.execute(Query/Command) -> Handler -> GraphQL -> Mapper -> Domain -> Presenter.updateModel()
```

Desde 2026 el mismo repositorio compila varios portales (Administraciones, Proveedores y Encargados) que comparten core, cliente GraphQL, theme y libreria de componentes. La frontera entre `shared/` y cada portal se aplica con reglas de ESLint, no por convencion.

Funcionalidades donde tuve participacion principal:

- Sueldos y liquidaciones de empleados (payroll), recibos y prorrateos.
- Unidades funcionales, consorcios, propietarios, cargos por unidad y vencimientos.
- Rocket: sistema de tickets y conversaciones de soporte con GraphQL subscriptions sobre WebSocket, reconexion con resincronizacion, indicadores de accion en el header, audiencias por grupo de categoria y pegado de imagenes.
- Amenities, asambleas, juicios, polizas de seguro, ordenes de pago, notas y datos de contacto (firmas y logos de la administracion).
- DataGrid editable reutilizable para carga masiva de datos.
- Ajustes mobile de tablas, filtros y resumenes.

Delivery:

- GitHub Actions que construye imagenes Docker por portal, las publica en GitHub Container Registry y despliega en AWS Lightsail con Docker Compose, Traefik como reverse proxy y certificados de Let's Encrypt.
- Health checks post-deploy y flujo de hotfixes a produccion desde tags `hotfix-*`.
- Trabajo por tickets con pull requests y conventional commits.

Stack:

React 18, TypeScript, Vite, Material UI, MUI X DataGrid, MUI X Date Pickers, React Router, i18next, Apollo GraphQL, GraphQL subscriptions (graphql-ws), Clean Architecture, CQRS, Presenter Pattern, ESLint, Docker, GitHub Actions, GHCR, AWS Lightsail, Traefik, NGINX.

Version para LinkedIn/CV:

Portal Expensas: build a condominium management platform covering settlements, payroll, payments, units, suppliers, and documents. Develop interfaces and business workflows using React, TypeScript, Material UI, and Apollo GraphQL, applying Clean Architecture, CQRS, and the Presenter Pattern. (Texto publicado en LinkedIn. El dato de segundo contribuidor queda para entrevistas, no para el perfil.)

Version corta:

Plataforma administrativa React + TypeScript para gestion de consorcios con Clean Architecture, CQRS y Presenter Pattern, Apollo GraphQL con subscriptions en tiempo real, MUI X DataGrid, multiples portales desde un mismo core y despliegue con GitHub Actions, Docker y AWS Lightsail.

### News Kiosk

Plataforma web para la gestion, busqueda, analisis y visualizacion de articulos y noticias.

Contexto:

- Compania: 404 Crafters.
- Periodo aproximado: noviembre 2023 - marzo 2025.
- Cliente: cliente nativo de Estados Unidos.
- Participacion: desarrollo full stack y definicion/planteo de UI.

Resumen:

News Kiosk permite explorar contenido periodistico por sectores, industrias, fuentes, terminos relevantes, companias y metricas. Ofrece una experiencia tipo dashboard para filtrar articulos, visualizar detalle, detectar topicos, resaltar terminos, guardar busquedas favoritas y compartir resultados por email o enlaces publicos.

El proyecto esta compuesto por una aplicacion frontend moderna en React y TypeScript, y una API REST desarrollada con Node.js, Express y MongoDB. La interfaz incluye autenticacion, rutas protegidas, dashboards, vistas de articulos, gestion de busquedas guardadas, emails, navegacion por topicos, lectura de PDFs/contenido plano y componentes reutilizables basados en Material UI.

Arquitectura frontend:

El frontend esta organizado con separacion por capas:

- Presentation: paginas, layouts, componentes, temas, contextos y rutas.
- Domain: modelos, repositorios y casos de uso.
- Data: DTOs, datasources y repositorios concretos para consumir APIs.

Para el manejo de datos asincronicos utiliza React Query, mientras que Axios centraliza la comunicacion HTTP con servicios backend.

Arquitectura backend:

El backend expone una API REST modular organizada por rutas, controladores, modelos y middlewares. Gestiona entidades como usuarios, sesiones, articulos, topicos, terminos, sectores, fuentes, busquedas, carpetas, templates, historial, importaciones y contenido compartido.

Utiliza Mongoose para modelado y persistencia en MongoDB, JWT para autenticacion, Nodemailer para envio de emails, Winston/CloudWatch para logging y Docker/PM2 para despliegue y ejecucion en entornos productivos.

Funcionalidades:

- Autenticacion y rutas protegidas.
- Dashboards de exploracion y analisis de noticias.
- Busqueda y filtrado por sectores, industrias, fuentes, companias y terminos clave.
- Visualizacion de detalle de articulos.
- Deteccion y navegacion por topicos.
- Resaltado de terminos relevantes.
- Gestion de busquedas favoritas.
- Compartido de resultados por email o enlaces publicos.
- Lectura de PDFs y contenido plano.
- Gestion de templates, historial, importaciones y contenido compartido.

Stack:

Frontend: React 18, TypeScript, React Router, Material UI, Emotion, React Query, Axios, React Hook Form, Yup, i18next, Framer Motion, React PDF, React Quill, Draft.js.

Backend: Node.js, Express, MongoDB, Mongoose, JWT, bcrypt, Nodemailer, AWS SDK, Winston, PM2.

Infraestructura y herramientas: Docker, Docker Compose, GitLab CI/CD, ESLint, Prettier, npm/yarn.

Version para LinkedIn/CV:

Desarrolle y mantuve una plataforma full stack de analisis y gestion de noticias, orientada a la busqueda avanzada, categorizacion, visualizacion y seguimiento de articulos por sectores, industrias, fuentes, companias y terminos clave. Implemente una arquitectura frontend en React + TypeScript separada por capas de presentacion, dominio y datos, integrando React Query, Axios, Material UI, rutas protegidas, autenticacion JWT, dashboards interactivos, lectura de PDFs y gestion de busquedas guardadas. En backend trabaje con Node.js, Express, MongoDB y Mongoose, disenando APIs REST modulares para articulos, usuarios, sesiones, terminos, fuentes, busquedas, templates, historial, importaciones y funcionalidades de compartido/envio por email. El proyecto incluye despliegue con Docker/PM2, logging con Winston/CloudWatch y automatizacion CI/CD con GitLab.

Version corta:

Plataforma full stack para analisis, busqueda y gestion de noticias. Frontend en React + TypeScript con arquitectura por capas, Material UI, React Query y Axios. Backend REST en Node.js/Express con MongoDB/Mongoose, autenticacion JWT, envio de emails, logging y despliegue con Docker/PM2.

### WhatsApp AI Tournament Assistant

Asistente conversacional por WhatsApp para torneos amateur que permite a participantes y organizadores consultar informacion operativa en lenguaje natural, sin instalar una aplicacion ni iniciar sesion.

Contexto:

- Cliente/organizacion: Mundialito Senior.
- Periodo: marzo 2026 - julio 2026.
- Tipo: desarrollo freelance para un cliente.
- Estado: presentado al cliente con devolucion positiva; puesta en marcha pendiente del lado del cliente.
- Objetivo: reducir consultas manuales a organizadores y ofrecer respuestas rapidas, consistentes y auditables.
- Canal: WhatsApp mediante webhook de Twilio.
- Estado: arquitectura v2 implementada en NestJS, con camino documentado hacia WhatsApp Business productivo.

Resumen:

El sistema responde sobre inscripciones, reglas, sedes, fixture, resultados, tablas de posiciones, equipos, planteles, estadisticas de jugadores y rankings. Combina una base de conocimiento editable en Google Docs con datos de torneos sincronizados y consultas acotadas a datos vivos de CopaFacil.

Arquitectura:

La solucion esta construida con NestJS 10, TypeScript estricto y Node.js 20+. La arquitectura separa cuatro contextos: `data`, `assistant`, `shared` y `admin`, con una direccion de dependencias clara. La capa `data` no conoce al LLM; el motor conversacional consume casos de uso y servicios de lectura desacoplados.

El flujo conversacional utiliza una maquina de estados para saludo, despedida, seleccion y cambio de torneo. Para una consulta normal, un pipeline de dos llamadas al LLM realiza routing mediante tools, ejecuta las consultas necesarias y genera la respuesta final usando el historial y los resultados obtenidos.

El proyecto evoluciono desde un enfoque monolitico hacia una arquitectura donde la lectura de datos, el motor conversacional, las herramientas administrativas y las integraciones externas quedan separadas. Esto permite cambiar fuentes de datos, reglas de negocio o proveedor de LLM sin acoplar toda la aplicacion.

Funcionalidades:

- Recepcion de mensajes entrantes mediante webhook de Twilio y respuesta en TwiML.
- Validacion manual de la firma HMAC-SHA1 de Twilio con fail-closed cuando la configuracion es invalida.
- Seleccion multi-torneo y multi-categoria, con cambio de torneo durante la conversacion.
- Memoria de sesion en RAM con TTL de 10 minutos para mantener el contexto conversacional.
- Normalizacion de consultas y tolerancia a errores de escritura en nombres de equipos.
- Siete tools con `strict: true` para fixture, resultados, posiciones, equipos, jugadores, estructura y rankings.
- Function calling para consultar unicamente los datos necesarios para cada pregunta.
- Dos perfiles de datos: Postgres para estructura y lecturas sincronizadas; CopaFacil para resultados y rankings vivos, con fallback a Postgres.
- Cliente HTTP centralizado con retry/backoff y reparacion de JSON malformado proveniente de CopaFacil.
- Guarda anti-alucinacion que compara la respuesta generada contra los datos crudos devueltos por las tools y degrada a una respuesta segura si detecta informacion no sustentada.
- Google Docs como CMS no-code para FAQ y lista de torneos.
- Panel administrativo protegido por `AdminKeyGuard` para configurar torneos, ejecutar sincronizaciones y probar consultas.
- Plataforma de testing in-process para curar preguntas, convertirlas en casos y ejecutar el mismo motor que usa produccion.
- Visor de solo lectura de conversaciones reales recibidas por WhatsApp.
- Persistencia en PostgreSQL para configuracion, datos sincronizados, testing y conversaciones reales.
- Validacion de variables de entorno con Joi, manejo global de excepciones y headers de seguridad con Helmet.

Stack:

NestJS 10, TypeScript strict, Node.js 20+, OpenAI SDK, `gpt-4.1-mini`, function calling, structured outputs, Twilio WhatsApp API, TwiML, PostgreSQL, CopaFacil API, Google Docs, Joi, Helmet, retry/backoff, AdminKeyGuard.

Valor profesional y comercial:

- Es un caso de IA aplicada a una operacion concreta: responder consultas frecuentes y acceder a datos deportivos desde el canal que ya utilizan los usuarios.
- Demuestra integracion entre mensajeria, LLMs, APIs externas, persistencia, herramientas internas y reglas de negocio.
- Es especialmente valioso para entrevistas por el tratamiento de confiabilidad: tool calling estricto, separacion de fuentes, fallback, control de alucinaciones, validacion de firmas y testing del mismo pipeline de produccion.
- Puede presentarse comercialmente como un patron adaptable a soporte, reservas, consultas operativas, eventos, clubes, turismo o servicios con informacion estructurada.
- Conviene describirlo como producto en desarrollo o arquitectura preparada para productizacion, sin afirmar volumen de usuarios o disponibilidad productiva si no existen metricas verificadas.

Version corta:

Construi un asistente conversacional por WhatsApp para torneos amateur con NestJS, TypeScript, Twilio, OpenAI, PostgreSQL, Google Docs y CopaFacil API. El sistema gestiona multiples torneos, utiliza siete tools con function calling estricto, consulta datos estructurados y vivos, aplica fallback y valida las respuestas para evitar informacion no sustentada.

### CUTI - Corporate Conference Calls

Aplicacion mobile orientada a la gestion y participacion en conference calls corporativas, con foco en la interaccion entre empresas e inversores.

Contexto:

- Modalidad: freelance / periodo de crecimiento profesional.
- Periodo: febrero 2023 - noviembre 2023.
- Foco: aprendizaje y aplicacion de React Native, TypeScript, arquitectura limpia e integraciones realtime.

Resumen:

CUTI permite registrar usuarios con distintos perfiles, autenticar sesiones, crear llamadas, listar y buscar conferencias, participar en llamadas en vivo por audio, gestionar speakers/audience, levantar la mano para solicitar participacion, visualizar documentos PDF asociados y acceder a grabaciones posteriores.

El proyecto integra comunicacion en tiempo real mediante Agora RTC para audio en vivo y Socket.IO para sincronizacion de estado de las llamadas, actualizaciones de participantes y eventos de moderacion. Ademas, consume una API REST para autenticacion, gestion de usuarios, creacion de calls, obtencion de tokens Agora, busqueda, edicion de perfil y administracion de participantes.

Funcionalidades:

- Registro y autenticacion de usuarios.
- Gestion de perfiles empresa/inversor.
- Creacion, listado y busqueda de conference calls.
- Participacion en llamadas en vivo por audio mediante Agora RTC.
- Sincronizacion realtime con Socket.IO.
- Gestion de speakers y audience.
- Accion de levantar la mano para solicitar participacion.
- Visualizacion de documentos PDF asociados.
- Reproduccion de grabaciones posteriores.
- Edicion de perfil y avatar.
- Persistencia de sesion/token con AsyncStorage.
- Consumo de API REST con Axios.
- Manejo centralizado de errores.

Arquitectura:

La aplicacion esta organizada con una separacion clara por capas, cercana a Clean Architecture:

- `ui`: pantallas, componentes reutilizables, theme, navegacion y logica de presentacion.
- `core/domain`: entidades de dominio, contratos, validadores, errores y tipos principales.
- `core/useCases`: casos de uso para login, registro, creacion de calls, busqueda, moderacion y gestion de usuarios.
- `core/infrastructure`: implementaciones concretas para HTTP, almacenamiento local, formateo de respuestas, manejo de errores y servicios externos.
- `extensions` / `ui/agora`: integracion tecnica con Agora RTC, permisos nativos y funciones de audio.

Esta estructura permite mantener la logica de negocio desacoplada de la interfaz y de los proveedores externos, haciendo que las pantallas consuman casos de uso en lugar de interactuar directamente con la API.

Stack:

React Native 0.68, TypeScript, React 17, React Navigation Native Stack, Agora RTC SDK, Socket.IO Client, Axios, AsyncStorage, React Native Config, React Native WebView, React Native Image Crop Picker, React Native Simple Audio Player, Sound Player, Jest, ESLint, Android, iOS.

Version para LinkedIn:

Desarrolle una aplicacion mobile en React Native y TypeScript para la gestion de conference calls corporativas entre empresas e inversores. La app incluye autenticacion, registro de perfiles, creacion y busqueda de llamadas, participacion en audio en vivo mediante Agora RTC, sincronizacion en tiempo real con Socket.IO, gestion de speakers/audience, visualizacion de PDFs, reproduccion de grabaciones y edicion de perfil. Implemente una arquitectura por capas inspirada en Clean Architecture, separando UI, casos de uso, dominio e infraestructura para mejorar mantenibilidad, escalabilidad y testabilidad.

Version para CV:

Aplicacion mobile de conference calls corporativas desarrollada con React Native, TypeScript, Agora RTC, Socket.IO y Axios. Implementa autenticacion, registro de usuarios, gestion de perfiles empresa/inversor, creacion y busqueda de llamadas, audio en vivo, moderacion de participantes, visualizacion de documentos PDF y reproduccion de grabaciones. Arquitectura modular por capas con separacion entre UI, dominio, casos de uso e infraestructura, integrando API REST, almacenamiento local con AsyncStorage y manejo centralizado de errores.

### POC Cartas - Baraja Espanola

Prueba de concepto mobile para la manipulacion interactiva de una baraja espanola configurable.

Contexto:

- Modalidad: proyecto autodidacta / aprendizaje continuo.
- Periodo: abril 2026 - mayo 2026.
- Foco: practica mobile con Expo, React Native, TypeScript, arquitectura hexagonal e interacciones tactiles.

Resumen:

El proyecto permite simular una mesa de juego donde el mazo comienza apilado boca abajo, las cartas pueden arrastrarse desde el mazo, soltarse libremente sobre la mesa, reposicionarse, superponerse dinamicamente y voltearse mediante doble toque o doble clic.

Funcionalidades:

- Barajas espanolas de 40 y 50 cartas.
- Palos tradicionales: Oro, Copa, Basto y Espada.
- Inclusion/exclusion de rangos segun tamano del mazo.
- Comodines en variante de 50 cartas.
- Personalizacion de color del dorso, diseno de caras y tamano del mazo.
- Arrastrar, soltar, reposicionar, superponer y voltear cartas.

Arquitectura:

El proyecto sigue arquitectura hexagonal, separando dominio, casos de uso, mappers, infraestructura y presentacion. La logica de negocio se mantiene independiente de la UI, permitiendo consumir funcionalidad desde casos de uso locales o desde un backend REST desarrollado con Node.js y Express.

Stack:

React Native, Expo, TypeScript, Node.js, Express, REST API, react-native-svg.

Conceptos:

Arquitectura hexagonal, separacion de dominio y presentacion, casos de uso puros, diseno mobile-first, animaciones interactivas, modelado de entidades de dominio, configuracion dinamica de UI y extensibilidad visual.

### Portal de Aliados

Portal web administrativo y de inteligencia de negocios para aliados de Fanki.

Contexto:

- Compania: 404 Crafters.
- Periodo aproximado: agosto 2024 - abril 2025.
- Participacion: desarrollo de producto y definicion general de UI.

Resumen:

La plataforma esta orientada a la gestion y analisis de eventos, ventas, pagos, asistencias, abonos, comercios y usuarios. Permite a distintos perfiles operativos y administrativos consultar metricas comerciales, descargar reportes, visualizar dashboards, gestionar eventos activos/pasados y administrar configuraciones asociadas a organizaciones especificas.

Arquitectura:

SPA moderna con React 18, TypeScript y Vite, utilizando Material UI, MUI X Data Grid/Charts, ApexCharts, React Router, React Hook Form, Zod, i18next y librerias de soporte para estado observable, presenters, validacion, HTTP y almacenamiento.

La aplicacion implementa autenticacion, control de acceso por roles, restricciones por organizacion, feature flags y carga diferida de modulos para optimizar rendimiento.

Sigue una separacion por capas: dominio, casos de uso, infraestructura y UI. La logica de negocio se organiza en use cases y modelos de dominio, mientras que la presentacion se estructura con componentes React y presenters para manejar estado, inicializacion de sesion, navegacion y flujos de pantalla.

Backend / delivery:

Incluye un servidor Node.js/Express para servir el build productivo, exponer configuracion runtime y aplicar middlewares de seguridad y performance como Helmet, Compression, Morgan y Cookie Parser. La entrega contempla pipeline CI/CD con GitLab, despliegue en Vercel para entornos productivo/staging y soporte de containerizacion con Docker multi-stage y Helm/Kubernetes.

Stack:

React, TypeScript, Vite, Material UI, MUI X, ApexCharts, React Router, React Hook Form, Zod, i18next, Node.js, Express, Docker, GitLab CI/CD, Vercel, Helm/Kubernetes.

Version corta:

Desarrolle un portal web B2B para aliados, enfocado en gestion de eventos e inteligencia de negocios sobre ventas, pagos, asistencias, abonos y comercios. Implementado con React, TypeScript, Vite y Material UI, con arquitectura por capas basada en dominio, casos de uso, infraestructura y UI. Incluye autenticacion, autorizacion por roles, restricciones por organizacion, dashboards, reportes exportables, feature flags y despliegue mediante Node/Express, Docker, GitLab CI/CD, Vercel y Helm/Kubernetes.

## Iniciativa propia - Prostagma (en desarrollo)

Prostagma es una celula de desarrollo senior con base en Tandil, orientada a acoplarse al negocio del cliente con desarrollo web y mobile, IA, chatbots, automatizaciones y cloud. A octubre 2026 esta en etapa de armado: landing sin publicar y productos en fase inicial. No incluir en el CV como empresa hasta que tenga presencia publica.

### Copa Prostagma

Plataforma SaaS multi-tenant para administrar torneos de futbol: organizaciones, competencias, equipos, jugadores, fixture, resultados y tablas de posiciones. Es la evolucion natural del WhatsApp AI Tournament Assistant hacia un producto propio.

- Periodo: agosto 2026 - actualidad.
- Estado: bootstrap tecnico del monorepo y vertical slices de autenticacion, Organizations y Memberships.
- Arquitectura: monorepo con pnpm y Turborepo; API en NestJS, dashboard administrativo con React + Vite + Material UI, web publica con Next.js, paquetes compartidos de tipos y validacion con Zod.
- Decisiones documentadas en ADRs: multi-tenancy con esquema compartido, acceso basado en memberships, abstraccion `CurrentUserProvider`, creacion atomica de organizaciones y autenticacion con password + Bearer tokens.
- Stack planificado: TypeScript strict, PostgreSQL, Prisma, Redis, Docker Compose, Vitest, Jest y Playwright; app mobile futura con React Native y Expo.

### Prostagma AI Reports

Plugin WordPress de reportes de solo lectura sobre posts publicados (busqueda por palabra clave, periodo actual, agrupacion por categoria o autor y posts sin imagen destacada), con endpoint REST protegido por capability y nonce, y adaptador opcional al WordPress AI Client para generar resumenes. Si el cliente de IA no esta disponible, muestra un resumen local determinista.

- Periodo: julio 2026.
- Stack: PHP, WordPress REST API, WordPress AI Client, JavaScript vanilla.

### Prostagma landing

Landing estatica modular sin build: componentes ES modules, GSAP + ScrollTrigger con degradacion elegante y soporte de `prefers-reduced-motion`, canvas de particulas y demo de chatbot en vanilla JS.
