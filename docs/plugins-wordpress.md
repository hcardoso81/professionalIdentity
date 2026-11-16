# Prompt generico para plugins WordPress

Guia de trabajo para agentes IA en plugins WordPress personalizados.

Version de la guia: 2026-11-07

Usar este documento como referencia para redactar un `AGENTS.md` corto en cualquier plugin nuevo. La guia prioriza arquitectura clara, seguridad WordPress, bootstrap liviano, separacion por capas, convenciones mantenibles y documentacion viva.

La estructura propuesta es una referencia maxima, no una obligacion. Para plugins pequenos, priorizar claridad, seguridad WordPress y bajo costo de mantenimiento. Escalar hacia capas de dominio, aplicacion e infraestructura cuando exista logica de negocio real, integraciones externas, workflows complejos o necesidad de testing aislado.

## Uso con agentes IA

- Claude Code carga automaticamente `CLAUDE.md`, no `AGENTS.md`. En cada plugin crear un `CLAUDE.md` minimo que importe el otro archivo con una linea `@AGENTS.md`. Asi Claude Code, Codex y otros agentes leen las mismas reglas.
- `AGENTS.md` se carga completo en cada sesion. Mantenerlo corto (idealmente menos de 200 lineas) y especifico del plugin: seccion `Proyecto`, reglas criticas y decisiones propias.
- Esta guia no se copia dentro de `AGENTS.md`: guardarla sin editar en `docs/plugins-wordpress.md` del plugin y referenciarla desde `AGENTS.md` para que el agente la lea cuando la tarea lo requiera. Comparar `Version de la guia` con la original para detectar copias viejas.
- Si una regla de esta guia no aplica a un plugin puntual, dejarlo explicito en `AGENTS.md` en lugar de borrarla silenciosamente.

## Proyecto

Completar esta seccion al iniciar un plugin nuevo:

- Plugin:
- Entrada principal:
- Namespace:
- Prefijo (funciones, hooks, options, handles):
- Text domain:
- Version:
- Requiere WordPress (minimo):
- Requiere PHP (minimo):
- Plugins requeridos:
- Objetivo:
- Shortcodes:
- CPTs y taxonomias:
- Tablas propias:
- Opciones:
- AJAX / admin-post / REST:
- Cron jobs:
- Integraciones:
- Datos personales (que se guarda, para que, por cuanto tiempo y a que terceros se envia):
- Dependencias:
- Repositorio y visibilidad:
- Entorno local (URL, ruta PHP, WP-CLI disponible):
- Comandos de validacion:

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
5. No introducir frameworks ni dependencias de produccion sin confirmacion. Composer se permite sin consulta solo como dependencia de desarrollo (`require-dev`) para PHPCS y PHPUnit.
6. No cambiar slugs, nombres de opciones, CPTs, meta keys, tablas o campos ACF existentes sin plan de compatibilidad o migracion.
7. Ante decisiones que afecten datos persistentes (borrado, migraciones, renombres), consultar antes de implementar.

Al finalizar cada tarea:

1. Sugerir un mensaje de commit convencional. No ejecutar `git commit` ni `git push` salvo pedido explicito.
2. Actualizar `README.md` si cambio el comportamiento publico, instalacion, configuracion o uso.
3. Actualizar `AGENTS.md` si se agregaron reglas, arquitectura, convenciones o flujos nuevos.
4. Indicar archivos modificados y validaciones ejecutadas (o recomendadas si no se pudieron ejecutar).
5. Proponer tests manuales cuando no exista suite automatica.
6. Repasar el `Checklist de cierre`.

## Stack base

- PHP 8.3 o superior, salvo que el hosting real del cliente exija otra version: definirla en `Proyecto` y validar con esa misma version. No usar como minimo de un plugin nuevo una version sin soporte de seguridad.
- WordPress Plugin API.
- JavaScript o jQuery solo cuando sea necesario.
- HTML/CSS para vistas admin o frontend.
- ACF opcional, si el plugin lo requiere.
- Composer para herramientas de desarrollo. Dependencias de produccion solo si el proyecto ya las usa o se confirma su incorporacion.

## Estructura recomendada

```text
plugin-name/
|-- plugin-name.php
|-- uninstall.php
|-- AGENTS.md
|-- CLAUDE.md
|-- README.md
|-- CHANGELOG.md
|-- composer.json
|-- phpcs.xml.dist
|-- phpunit.xml.dist
|-- .gitattributes
|-- .github/workflows/ci.yml
|-- autoload.php
|-- src/
|   |-- Bootstrap/
|   |   |-- Plugin.php
|   |   |-- Activator.php
|   |   `-- Deactivator.php
|   |-- Domain/
|   |   |-- Model/
|   |   |-- Service/
|   |   |-- Repository/
|   |   `-- Support/
|   |-- Application/
|   |-- Infrastructure/
|   |   |-- WordPress/
|   |   |-- Persistence/
|   |   |-- Http/
|   |   `-- Logging/
|   `-- UI/
|       |-- Admin/
|       |-- Frontend/
|       `-- Rest/
|-- templates/
|   |-- admin/
|   `-- public/
|-- assets/
|   |-- admin/
|   `-- public/
|-- languages/
`-- tests/
```

Reglas de ubicacion:

- Clases PHP siempre en `src/`, nunca en `templates/` ni `assets/`.
- Vistas HTML/PHP en `templates/admin` o `templates/public`.
- CSS, JS e imagenes en `assets/admin` o `assets/public`.
- No crear carpetas paralelas (`admin/`, `public/`, `bootstrap/`) que dupliquen estas responsabilidades.

No todas las carpetas son obligatorias. Crear solo lo que el plugin necesite.

Para plugins pequenos se puede iniciar con una estructura mas simple:

```text
plugin-name/
|-- plugin-name.php
|-- AGENTS.md
|-- CLAUDE.md
|-- README.md
|-- autoload.php
|-- src/
|   |-- Bootstrap/
|   |-- Admin/
|   |-- Frontend/
|   `-- Support/
|-- templates/
|-- assets/
|-- CHANGELOG.md
|-- composer.json
|-- phpcs.xml.dist
|-- .gitattributes
`-- .github/workflows/ci.yml
```

Cuando el plugin crezca, `src/Admin` y `src/Frontend` migran a `src/UI/Admin` y `src/UI/Frontend`, y la logica de negocio que haya en ellos se extrae a `Domain` o `Application`. Documentar en `AGENTS.md` cual de las dos estructuras usa el plugin.

El objetivo no es demostrar arquitectura, sino construir plugins mantenibles, seguros y faciles de evolucionar. La arquitectura debe justificar su costo: separar capas cuando reduzca acoplamiento real, facilite testing o permita cambiar infraestructura sin tocar reglas de negocio.

Criterios para elegir:

- Estructura simple: sin integraciones externas ni reglas de negocio propias.
- Agregar `Domain`: hay reglas que conviene probar sin WordPress.
- Agregar `Application`: hay flujos con varios pasos o varias entradas (admin, cron, REST).
- Ninguna clase o vista deberia superar 400 lineas: dividir por responsabilidad.

## Archivo principal del plugin

El archivo principal debe ser liviano.

Responsabilidades permitidas:

- Header del plugin.
- Proteccion `ABSPATH`.
- Definicion de constantes.
- Carga de autoload.
- Registro de hooks de activacion/desactivacion (deben registrarse aca, con `__FILE__`).
- Delegar el arranque a la clase `Plugin` en `plugins_loaded`.

Ejemplo:

```php
<?php
/**
 * Plugin Name:       Plugin Name
 * Description:       Plugin description.
 * Version:           1.0.0
 * Requires at least: 6.4
 * Requires PHP:      8.3
 * Author:            Hernan Cardoso
 * Author URI:        https://www.linkedin.com/in/cardosohernan/
 * License:           GPL-2.0-or-later
 * License URI:       https://www.gnu.org/licenses/gpl-2.0.html
 * Text Domain:       plugin-name
 * Domain Path:       /languages
 *
 * CV online: https://hcardoso81.github.io/professionalIdentity/
 */

declare(strict_types=1);

if (!defined('ABSPATH')) {
    exit;
}

define('MY_PLUGIN_VERSION', '1.0.0');
define('MY_PLUGIN_FILE', __FILE__);
define('MY_PLUGIN_PATH', plugin_dir_path(__FILE__));
define('MY_PLUGIN_URL', plugin_dir_url(__FILE__));
define('MY_PLUGIN_BASENAME', plugin_basename(__FILE__));

require_once MY_PLUGIN_PATH . 'autoload.php';

register_activation_hook(__FILE__, [PluginVendor\PluginName\Bootstrap\Activator::class, 'activate']);
register_deactivation_hook(__FILE__, [PluginVendor\PluginName\Bootstrap\Deactivator::class, 'deactivate']);

add_action('plugins_loaded', [PluginVendor\PluginName\Bootstrap\Plugin::class, 'boot']);
```

Notas:

- `CV online` no es un header reconocido por WordPress; se ignora y queda solo como comentario.
- Si el plugin depende de otro plugin publicado en wordpress.org (por ejemplo ACF), agregar `Requires Plugins: advanced-custom-fields` (WordPress 6.5+).
- No poner logica de negocio pesada en este archivo.
- Reemplazar `MY_PLUGIN` por un prefijo real del plugin. Evitar copiar nombres genericos como constantes finales del proyecto.

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

- Clases en `PascalCase`, un archivo por clase con el mismo nombre (`Plugin.php` contiene `Plugin`).
- Metodos en `camelCase`.
- Constantes en `UPPER_SNAKE_CASE`.
- Hooks, options, meta keys, nonces, AJAX actions, cron events, handles, tablas, shortcodes, constantes y funciones globales con prefijo unico del plugin.
- El codigo nuevo va en clases con namespace. Evitar funciones globales: un nombre generico como `get_ip()` puede causar un error fatal si otro plugin lo declara.
- Evitar strings repetidos: usar constantes de clase para slugs, post types, option names y action names.
- Si el plugin expone hooks propios para extension, usar el prefijo (`plugin_name_before_save`) y documentarlos en `README.md`.

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

Si no hay Composer, usar este autoload PSR-4 propio en `autoload.php`:

```php
<?php

declare(strict_types=1);

if (!defined('ABSPATH')) {
    exit;
}

spl_autoload_register(static function (string $class): void {
    $prefix = 'PluginVendor\\PluginName\\';

    if (strncmp($class, $prefix, strlen($prefix)) !== 0) {
        return;
    }

    $file = __DIR__ . '/src/' . str_replace('\\', '/', substr($class, strlen($prefix))) . '.php';

    if (is_readable($file)) {
        require_once $file;
    }
});
```

Con Composer, `autoload.php` solo hace `require_once __DIR__ . '/vendor/autoload.php';` y falla de forma controlada (aviso en admin) si `vendor/` no existe.

No mezclar includes manuales por todos lados. Centralizar carga en `autoload.php`.

Si el plugin se distribuye a sitios de terceros con librerias Composer populares (por ejemplo PhpSpreadsheet), considerar prefijar dependencias con Strauss o PHP-Scoper para evitar conflictos de versiones con otros plugins.

## Capas

### Regla de dependencias

`UI -> Application -> Domain`. `Infrastructure` implementa los detalles tecnicos.

- `Domain` no depende de ninguna otra capa ni de WordPress.
- `Application` no usa `$wpdb`, superglobales ni HTML.
- Crear una interfaz solo si hay una integracion externa, mas de una implementacion o necesidad real de sustituirla en tests.

### Domain

Contiene reglas de negocio y modelos simples.

Debe evitar dependencias directas de WordPress cuando sea razonable. Si el plugin es pequeno, priorizar claridad sobre abstraccion excesiva.

Puede contener:

- Models.
- Value Objects.
- Services de negocio.
- Criteria.
- Interfaces de repositorios.
- Helpers puros.

No deberia depender de:

- `$_GET`, `$_POST`, `$_COOKIE`, `$_FILES`.
- `$wpdb`.
- HTML.
- Hooks WordPress.

### Application

Orquesta casos de uso.

Ejemplos:

- Registrar lead.
- Exportar datos.
- Publicar contenido.
- Importar archivo.
- Procesar accion administrativa.

Debe coordinar servicios, repositorios e infraestructura. Recibe datos ya sanitizados y devuelve resultados o DTOs; no genera HTML ni lee superglobales.

### Infrastructure

Contiene adaptadores tecnicos.

Ejemplos:

- Repositorios `$wpdb`.
- Integraciones HTTP externas (`wp_remote_get()`, `wp_remote_post()` con timeout explicito).
- Wrappers de WordPress.
- Loggers.
- Registro de CPTs y taxonomias.
- Registro de ACF.
- Migraciones o instalacion de tablas.

### UI/Admin

Contiene pantallas, formularios, tablas, columnas, acciones admin y assets del administrador.

Reglas:

- Cargar assets solo en pantallas necesarias.
- Verificar capacidades.
- Verificar nonces.
- Escapar siempre la salida.
- Mantener vistas en `templates/admin` si el HTML crece.
- No mostrar avisos de otros plugins, del tema ni de WordPress en las pantallas propias del plugin: le sacan el foco a la pantalla.

Patron para ocultar avisos ajenos:

```php
add_action('in_admin_header', [$this, 'hideForeignNotices'], PHP_INT_MAX);

public function hideForeignNotices(): void
{
    if (! $this->isPluginScreen()) {
        return;
    }

    foreach (['admin_notices', 'all_admin_notices', 'network_admin_notices', 'user_admin_notices'] as $hook) {
        remove_all_actions($hook);
    }
}
```

- Aplicarlo solo en las pantallas del plugin (comparar `get_current_screen()`), nunca de forma global: en el resto del admin los avisos deben seguir visibles.
- Debe correr al final de `in_admin_header`, justo antes de que WordPress imprima los avisos, para incluir los registrados tarde.
- Los avisos propios no deben usar esos hooks: imprimirlos dentro de la vista del plugin. Los mensajes nativos de una pantalla de CPT ("Entrada actualizada") no los usan y se siguen mostrando.
- Algunos plugins imprimen avisos fuera de esos hooks (por ejemplo en `admin_print_footer_scripts`) y el JavaScript del admin los mueve junto al titulo. Para esos casos sumar un respaldo CSS en una hoja que cargue solo en las pantallas del plugin:

```css
.wrap > :is(.notice, .updated, .error, .update-nag):not(#message, #notice, #lost-connection-notice, #local-storage-notice) {
    display: none;
}
```

- Si la vista del plugin imprime avisos propios, excluir tambien su selector de esa regla.
- Comprobar la pantalla en el navegador. Los overlays y punteros de otros plugins no quedan cubiertos: resolverlos solo si molestan.

Avisos despues de una accion:

- Guardar el resultado en un transient por usuario, no en la URL: un link armado podria mostrarle texto falso a un administrador.
- Leerlo una sola vez y borrarlo al mostrarlo.

### UI/Frontend

Contiene shortcodes, render publico, templates, assets frontend y AJAX publico.

Reglas:

- No cargar assets globalmente si no hacen falta.
- Validar nonces en AJAX.
- Sanitizar inputs del usuario.
- Responder con `wp_send_json_success()` o `wp_send_json_error()`.
- Los shortcodes deben retornar el HTML, nunca hacer `echo`.

### UI/Rest

Contiene controladores REST (`register_rest_route()`). Ver seccion `AJAX, admin-post y REST API`.

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
    private static bool $booted = false;

    public static function boot(): void
    {
        if (self::$booted) {
            return;
        }

        self::$booted = true;
        (new self())->registerHooks();
    }

    public function registerHooks(): void
    {
        (new Installer())->registerHooks();
        (new Ajax\LeadController())->registerHooks();

        if (is_admin()) {
            (new Admin\AdminAssets())->registerHooks();
            (new Admin\SettingsPage())->registerHooks();
        }

        (new Frontend\Shortcode())->registerHooks();
    }
}
```

Reglas:

- `is_admin()` devuelve `true` tambien en requests a `admin-ajax.php`. Registrar handlers `wp_ajax_*` y `wp_ajax_nopriv_*` fuera de condiciones `is_admin()` / `!is_admin()` para evitar que dejen de funcionar.
- `is_admin()` no es un control de permisos: siempre verificar `current_user_can()`.
- No ejecutar trabajo pesado ni llamar funciones de traduccion durante el boot; registrar hooks y diferir el trabajo a `init`, `admin_menu`, `rest_api_init`, etc.

## Ciclo de vida

Usar hooks de ciclo de vida solo para tareas propias de instalacion, limpieza o compatibilidad.

Activation:

- Debe ser idempotente y nunca borrar datos: reactivar un plugin no puede cambiar datos existentes.
- Crear tablas personalizadas si aplica.
- Guardar defaults iniciales.
- Registrar roles o capabilities si el plugin los necesita.
- Hacer `flush_rewrite_rules()` solo si hay CPTs, taxonomias o rewrite rules (registrandolos antes del flush).

Deactivation:

- Limpiar cron jobs registrados por el plugin.
- Hacer `flush_rewrite_rules()` si el plugin registro CPTs, taxonomias o rewrite rules.
- No borrar datos persistentes del usuario.

Uninstall:

- Borrar opciones, tablas o archivos solo si el comportamiento esta documentado.
- Nunca borrar datos del usuario sin confirmacion clara o setting explicito (por ejemplo `plugin_name_delete_data_on_uninstall`).
- `uninstall.php` es obligatorio si el plugin guarda tablas, opciones o archivos, aunque decida conservarlos: debe documentar que borra y que no.
- Validar al inicio `if (!defined('WP_UNINSTALL_PLUGIN')) { exit; }`.

Actualizaciones y migraciones:

- `register_activation_hook()` no se ejecuta al actualizar el plugin. Guardar la version del esquema en una opcion (`plugin_name_db_version`) y compararla en `plugins_loaded` para correr migraciones pendientes.
- Las migraciones deben ser idempotentes.
- Crear o alterar tablas con `dbDelta()` (respetando su formato estricto) y nombres con `$wpdb->prefix`.

Multisite:

- Si el plugin puede activarse en red, contemplar que las tablas y opciones son por sitio. Documentar en `AGENTS.md` si el plugin no soporta multisite.

## WP-Cron

Si el plugin usa cron jobs:

- Registrar eventos solo si no existen (`wp_next_scheduled()`).
- Usar action names con prefijo unico del plugin.
- Limpiar eventos en deactivation (`wp_clear_scheduled_hook()`).
- No ejecutar tareas pesadas en cada request.
- Procesar el trabajo largo por lotes, con un lock contra ejecuciones superpuestas.
- Delegar la tarea programada a un servicio o caso de uso.
- Loguear errores relevantes sin exponer datos sensibles.
- WP-Cron depende de visitas; si la tarea es critica, documentar el uso de un cron real del sistema.

## Settings y options

Para pantallas de configuracion:

- Usar Settings API cuando sea razonable.
- Sanitizar opciones con callbacks especificos (`sanitize_callback` en `register_setting()`).
- Definir defaults centralizados.
- No leer `get_option()` disperso por todo el codigo.
- Encapsular acceso a opciones en una clase de settings/configuracion.
- Preferir una sola opcion serializada (`plugin_name_settings`) antes que muchas opciones sueltas.
- Opciones grandes o de uso poco frecuente: guardarlas con autoload desactivado.
- Secretos (API keys, tokens): preferir constantes en `wp-config.php` y usar la opcion solo como fallback. Nunca mostrarlos completos en pantalla.
- El formulario nunca reimprime un secreto, ni siquiera en un campo `password`: dejar el campo vacio y conservar el valor actual si no se envia uno nuevo.

## Seguridad WordPress

Siempre aplicar:

Proteccion directa en todo archivo PHP:

```php
if (!defined('ABSPATH')) {
    exit;
}
```

Sanitizacion de entrada:

- `sanitize_text_field()`
- `sanitize_textarea_field()`
- `sanitize_email()`
- `sanitize_key()`
- `sanitize_title()`
- `sanitize_file_name()`
- `esc_url_raw()`
- `absint()`
- `intval()`
- `wp_kses_post()` / `wp_kses()` para HTML permitido
- `wp_unslash()` antes de sanitizar superglobales

Requests:

Patron estandar para leer `$_POST`, `$_GET` o `$_REQUEST`:

```php
$name = isset($_POST['name']) ? sanitize_text_field(wp_unslash($_POST['name'])) : '';
$id   = isset($_POST['id']) ? absint($_POST['id']) : 0;
$ids  = isset($_POST['ids']) ? array_map('absint', (array) wp_unslash($_POST['ids'])) : [];
```

- Validar siempre existencia, tipo esperado, nonce y permisos antes de usar o guardar.
- WordPress agrega slashes a las superglobales: siempre `wp_unslash()` antes de sanitizar.
- No usar `filter_input()`: lee el request original (sin los slashes de WordPress, por lo que `wp_unslash()` corromperia backslashes legitimos) y no ve valores asignados a `$_POST` en tests.
- Para los falsos positivos de Intelephense con `$_POST`, corregir la configuracion del editor (ver `Configuracion recomendada VS Code`), no el codigo.

Escaping de salida (escapar lo mas tarde posible, en el momento de imprimir):

- `esc_html()`
- `esc_attr()`
- `esc_url()`
- `esc_textarea()`
- `esc_js()` (preferir `wp_json_encode()` para datos)
- `wp_kses_post()`
- Variantes traducidas: `esc_html__()`, `esc_attr__()`, `esc_html_e()`.

Nonces:

```php
wp_nonce_field('plugin_name_save_settings');            // formulario
check_admin_referer('plugin_name_save_settings');        // admin / admin-post
check_ajax_referer('plugin_name_save_lead', 'nonce');    // AJAX
```

Un nonce no es autorizacion: siempre combinarlo con `current_user_can()`. En AJAX publico (`nopriv`) el nonce protege contra CSRF pero no autentica: aplicar validaciones, y rate limiting obligatorio si el endpoint consulta datos, escribe o llama a un servicio externo. La respuesta no debe revelar si un email u otro dato existe. Tener en cuenta que el cache de pagina puede servir nonces vencidos.

Permisos:

- `current_user_can('manage_options')`
- `current_user_can('edit_post', $postId)`
- `current_user_can('edit_posts')`
- Preferir capabilities propias o especificas antes que chequear roles.

Redirecciones:

- Usar `wp_safe_redirect()` seguido de `exit`.

### Uploads y archivos importados

Para formularios de carga de archivos en admin:

- Validar capability antes de procesar el request.
- Validar nonce con `check_admin_referer()`.
- No confiar en el nombre original del archivo.
- Validar extension y MIME con `wp_check_filetype_and_ext()`.
- Usar `wp_handle_upload()` (con `'test_form' => false`) o un mecanismo WordPress equivalente.
- Definir un allowlist explicito de extensiones y MIME types.
- Tratar errores de `$_FILES` antes de leer el archivo.
- Eliminar archivos temporales/importados cuando ya no sean necesarios con `wp_delete_file()`.
- No imprimir rutas absolutas ni detalles internos de errores al usuario final.
- Sanitizar todo valor leido desde archivos antes de usarlo en dominio o base de datos.

Para imports Excel:

- Usar una libreria mantenida como PhpSpreadsheet mediante Composer cuando el proyecto lo permita.
- Si la dependencia no esta instalada, fallar de forma controlada y documentar `composer install`.
- Validar columnas requeridas antes de procesar filas.
- Ignorar filas incompletas o con valores no reconocidos, registrando un resumen claro.
- Normalizar datos antes de persistirlos.
- Persistir conteos como enteros no negativos.
- Para archivos grandes, procesar por lotes y contemplar limites de memoria y tiempo de ejecucion.

### Exportaciones CSV

- Exigir capability y nonce.
- Neutralizar formulas: anteponer `'` a las celdas que empiecen con `=`, `+`, `-`, `@`, tab o CR.
- No mostrar mensajes de excepcion al usuario.

### Datos personales

Aplica a emails, IPs, nombres y cualquier dato que identifique a una persona.

- Documentar en `AGENTS.md` que datos se guardan, para que, por cuanto tiempo y a que terceros se envian.
- Si hay consentimiento, guardar la fecha y la version del texto aceptado.
- Nunca reactivar en un servicio externo a un contacto dado de baja.
- Enviar a un tercero solo lo necesario y por HTTPS.
- Integrar los exportadores y borradores de datos personales de WordPress (`wp_privacy_personal_data_exporters` y `wp_privacy_personal_data_erasers`).

## AJAX, admin-post y REST API

Para AJAX:

1. Validar nonce.
2. Validar permisos si corresponde.
3. Sanitizar payload.
4. Delegar logica a servicio.
5. Responder JSON con `wp_send_json_success()` / `wp_send_json_error()` y codigo HTTP adecuado.

Para `admin-post.php`:

1. Usar action names con prefijo.
2. Validar nonce.
3. Validar capability.
4. Sanitizar request.
5. Redirigir con `wp_safe_redirect()` + `exit`.

Para REST API (preferible para integraciones, consumo desde JS moderno o bloques):

```php
add_action('rest_api_init', function (): void {
    register_rest_route('plugin-name/v1', '/items', [
        'methods'             => WP_REST_Server::CREATABLE,
        'callback'            => [$this, 'createItem'],
        'permission_callback' => static fn (): bool => current_user_can('edit_posts'),
        'args'                => [
            'title' => [
                'type'              => 'string',
                'required'          => true,
                'sanitize_callback' => 'sanitize_text_field',
            ],
        ],
    ]);
});
```

- `permission_callback` es obligatorio. Para endpoints publicos usar `'__return_true'` de forma explicita y documentada.
- Validar y sanitizar con `args` en lugar de leer el request a mano.
- Retornar `WP_REST_Response` o `WP_Error` con codigo HTTP adecuado.
- Namespace de rutas con version (`plugin-name/v1`).

## Base de datos

- Toda query con datos externos debe usar `$wpdb->prepare()`.
- Para nombres de tabla o columna dinamicos usar el placeholder `%i` (WordPress 6.2+); nunca concatenar input del usuario.
- Nombres de tabla con `$wpdb->prefix . 'plugin_name_items'`, centralizados en el repositorio.
- Usar `$wpdb->insert()`, `$wpdb->update()` y `$wpdb->delete()` con arrays de formato cuando sea posible.
- Verificar el resultado de cada operacion y loguear `$wpdb->last_error` cuando falle, sin mostrarlo al usuario.
- Si falla una escritura, el repositorio lanza una excepcion. Una transaccion solo sirve si esos fallos la interrumpen.
- Preferir CPTs + meta cuando el dato encaje en el modelo de WordPress; usar tablas propias cuando haya volumen, consultas complejas o estructura relacional.

## Integraciones externas

- Timeout explicito en toda llamada; solo HTTPS.
- Validar el codigo HTTP y la forma de la respuesta antes de usarla.
- No encadenar llamadas bloqueantes al renderizar una pantalla ni dentro de un request publico: diferirlas (cron o Action Scheduler) o pedirlas por AJAX.
- Con redirecciones manuales, usar una allowlist de hosts.
- Definir que pasa si el servicio falla y como se registra.
- Confirmar que la licencia del servicio permite el uso comercial.

## Integraciones con IA

- Usar el AI Client de WordPress (`wp_ai_client_prompt()`, WordPress 7.0+) cuando el plugin no exija un proveedor concreto.
- Comprobar `is_supported_for_text_generation()` antes de ofrecer la funcion.
- `generate_text()` devuelve `string|WP_Error`; `generate_text_result()` devuelve un objeto, no un string.
- El modelo es una preferencia: el plugin debe funcionar sin el.
- La IA es opcional salvo que sea el objetivo del plugin: definir un fallback.
- Tratar su salida como no confiable: validar, sanitizar y escapar.
- Las acciones que publican o modifican datos requieren revision humana.
- Probar el camino real, no solo el fallback.
- Exponer acciones a agentes (Abilities API) solo si hace falta, con permisos especificos.

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

- Usar constantes para slugs (maximo 20 caracteres para post types).
- Registrar en infraestructura, en el hook `init`.
- No hacer `flush_rewrite_rules()` en cada request.
- Hacer flush solo en activacion/desactivacion.

## Assets

Usar handles con prefijo del plugin.

```php
wp_enqueue_script(
    'plugin-name-admin',
    MY_PLUGIN_URL . 'assets/admin/admin.js',
    [],
    MY_PLUGIN_VERSION,
    ['in_footer' => true, 'strategy' => 'defer']
);
```

Reglas:

- Admin assets solo en pantallas necesarias (comparar el `$hook_suffix` de `admin_enqueue_scripts`).
- Frontend assets solo cuando el shortcode, template o feature se usa (registrar con `wp_register_script()` y encolar desde el render).
- Usar `wp_add_inline_script()` para pasar datos de PHP a JS; `wp_localize_script()` solo para strings traducibles.
- Usar `wp_set_script_translations()` si el JS tiene textos traducibles.
- Declarar `jquery` como dependencia solo si realmente se usa.
- No hardcodear URLs si pueden venir de WordPress (`admin_url('admin-ajax.php')`, `rest_url()`).

## Logs

Si el plugin usa logs:

- Guardarlos en una carpeta propia del plugin dentro de uploads (`wp_upload_dir()['basedir'] . '/plugin-name/logs/'`), no dentro de la carpeta del plugin: WordPress borra la carpeta del plugin al actualizarlo y en muchos hostings no es escribible.
- Usar nombres de archivo no predecibles (por ejemplo con `wp_hash()`), proteger la carpeta con `index.php` vacio y `.htaccess` (`Deny from all`). En Nginx `.htaccess` no aplica: documentar la regla equivalente.
- Crear un logger propio o adaptador simple para centralizar escrituras.
- Registrar errores relevantes de imports, uploads, integraciones y procesos administrativos.
- No mostrar stack traces, rutas absolutas ni detalles internos al usuario final; esos detalles deben ir al log.
- No commitear `.log`.
- La rotacion y la retencion son obligatorias: definir tamano maximo o antiguedad y documentarlas.
- No loguear secretos, tokens, passwords ni payloads sensibles. Emails e IPs van con hash, salvo necesidad justificada.
- Incluir contexto util: `post_id`, `user_id`, `status`, `http_code`, `action`.
- Usar niveles: `info`, `warning`, `error`, `exception`.

## Configuracion

Preferir constantes para:

- `MY_PLUGIN_VERSION`
- `MY_PLUGIN_FILE`
- `MY_PLUGIN_PATH`
- `MY_PLUGIN_URL`
- `MY_PLUGIN_BASENAME`

Para opciones:

- `plugin_name_settings`
- `plugin_name_db_version`
- `plugin_name_api_key`

Encapsular defaults en una clase de settings.

## Tipado PHP

En archivos propios:

- Usar `declare(strict_types=1);`.
- Tipar parametros y retornos cuando sea posible.
- Evitar arrays magicos en logica de negocio.
- Preferir DTOs, Value Objects o clases simples cuando el dato crece o cruza varias capas.
- Mantener compatibilidad con la version de PHP declarada en `Requires PHP`.

Cuidado con `strict_types` en codigo WordPress:

- Muchas funciones de WordPress devuelven strings donde uno espera int (`get_option()`, `get_post_meta()`, `$wpdb->get_var()`). Castear explicitamente (`(int)`, `absint()`) antes de pasarlas a metodos tipados.
- Los callbacks de hooks pueden recibir `null`, `''` o tipos inesperados segun el contexto. En callbacks de hooks de WordPress, tipar de forma permisiva (o sin tipo) y normalizar dentro del metodo; los filtros deben devolver siempre el tipo que reciben.

## Internacionalizacion

Todo texto visible debe usar el text domain del plugin.

```php
__('Text', 'plugin-name')
esc_html__('Text', 'plugin-name')
```

Reglas:

- El text domain debe ser un string literal, nunca una constante o variable: las herramientas de extraccion (`wp i18n make-pot`) no lo detectan.
- No llamar funciones de traduccion antes de `init` (WordPress 6.7+ muestra un aviso "translation loading triggered too early").
- Si el plugin no se distribuye por wordpress.org, cargar traducciones con `load_plugin_textdomain('plugin-name', false, dirname(MY_PLUGIN_BASENAME) . '/languages')` en `init`.
- Usar `sprintf()` con placeholders y comentarios `/* translators: */` en lugar de concatenar textos.

## Accesibilidad

- Foco visible y navegacion por teclado.
- Modales con `role="dialog"`, `aria-modal`, cierre con Esc y foco atrapado.
- Labels en los formularios y `alt` en las imagenes.
- No comunicar estados solo por color.

## Calidad automatizada

Minimo obligatorio en todo plugin nuevo:

- `php -l` y PHPCS en GitHub Actions, en cada push y PR.
- Los errores de PHPCS bloquean; las advertencias se revisan.
- Solo se admite `phpcs:ignore` en la linea afectada y con motivo.
- PHPUnit para `Domain` si existe, sin levantar WordPress.
- Sin `Domain`: pruebas manuales documentadas en `docs/` o `README.md`.

PHPStan con `szepeviktor/phpstan-wordpress` es opcional. Si hay JavaScript o CSS, validar manualmente o con herramientas disponibles.

Documentar en la seccion `Proyecto` los comandos exactos de validacion para que el agente pueda ejecutarlos.

`composer.json`:

```json
{
  "require-dev": {
    "wp-coding-standards/wpcs": "^3.0",
    "dealerdirect/phpcodesniffer-composer-installer": "^1.0",
    "phpunit/phpunit": "^11.5"
  },
  "config": {
    "allow-plugins": {
      "dealerdirect/phpcodesniffer-composer-installer": true
    }
  }
}
```

`phpcs.xml.dist` (reglas de seguridad, sin el estilo de WPCS, que choca con PSR-4 y `camelCase`):

```xml
<?xml version="1.0"?>
<ruleset name="Plugin">
  <file>.</file>
  <exclude-pattern>/vendor/*</exclude-pattern>
  <exclude-pattern>/node_modules/*</exclude-pattern>
  <exclude-pattern>/dist/*</exclude-pattern>
  <exclude-pattern>/tests/*</exclude-pattern>
  <arg name="extensions" value="php"/>
  <config name="ignore_warnings_on_exit" value="1"/>
  <rule ref="WordPress.Security">
    <exclude name="WordPress.Security.EscapeOutput.ExceptionNotEscaped"/>
  </rule>
  <rule ref="WordPress.DB.PreparedSQL"/>
  <rule ref="WordPress.DB.PreparedSQLPlaceholders"/>
  <rule ref="WordPress.WP.I18n"/>
  <rule ref="WordPress.PHP.DevelopmentFunctions"/>
</ruleset>
```

`.github/workflows/ci.yml`:

```yaml
name: CI
on:
  push:
  pull_request:
jobs:
  quality:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v7
      - uses: shivammathur/setup-php@v2
        with:
          php-version: '8.3'
          tools: composer
      - run: composer install --no-interaction --no-progress
      - name: Sintaxis
        run: find . -name '*.php' -not -path './vendor/*' -not -path './node_modules/*' -print0 | xargs -0 -n1 php -l
      - run: vendor/bin/phpcs
      - name: Tests
        if: hashFiles('phpunit.xml.dist') != ''
        run: vendor/bin/phpunit
```

`phpunit.xml.dist`:

```xml
<?xml version="1.0"?>
<phpunit bootstrap="tests/bootstrap.php" colors="true">
  <testsuites>
    <testsuite name="unit">
      <directory>tests/Unit</directory>
    </testsuite>
  </testsuites>
</phpunit>
```

`tests/bootstrap.php` (las clases protegen su carga con `ABSPATH`):

```php
<?php

declare(strict_types=1);

define('ABSPATH', __DIR__ . '/');

require __DIR__ . '/../autoload.php';
```

## Testing

El minimo esta en `Calidad automatizada`. Por encima de ese minimo, la cobertura debe escalar con el riesgo del cambio:

- Brain Monkey cuando la logica a probar llama funciones de WordPress.
- Tests de integracion en un WordPress local cuando el cambio toque hooks, AJAX, admin-post, REST, CPTs, tablas o migraciones.

Priorizar tests en:

- Servicios de dominio.
- Reglas de acceso.
- Sanitizacion y validacion de inputs.
- Repositorios con queries complejas.
- Migraciones.
- Integraciones externas con errores o timeouts.

## README.md

Actualizar `README.md` cuando cambie:

- Chips tecnologicos (ver formato abajo).
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
- Acciones AJAX/admin-post y endpoints REST.
- Migraciones o tablas.

Cada README de plugin nuevo debe incluir una seccion temprana llamada `Technology Chips` o `Chips tecnologicos`, con badges de colores y logos para todas las tecnologias, APIs, librerias, formatos e integraciones usadas por el plugin.

Formato recomendado:

```md
## Technology Chips

![WordPress](https://img.shields.io/badge/WordPress-21759B?style=for-the-badge&logo=wordpress&logoColor=white)
![PHP](https://img.shields.io/badge/PHP-8.3%2B-777BB4?style=for-the-badge&logo=php&logoColor=white)
![Composer](https://img.shields.io/badge/Composer-885630?style=for-the-badge&logo=composer&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-Custom%20Tables-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
```

Usar preferentemente badges de Shields.io con `style=for-the-badge`, colores reconocibles de marca y logos oficiales cuando existan. Los chips deben mantenerse actualizados cuando se agreguen o retiren tecnologias, dependencias, integraciones, formatos de archivo o APIs relevantes.

## AGENTS.md y CLAUDE.md

Actualizar `AGENTS.md` cuando se agregue:

- Nueva capa.
- Nueva convencion.
- Nuevo flujo importante.
- Nueva integracion externa.
- Nuevo CPT, shortcode, AJAX action, admin-post action o endpoint REST.
- Nueva dependencia.
- Nueva regla de seguridad o compatibilidad.

`CLAUDE.md` solo contiene la linea `@AGENTS.md` (y, si hace falta, instrucciones exclusivas de Claude Code). La fuente de verdad es `AGENTS.md`.

## Repositorio y release

- Repos de clientes: privados por defecto.
- Nunca commitear emails personales, datos de clientes, logs ni secretos.
- Hallazgos de seguridad abiertos: solo en repos privados.
- Paquete reproducible: `.gitattributes` con `export-ignore` y, si hay dependencias de produccion, `composer install --no-dev`.
- Version alineada entre header, constante y tag.
- `CHANGELOG.md` actualizado en cada release.

`.gitattributes`:

```text
* text=auto eol=lf
*.png binary
*.jpg binary

/docs export-ignore
/tests export-ignore
/.github export-ignore
/.vscode export-ignore
/.claude export-ignore
/composer.json export-ignore
/composer.lock export-ignore
/phpcs.xml.dist export-ignore
/phpunit.xml.dist export-ignore
*.md export-ignore
.gitignore export-ignore
.gitattributes export-ignore
```

Si el plugin tiene dependencias de produccion, generar `vendor/` con `--no-dev` e incluirlo en el paquete.

## Commit convencional

Cada respuesta final debe incluir una sugerencia de commit.

Los commits, las descripciones de PR y los comentarios se publican solo con la identidad del autor del repositorio. Los agentes IA no firman: sin `Co-Authored-By`, sin "Generated with Claude Code" ni marcas equivalentes, y sin enlaces de sesion.

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

Las correcciones de seguridad usan `fix(security)` o `fix` con el scope afectado; `security` no es un tipo estandar de Conventional Commits y herramientas como commitlint lo rechazan.

Ejemplos:

```text
feat(admin): add settings page for popup rules
fix(ajax): validate nonce before saving lead
fix(security): escape settings output
refactor(domain): extract lead access rules
docs(readme): document shortcode usage
```

## Configuracion recomendada VS Code

Crear `.vscode/settings.json`:

```json
{
  "intelephense.environment.phpVersion": "8.3.0",
  "intelephense.stubs": [
    "wordpress",
    "superglobals",
    "Core",
    "standard",
    "spl",
    "date",
    "pcre",
    "session",
    "json",
    "filter",
    "ctype",
    "mbstring",
    "hash",
    "curl",
    "openssl",
    "fileinfo",
    "Reflection",
    "SimpleXML",
    "xml",
    "zip"
  ],
  "php.suggest.basic": false,
  "php.validate.enable": true,
  "php.validate.executablePath": "C:/laragon/bin/php/php-8.x.x/php.exe",
  "files.associations": {
    "*.php": "php"
  }
}
```

Notas:

- Al definir `intelephense.stubs` se reemplaza la lista por defecto. Incluir `superglobals` evita el falso positivo `Undefined variable '$_POST'` sin necesidad de desactivar `intelephense.diagnostics.undefinedVariables`, que oculta errores reales.
- Ajustar `intelephense.environment.phpVersion` a la version minima del plugin y `php.validate.executablePath` a la ruta real de PHP en Laragon.

## Checklist de cierre

- [ ] CI en verde.
- [ ] Nonce, capability, sanitizacion y escaping en todo lo tocado.
- [ ] Activar, desactivar y reactivar sin perder datos.
- [ ] Probado sin plugins opcionales y con el servicio externo caido.
- [ ] `README.md`, `AGENTS.md` y `CHANGELOG.md` actualizados.

## Principios finales

- El archivo principal coordina, no implementa.
- Las clases deben tener una responsabilidad clara.
- El dominio debe evitar saber demasiado de WordPress cuando esa separacion aporte claridad real.
- WordPress debe quedar encapsulado en infraestructura, admin o frontend.
- La seguridad no es opcional: sanitizar al entrar, escapar al salir, nonce + capability en cada accion.
- No repetir strings criticos.
- No romper compatibilidad con datos existentes.
- Documentar cada feature nueva.
- Sugerir siempre un commit convencional al terminar.
