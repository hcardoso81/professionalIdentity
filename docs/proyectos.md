# Proyectos Profesionales

Este documento contiene el detalle de proyectos para usar como fuente de verdad en CV, LinkedIn, portfolio, entrevistas y prompts de IA.

## WordPress

### SEO Content Locker

Plugin personalizado para WordPress orientado a monetizacion, captacion de leads y control de acceso a contenido premium.

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

Detalles tecnicos:

El plugin esta organizado con una arquitectura cercana a capas. Los controladores AJAX delegan la logica a servicios como `LeadRegistrationService` y `LeadAccessService`, mientras que el acceso a base de datos queda encapsulado en repositorios como `LeadRepository` y `SameIpRepository`.

El flujo principal registra un lead, valida reCAPTCHA, verifica si el email ya tiene acceso activo, controla si la IP ya fue usada previamente, guarda el registro en la base de datos, consulta el pais de origen, sincroniza el contacto con Mailchimp y dispara eventos internos para logging y notificaciones.

Stack:

PHP, WordPress Plugin API, MySQL, JavaScript vanilla, AJAX, Mailchimp API v3, Google reCAPTCHA, WP_List_Table, wp_remote_request, wp_mail, shortcodes, hooks, nonces, custom database tables, CSV export.

Version corta:

Desarrolle un plugin WordPress personalizado para bloquear contenido SEO-friendly y capturar leads mediante email, con prueba gratuita temporal, control por IP, restauracion de sesiones, Google reCAPTCHA, integracion con Mailchimp, panel administrativo, exportacion CSV, logs y notificaciones automaticas.

### WP2LinkedIn

Plugin WordPress orientado a publicar manualmente entradas de WordPress en una pagina de empresa de LinkedIn.

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

Version corta:

Plugin administrativo liviano y especifico para conectar WordPress con una pagina de empresa de LinkedIn y publicar posts de forma controlada usando contenido personalizado desde ACF, OAuth, validacion de token, featured image e indicadores editoriales en el listado de posts.

### Welcome Popup Manager

Plugin personalizado para WordPress que permite administrar y mostrar un popup de bienvenida configurable en el frontend del sitio.

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

Stack:

PHP, WordPress Plugin API, hooks de WordPress, WP_Query, Advanced Custom Fields, Composer, PhpSpreadsheet, Select2, jQuery, CSS personalizado.

Version corta:

Plugin WordPress personalizado para mejorar la gestion editorial del backend, agregando filtros avanzados por etiquetas, integracion con filtros nativos y exportacion de posts filtrados a Excel. Desarrollado en PHP con WordPress Plugin API, Composer, PhpSpreadsheet, ACF y Select2, bajo una arquitectura modular por capas.

## React / TypeScript / Full Stack

### Portal Expensas Admins

Aplicacion web administrativa para la gestion integral de consorcios y expensas.

Resumen:

Permite operar modulos vinculados a administraciones, consorcios, unidades funcionales, empleados, sueldos, liquidaciones, pagos, proveedores, documentos y tickets internos de soporte mediante una interfaz orientada al trabajo diario de administracion.

Arquitectura:

El proyecto esta desarrollado con React, TypeScript y Material UI, utilizando MUI X DataGrid para vistas tabulares avanzadas, React Router para navegacion, i18next para internacionalizacion y Apollo GraphQL para comunicacion con backend.

La aplicacion sigue una arquitectura basada en Clean Architecture, CQRS y Presenter Pattern. Los componentes React consumen ViewModels y delegan acciones en presenters, mientras que las operaciones contra backend se canalizan mediante casos de uso, handlers, mappers y entidades de dominio.

Funcionalidades:

- Gestion de expensas.
- Liquidaciones.
- Prorrateos.
- Empleados y recibos.
- Cuentas corrientes.
- Pagos.
- Documentos.
- Tickets tipo Rocket.
- GraphQL subscriptions para actualizaciones en tiempo real en conversaciones y tickets.

Stack:

React, TypeScript, Material UI, MUI X DataGrid, React Router, i18next, Apollo GraphQL, GraphQL subscriptions, Clean Architecture, CQRS, Presenter Pattern.

Version corta:

Desarrollo y mantenimiento de una aplicacion administrativa React + TypeScript para gestion de expensas, consorcios, empleados, liquidaciones, pagos y soporte interno. Implementacion de Clean Architecture, CQRS y Presenter Pattern, integracion con Apollo GraphQL, subscriptions en tiempo real, Material UI, MUI DataGrid, React Router e i18next.

### News Kiosk

Plataforma web para la gestion, busqueda, analisis y visualizacion de articulos y noticias.

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

Asistente inteligente para torneos amateur de futbol que permite a participantes y organizadores consultar informacion en lenguaje natural directamente desde WhatsApp.

Resumen:

El sistema responde sobre inscripciones, reglas, sedes, fixture, resultados, tablas de posiciones, planteles, estadisticas de jugadores y rankings, combinando una base de conocimiento editable con datos en vivo de la API de CopaFacil.

Arquitectura:

La solucion esta construida con NestJS, TypeScript estricto, Node.js, Twilio WhatsApp API, Groq/OpenAI-compatible LLM API, Google Docs como CMS no-code y CopaFacil API.

La arquitectura modular separa canal de mensajeria, orquestacion conversacional, integracion con LLM, dominio de torneos, base documental y logging operativo.

Funcionalidades:

- Seleccion multi-torneo.
- Memoria de sesion.
- Normalizacion de consultas.
- Tolerancia a errores de escritura.
- Function calling/tools para consultar solo los datos necesarios.
- Auditoria de conversaciones en JSONL.
- Endpoints administrativos protegidos.
- Validacion de configuracion con Joi.
- Manejo global de errores.
- Seguridad HTTP basica con Helmet.

Stack:

NestJS, TypeScript, Node.js, Twilio WhatsApp API, Groq, OpenAI-compatible APIs, Google Docs, CopaFacil API, Joi, Helmet, JSONL logging.

Version corta:

Construi un asistente de IA por WhatsApp para torneos de futbol amateur, desarrollado con NestJS, TypeScript, Twilio, Groq/OpenAI-compatible APIs, Google Docs y CopaFacil API. El bot entiende consultas en lenguaje natural, gestiona multiples torneos, responde FAQs desde una base editable y consulta datos en vivo para fixture, resultados, posiciones, jugadores y rankings.

### CUTI - Corporate Conference Calls

Aplicacion mobile orientada a la gestion y participacion en conference calls corporativas, con foco en la interaccion entre empresas e inversores.

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
