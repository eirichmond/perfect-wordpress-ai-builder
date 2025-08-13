# Header Notice Procedural Plugin Context

Location: `wp-content/plugins/header-notice-procedural/claude-procedural-details.md`

This plugin follows **traditional WordPress procedural patterns** using hooks and filters in the standard WordPress way.

## Plugin Architecture: Procedural Approach

### Core Philosophy
- Use **simple procedural functions** with WordPress hooks and filters
- Follow traditional WordPress plugin development patterns
- Keep functions small, focused, and easy to understand
- **Never over-complicate** - use the simplest solution that works
- Break complex functionality into simple, manageable steps

### File Structure (Procedural)
```
header-notice-procedural/
├── header-notice-procedural.php    # Main plugin file
├── includes/
│   ├── functions.php               # Core functionality functions
│   ├── admin.php                   # Admin-specific functions
│   └── frontend.php                # Frontend display functions
├── assets/
│   ├── css/admin.css              # Admin styles
│   ├── css/frontend.css           # Frontend styles
│   └── js/admin.js                # Admin JavaScript
├── languages/                     # Translation files
└── README.txt                     # WordPress plugin readme
```

## Procedural Development Standards

### Function Naming Convention
- Prefix ALL functions with plugin slug: `hnp_` (header_notice_procedural)
- Use descriptive, clear function names
- Follow WordPress naming conventions (lowercase with underscores)

```php
// ✅ CORRECT - Procedural approach
function hnp_display_header_notice() {
    // Simple, focused function
}

function hnp_save_notice_settings( $settings ) {
    // Clear purpose, easy to understand
}

function hnp_enqueue_admin_scripts() {
    // Follows WordPress patterns
}
```

### Hook Implementation Pattern
```php
// ✅ Standard WordPress procedural pattern
add_action( 'wp_head', 'hnp_display_header_notice' );
add_action( 'admin_menu', 'hnp_add_admin_menu' );
add_filter( 'plugin_action_links_' . plugin_basename(__FILE__), 'hnp_add_settings_link' );

// Functions defined separately
function hnp_display_header_notice() {
    // Step 1: Get notice settings
    $notice_text = get_option( 'hnp_notice_text', '' );
    
    // Step 2: Check if notice should display
    if ( empty( $notice_text ) || ! hnp_should_display_notice() ) {
        return;
    }
    
    // Step 3: Display the notice
    echo '<div class="header-notice">' . esc_html( $notice_text ) . '</div>';
}
```

## WordPress Coding Standards (Procedural)

### Security Standards
```php
// ✅ Input validation and sanitization
function hnp_save_notice_text() {
    // Step 1: Verify nonce
    if ( ! wp_verify_nonce( $_POST['hnp_nonce'], 'hnp_save_notice' ) ) {
        return false;
    }
    
    // Step 2: Check user capabilities
    if ( ! current_user_can( 'manage_options' ) ) {
        return false;
    }
    
    // Step 3: Sanitize input
    $notice_text = sanitize_textarea_field( $_POST['notice_text'] );
    
    // Step 4: Save to database
    update_option( 'hnp_notice_text', $notice_text );
}

// ✅ Output escaping
function hnp_display_admin_field() {
    $current_value = get_option( 'hnp_notice_text', '' );
    echo '<textarea name="notice_text">' . esc_textarea( $current_value ) . '</textarea>';
}
```

### Database Operations
```php
// ✅ Use WordPress functions, not direct SQL
function hnp_get_notice_settings() {
    return array(
        'text'         => get_option( 'hnp_notice_text', '' ),
        'show_on_all'  => get_option( 'hnp_show_on_all', false ),
        'css_class'    => get_option( 'hnp_css_class', 'default-notice' )
    );
}

// ✅ Simple option management
function hnp_update_notice_setting( $key, $value ) {
    $allowed_keys = array( 'hnp_notice_text', 'hnp_show_on_all', 'hnp_css_class' );
    
    if ( in_array( $key, $allowed_keys ) ) {
        update_option( $key, $value );
        return true;
    }
    
    return false;
}
```

## Plugin Structure Implementation

### Main Plugin File Pattern
```php
<?php
/**
 * Plugin Name: Header Notice Procedural
 * Description: Simple header notice plugin using procedural WordPress patterns
 * Version: 1.0.0
 * Author: Your Name
 */

// Prevent direct access
if ( ! defined( 'ABSPATH' ) ) {
    exit;
}

// Define plugin constants
define( 'HNP_PLUGIN_URL', plugin_dir_url( __FILE__ ) );
define( 'HNP_PLUGIN_PATH', plugin_dir_path( __FILE__ ) );
define( 'HNP_VERSION', '1.0.0' );

// Include required files
require_once HNP_PLUGIN_PATH . 'includes/functions.php';
require_once HNP_PLUGIN_PATH . 'includes/admin.php';
require_once HNP_PLUGIN_PATH . 'includes/frontend.php';

// Register activation/deactivation hooks
register_activation_hook( __FILE__, 'hnp_activate_plugin' );
register_deactivation_hook( __FILE__, 'hnp_deactivate_plugin' );

// Initialize plugin
add_action( 'plugins_loaded', 'hnp_init' );

function hnp_init() {
    // Load text domain for translations
    load_plugin_textdomain( 'header-notice-procedural', false, dirname( plugin_basename( __FILE__ ) ) . '/languages' );
}
```

### Simple Step-by-Step Development Process

#### Step 1: Core Functionality
```php
// includes/functions.php
function hnp_display_header_notice() {
    // Keep it simple - just display the notice
    $notice = get_option( 'hnp_notice_text' );
    if ( $notice ) {
        echo '<div class="hnp-notice">' . esc_html( $notice ) . '</div>';
    }
}
add_action( 'wp_head', 'hnp_display_header_notice' );
```

#### Step 2: Admin Interface
```php
// includes/admin.php
function hnp_add_admin_menu() {
    add_options_page(
        'Header Notice Settings',
        'Header Notice',
        'manage_options',
        'header-notice-settings',
        'hnp_admin_page'
    );
}
add_action( 'admin_menu', 'hnp_add_admin_menu' );

function hnp_admin_page() {
    // Simple admin form - no over-complication
    ?>
    <div class="wrap">
        <h1>Header Notice Settings</h1>
        <form method="post" action="options.php">
            <?php
            settings_fields( 'hnp_settings' );
            do_settings_sections( 'hnp_settings' );
            ?>
            <table class="form-table">
                <tr>
                    <th><label for="hnp_notice_text">Notice Text</label></th>
                    <td><textarea id="hnp_notice_text" name="hnp_notice_text"><?php echo esc_textarea( get_option( 'hnp_notice_text' ) ); ?></textarea></td>
                </tr>
            </table>
            <?php submit_button(); ?>
        </form>
    </div>
    <?php
}
```

## Development Guidelines

### Simplicity Rules
1. **One function, one purpose** - keep functions small and focused
2. **Use WordPress standards** - don't reinvent the wheel
3. **Clear variable names** - make code self-documenting
4. **Comment the "why"** - not the "what"
5. **Test each function individually** - easier debugging

### PHPCS Integration
- Run `phpcs --standard=WordPress` before committing
- Fix all WordPress coding standard violations
- Use WordPress-specific functions for security and compatibility

### Debugging with Xdebug
- Set breakpoints in functions to step through logic
- Use `error_log()` for simple debugging output
- Leverage Xdebug's variable inspection in PHP 8.1

### Common Procedural Patterns
```php
// ✅ Simple conditional loading
function hnp_should_load_notice() {
    return is_front_page() || is_home();
}

// ✅ Basic settings validation
function hnp_validate_notice_text( $input ) {
    return sanitize_textarea_field( $input );
}

// ✅ Simple asset enqueueing
function hnp_enqueue_styles() {
    wp_enqueue_style( 'hnp-styles', HNP_PLUGIN_URL . 'assets/css/frontend.css', array(), HNP_VERSION );
}
add_action( 'wp_enqueue_scripts', 'hnp_enqueue_styles' );
```

## Remember
- **Keep it simple** - procedural doesn't mean complicated
- **Use WordPress patterns** - follow established conventions
- **Break into steps** - tackle one small piece at a time
- **Test frequently** - verify each function works independently
- **Run PHPCS** - maintain WordPress coding standards
