# Prompt generico para plugins WordPress

Guia de trabajo para agentes IA en plugins WordPress personalizados.

Usar este documento como base para crear un `AGENTS.md` inicial en cualquier plugin nuevo. La guia prioriza arquitectura clara, seguridad WordPress, bootstrap liviano, separacion por capas, convenciones mantenibles y documentacion viva.

## Proyecto

Completar esta seccion al iniciar un plugin nuevo:

- Plugin:
- Entrada principal:
- Namespace:
- Text domain:
- Version:
- Objetivo:
- Shortcodes:
- CPTs:
- Opciones:
- Integraciones:
- Dependencias:

## Objetivo

Este repositorio contiene un plugin personalizado de WordPress.

El objetivo es mantener una arquitectura clara, segura, mantenible y extensible, evitando logica mezclada en el archivo principal del plugin.

Cada tarea debe respetar:

- Separacion de responsabilidades.
- Buenas practicas WordPress.
- Codigo orientado a objetos cuando aporte claridad.
- Seguridad: sanitizacion, escaping, nonces y permisos.
- Cambios pequenos, revisables y compatibles.
- Documentacion actualizada.

## Reglas generales de trabajo

Antes de modificar codigo:

1. Revisar la estructura existente.
2. Ejecutar o revisar `git status --short` si es posible.
3. No revertir cambios locales del usuario.
4. Mantener el cambio acotado al pedido.
5. No introducir frameworks, Composer o dependencias externas sin confirmacion.
6. No cambiar slugs, nombres de opciones, CPTs, meta keys o campos ACF existentes sin plan de compatibilidad o migracion.

Al finalizar cada tarea:

1. Sugerir un mensaje de commit convencional.
2. Actualizar `README.md` si cambio el comportamiento publico, instalacion, configuracion o uso.
3. Actualizar `AGENTS.md` si se agregaron reglas, arquitectura, convenciones o flujos nuevos.
4. Indicar archivos modificados y validaciones recomendadas.
5. Proponer tests manuales cuando no exista suite automatica.

Ejemplos de commit:

```bash
feat(admin): add filtered CSV export
fix(security): validate nonce before deleting lead
refactor(domain): extract popup display rules
docs: update plugin setup instructions
```

## Stack base

- PHP.
- WordPress Plugin API.
- JavaScript o jQuery solo cuando sea necesario.
- HTML/CSS para vistas admin o frontend.
- ACF opcional, si el plugin lo requiere.
- Composer opcional, solo si el proyecto ya lo usa o se confirma su incorporacion.

## Estructura recomendada

```text
plugin-name/
|-- plugin-name.php
|-- AGENTS.md
|-- README.md
|-- composer.json
|-- autoload.php
|-- bootstrap/
|   |-- admin.php
|   |-- public.php
|   `-- plugin.php
|-- src/
|   |-- Bootstrap/
|   |-- Domain/
|   |   |-- Model/
|   |   |-- Service/
|   |   |-- Repository/
|   |   `-- Support/
|   |-- Infrastructure/
|   |   |-- WordPress/
|   |   |-- Persistence/
|   |   |-- Http/
|   |   `-- Logging/
|   |-- UI/
|   |   |-- Admin/
|   |   `-- Frontend/
|   `-- Application/
|-- admin/
|   |-- assets/
|   `-- views/
|-- public/
|   |-- assets/
|   `-- views/
|-- templates/
|-- assets/
`-- logs/
```

No todas las carpetas son obligatorias. Crear solo lo que el plugin necesite.

## Archivo principal del plugin

El archivo principal debe ser liviano.

Responsabilidades permitidas:

- Header del plugin.
- Proteccion `ABSPATH`.
- Definicion de constantes.
- Carga de autoload/bootstrap.
- Registro de hooks de activacion/desactivacion.
- Delegar el arranque a una clase `Plugin`, `Bootstrap` o archivo bootstrap.

Ejemplo:

```php
<?php
/**
 * Plugin Name: Plugin Name
 * Description: Plugin description.
 * Version: 1.0.0
 * Author: Author Name
 * Text Domain: plugin-name
 */

declare(strict_types=1);

if (!defined('ABSPATH')) {
    exit;
}

define('PLUGIN_NAME_VERSION', '1.0.0');
define('PLUGIN_NAME_PATH', plugin_dir_path(__FILE__));
define('PLUGIN_NAME_URL', plugin_dir_url(__FILE__));

require_once PLUGIN_NAME_PATH . 'autoload.php';

PluginVendor\PluginName\Bootstrap\Plugin::boot();
```

No poner logica de negocio pesada en este archivo.

## Namespaces y nombres

Usar un namespace base claro:

```php
PluginVendor\PluginName
```

Ejemplos:

```php
PluginVendor\PluginName\Domain\Service
PluginVendor\PluginName\Infrastructure\WordPress
PluginVendor\PluginName\UI\Admin
PluginVendor\PluginName\UI\Frontend
```

Convenciones:

- Clases en `PascalCase`.
- Metodos en `camelCase`.
- Constantes en `UPPER_SNAKE_CASE`.
- Hooks, options, nonces, AJAX actions y handles con prefijo unico del plugin.
- Evitar strings repetidos: usar constantes para slugs, post types, option names y action names.

## Autoload

Preferir Composer PSR-4 si el proyecto ya lo usa.

```json
{
  "autoload": {
    "psr-4": {
      "PluginVendor\\PluginName\\": "src/"
    }
  }
}
```

Si no hay Composer, usar autoload simple PSR-4 propio.

No mezclar includes manuales por todos lados. Centralizar carga en `autoload.php` o bootstrap.

## Capas

### Domain

Contiene reglas de negocio y modelos simples.

Debe evitar llamadas directas a WordPress cuando sea posible.

Puede contener:

- Models.
- Value Objects.
- Services de negocio.
- Criteria.
- Interfaces de repositorios.
- Helpers puros.

No deberia depender de:

- `$_GET`, `$_POST`, `$_COOKIE`.
- `$wpdb`.
- HTML.
- Hooks WordPress.

### Application

Orquesta casos de uso.

Ejemplos:

- Registrar lead.
- Exportar datos.
- Publicar contenido.
- Generar HTML.
- Procesar accion administrativa.

Debe coordinar servicios, repositorios e infraestructura.

### Infrastructure

Contiene adaptadores tecnicos.

Ejemplos:

- Repositorios `$wpdb`.
- Integraciones HTTP externas.
- Wrappers de WordPress.
- Loggers.
- Registro de CPTs.
- Registro de ACF.
- Migraciones o instalacion de tablas.

### UI/Admin

Contiene pantallas, formularios, tablas, columnas, acciones admin y assets del administrador.

Reglas:

- Cargar assets solo en pantallas necesarias.
- Verificar capacidades.
- Verificar nonces.
- Escapar siempre la salida.
- Mantener vistas en archivos separados si el HTML crece.

### UI/Frontend

Contiene shortcodes, render publico, templates, assets frontend y AJAX publico.

Reglas:

- No cargar assets globalmente si no hacen falta.
- Validar nonces en AJAX.
- Sanitizar inputs del usuario.
- Responder con `wp_send_json_success()` o `wp_send_json_error()`.

## Bootstrap

Cada clase que registre hooks debe tener un metodo claro:

```php
public function registerHooks(): void
{
    add_action('init', [$this, 'register']);
}
```

El bootstrap instancia servicios y llama `registerHooks()`.

Ejemplo:

```php
final class Plugin
{
    public static function boot(): void
    {
        $plugin = new self();
        $plugin->registerHooks();
    }

    public function registerHooks(): void
    {
        if (is_admin()) {
            (new Admin\AdminAssets())->registerHooks();
            (new Admin\SettingsPage())->registerHooks();
        }

        (new Frontend\Shortcode())->registerHooks();
    }
}
```

## Seguridad WordPress

Siempre aplicar:

Proteccion directa:

```php
if (!defined('ABSPATH')) {
    exit;
}
```

Sanitizacion:

- `sanitize_text_field()`
- `sanitize_email()`
- `sanitize_key()`
- `sanitize_title()`
- `esc_url_raw()`
- `absint()`
- `intval()`
- `wp_unslash()`

Escaping:

- `esc_html()`
- `esc_attr()`
- `esc_url()`
- `wp_kses_post()`

Nonces para admin actions:

```php
check_admin_referer('action_name');
```

Nonces para AJAX:

```php
check_ajax_referer('action_name', 'nonce');
```

Permisos:

- `current_user_can('manage_options')`
- `current_user_can('edit_post', $postId)`
- `current_user_can('edit_posts')`

SQL:

```php
$wpdb->prepare()
```

Toda query con datos externos debe usar `$wpdb->prepare()`.

## AJAX y admin-post

Para AJAX:

1. Validar nonce.
2. Validar permisos si corresponde.
3. Sanitizar payload.
4. Delegar logica a servicio.
5. Responder JSON.

Para `admin-post.php`:

1. Usar action names con prefijo.
2. Validar nonce.
3. Validar capability.
4. Sanitizar request.
5. Redirigir con `wp_safe_redirect()` cuando corresponda.

## ACF

Si se usa ACF:

- Registrar field groups de forma local cuando sea posible.
- Encapsular lectura en helper o service.
- Prever fallback si ACF no esta activo.
- No renombrar campos existentes sin compatibilidad.
- Documentar fields relevantes en `AGENTS.md`.

Ejemplo:

```php
if (function_exists('get_field')) {
    $value = get_field('field_name', $postId);
}
```

## CPTs, taxonomias y rewrite rules

Si se agregan CPTs:

- Usar constantes para slugs.
- Registrar en infraestructura.
- No hacer `flush_rewrite_rules()` en cada request.
- Hacer flush solo en activacion/desactivacion.

## Assets

Usar handles con prefijo del plugin.

```php
wp_enqueue_script(
    'plugin-name-admin',
    PLUGIN_NAME_URL . 'assets/js/admin.js',
    ['jquery'],
    PLUGIN_NAME_VERSION,
    true
);
```

Reglas:

- Admin assets solo en pantallas necesarias.
- Frontend assets solo cuando el shortcode, template o feature se usa.
- Usar `wp_localize_script()` o `wp_add_inline_script()` para pasar datos de PHP a JS.
- No hardcodear URLs si pueden venir de WordPress.

## Logs

Si el plugin usa logs:

- Guardarlos en `logs/`.
- No commitear `.log`.
- No loguear secretos, tokens, passwords ni payloads sensibles.
- Incluir contexto util: `post_id`, `user_id`, `status`, `http_code`, `action`.
- Usar niveles: `info`, `warning`, `error`, `exception`.

## Configuracion

Preferir constantes para:

- `PLUGIN_NAME_VERSION`
- `PLUGIN_NAME_PATH`
- `PLUGIN_NAME_URL`
- `PLUGIN_NAME_BASENAME`
- `PLUGIN_NAME_TEXT_DOMAIN`

Para opciones:

- `plugin_name_settings`
- `plugin_name_api_key`
- `plugin_name_enabled`

Encapsular defaults en una clase de settings.

## Internacionalizacion

Todo texto visible debe usar el text domain del plugin.

```php
__('Text', 'plugin-name')
esc_html__('Text', 'plugin-name')
```

## Validacion recomendada

Para PHP:

```bash
php -l plugin-name.php
php -l src/Path/File.php
```

Si hay Composer:

```bash
composer dump-autoload
composer install
```

Si hay JavaScript o CSS, validar manualmente o con herramientas disponibles.

## README.md

Actualizar `README.md` cuando cambie:

- Instalacion.
- Configuracion.
- Shortcodes.
- Hooks publicos.
- Pantallas admin.
- Opciones.
- Flujo funcional.
- Dependencias.
- Requisitos.
- Uso de ACF.
- Acciones AJAX/admin-post.
- Migraciones o tablas.

## AGENTS.md

Actualizar `AGENTS.md` cuando se agregue:

- Nueva capa.
- Nueva convencion.
- Nuevo flujo importante.
- Nueva integracion externa.
- Nuevo CPT, shortcode, AJAX action o admin-post action.
- Nueva dependencia.
- Nueva regla de seguridad o compatibilidad.

## Commit convencional

Cada respuesta final debe incluir una sugerencia de commit.

Formato:

```text
type(scope): description
```

Tipos sugeridos:

- `feat`
- `fix`
- `refactor`
- `docs`
- `style`
- `test`
- `chore`
- `perf`
- `security`

Ejemplos:

```text
feat(admin): add settings page for popup rules
fix(ajax): validate nonce before saving lead
refactor(domain): extract lead access rules
docs(readme): document shortcode usage
security(admin): escape settings output
```

## Configuracion recomendada VS Code

Crear `.vscode/settings.json`:

```json
{
  "intelephense.stubs": [
    "wordpress",
    "Core",
    "standard",
    "date",
    "pcre",
    "session",
    "json",
    "filter"
  ],
  "php.suggest.basic": false,
  "php.validate.enable": true,
  "files.associations": {
    "*.php": "php"
  }
}
```

## Principios finales

- El archivo principal coordina, no implementa.
- Las clases deben tener una responsabilidad clara.
- El dominio no debe saber demasiado de WordPress.
- WordPress debe quedar encapsulado en infraestructura, admin o frontend.
- La seguridad no es opcional.
- No repetir strings criticos.
- No romper compatibilidad con datos existentes.
- Documentar cada feature nueva.
- Sugerir siempre un commit convencional al terminar.
