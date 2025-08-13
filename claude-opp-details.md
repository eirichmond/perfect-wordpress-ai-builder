# Header Notice OOP Plugin Context

Location: `wp-content/plugins/header-notice-oop/claude-opp-details.md`

This plugin follows the **WordPress Plugin Boilerplate (WPPB)** structure from https://wppb.me/ using modern OOP patterns while keeping implementations simple and straightforward.

## Plugin Architecture: WPPB OOP Approach

### Core Philosophy
- Use **WordPress Plugin Boilerplate structure** exactly as defined by wppb.me
- Apply OOP principles but **keep implementations simple**
- Break complex functionality into small, manageable class methods
- **Never over-complicate** - choose the simplest OOP solution that works
- Follow WPPB naming conventions and file organization

### WPPB File Structure (Exact)
```
header-notice-oop/
├── header-notice-oop.php              # Main plugin file (bootstrap)
├── uninstall.php                      # Uninstall cleanup
├── includes/
│   ├── class-header-notice-oop.php              # Main plugin class
│   ├── class-header-notice-oop-loader.php       # Hook loader class
│   ├── class-header-notice-oop-i18n.php         # Internationalization
│   ├── class-header-notice-oop-activator.php    # Activation logic
│   ├── class-header-notice-oop-deactivator.php  # Deactivation logic
│   └── index.php                               # Security file
├── admin/
│   ├── class-header-notice-oop-admin.php        # Admin functionality
│   ├── partials/
│   │   └── header-notice-oop-admin-display.php  # Admin templates
│   ├── css/header-notice-oop-admin.css         # Admin styles
│   ├── js/header-notice-oop-admin.js           # Admin scripts
│   └── index.php                               # Security file
├── public/
│   ├── class-header-notice-oop-public.php       # Public functionality
│   ├── partials/
│   │   └── header-notice-oop-public-display.php # Public templates
│   ├── css/header-notice-oop-public.css        # Public styles
│   ├── js/header-notice-oop-public.js          # Public scripts
│   └── index.php                               # Security file
├── languages/                                  # Translation files
└── README.txt                                  # WordPress plugin readme
```

## WPPB OOP Development Standards

### Class Naming Convention (WPPB Standard)
- Follow exact WPPB naming: `Header_Notice_Oop_*`
- Use underscores, not hyphens in class names
- Prefix with plugin name for uniqueness
- Keep class responsibilities simple and focused

### Main Plugin Class Pattern (WPPB)
```php
// includes/class-header-notice-oop.php
class Header_Notice_Oop {

    protected $loader;
    protected $plugin_name;
    protected $version;

    public function __construct() {
        if ( defined( 'HEADER_NOTICE_OOP_VERSION' ) ) {
            $this->version = HEADER_NOTICE_OOP_VERSION;
        } else {
            $this->version = '1.0.0';
        }
        $this->plugin_name = 'header-notice-oop';

        $this->load_dependencies();
        $this->set_locale();
        $this->define_admin_hooks();
        $this->define_public_hooks();
    }

    // Simple, step-by-step initialization
    private function load_dependencies() {
        // Step 1: Load the loader
        require_once plugin_dir_path( dirname( __FILE__ ) ) . 'includes/class-header-notice-oop-loader.php';
        
        // Step 2: Load internationalization
        require_once plugin_dir_path( dirname( __FILE__ ) ) . 'includes/class-header-notice-oop-i18n.php';
        
        // Step 3: Load admin functionality
        require_once plugin_dir_path( dirname( __FILE__ ) ) . 'admin/class-header-notice-oop-admin.php';
        
        // Step 4: Load public functionality
        require_once plugin_dir_path( dirname( __FILE__ ) ) . 'public/class-header-notice-oop-public.php';
        
        // Step 5: Create loader instance
        $this->loader = new Header_Notice_Oop_Loader();
    }
}
```

### WPPB Loader Pattern (Keep Simple)
```php
// includes/class-header-notice-oop-loader.php
class Header_Notice_Oop_Loader {

    protected $actions;
    protected $filters;

    public function __construct() {
        $this->actions = array();
        $this->filters = array();
    }

    // Simple method to add actions
    public function add_action( $hook, $component, $callback, $priority = 10, $accepted_args = 1 ) {
        $this->actions = $this->add( $this->actions, $hook, $component, $callback, $priority, $accepted_args );
    }

    // Simple method to add filters
    public function add_filter( $hook, $component, $callback, $priority = 10, $accepted_args = 1 ) {
        $this->filters = $this->add( $this->filters, $hook, $component, $callback, $priority, $accepted_args );
    }

    // Keep the add method simple
    private function add( $hooks, $hook, $component, $callback, $priority, $accepted_args ) {
        $hooks[] = array(
            'hook'          => $hook,
            'component'     => $component,
            'callback'      => $callback,
            'priority'      => $priority,
            'accepted_args' => $accepted_args
        );
        return $hooks;
    }

    // Simple hook registration
    public function run() {
        foreach ( $this->filters as $hook ) {
            add_filter( $hook['hook'], array( $hook['component'], $hook['callback'] ), $hook['priority'], $hook['accepted_args'] );
        }

        foreach ( $this->actions as $hook ) {
            add_action( $hook['hook'], array( $hook['component'], $hook['callback'] ), $hook['priority'], $hook['accepted_args'] );
        }
    }
}
```

## WPPB Admin Class Implementation

### Admin Class Pattern (Simple)
```php
// admin/class-header-notice-oop-admin.php
class Header_Notice_Oop_Admin {

    private $plugin_name;
    private $version;

    public function __construct( $plugin_name, $version ) {
        $this->plugin_name = $plugin_name;
        $this->version = $version;
    }

    // Step 1: Simple admin menu registration
    public function add_admin_menu() {
        add_options_page(
            'Header Notice Settings',
            'Header Notice',
            'manage_options',
            $this->plugin_name,
            array( $this, 'display_admin_page' )
        );
    }

    // Step 2: Simple settings registration
    public function register_settings() {
        register_setting( 
            $this->plugin_name . '_settings', 
            $this->plugin_name . '_notice_text',
            array( $this, 'validate_notice_text' )
        );
    }

    // Step 3: Simple validation
    public function validate_notice_text( $input ) {
        return sanitize_textarea_field( $input );
    }

    // Step 4: Simple admin page display
    public function display_admin_page() {
        include_once 'partials/header-notice-oop-admin-display.php';
    }

    // Step 5: Simple asset enqueueing
    public function enqueue_styles() {
        wp_enqueue_style( 
            $this->plugin_name, 
            plugin_dir_url( __FILE__ ) . 'css/header-notice-oop-admin.css', 
            array(), 
            $this->version, 
            'all' 
        );
    }

    public function enqueue_scripts() {
        wp_enqueue_script( 
            $this->plugin_name, 
            plugin_dir_url( __FILE__ ) . 'js/header-notice-oop-admin.js', 
            array( 'jquery' ), 
            $this->version, 
            false 
        );
    }
}
```

## WPPB Public Class Implementation

### Public Display Class (Simple)
```php
// public/class-header-notice-oop-public.php
class Header_Notice_Oop_Public {

    private $plugin_name;
    private $version;

    public function __construct( $plugin_name, $version ) {
        $this->plugin_name = $plugin_name;
        $this->version = $version;
    }

    // Step 1: Simple notice display
    public function display_header_notice() {
        $notice_text = get_option( $this->plugin_name . '_notice_text' );
        
        if ( empty( $notice_text ) ) {
            return;
        }

        if ( ! $this->should_display_notice() ) {
            return;
        }

        include_once 'partials/header-notice-oop-public-display.php';
    }

    // Step 2: Simple display logic
    private function should_display_notice() {
        // Keep logic simple - can be extended later
        return is_front_page() || is_home();
    }

    // Step 3: Simple asset enqueueing
    public function enqueue_styles() {
        wp_enqueue_style( 
            $this->plugin_name, 
            plugin_dir_url( __FILE__ ) . 'css/header-notice-oop-public.css', 
            array(), 
            $this->version, 
            'all' 
        );
    }

    public function enqueue_scripts() {
        wp_enqueue_script( 
            $this->plugin_name, 
            plugin_dir_url( __FILE__ ) . 'js/header-notice-oop-public.js', 
            array( 'jquery' ), 
            $this->version, 
            false 
        );
    }
}
```

## WPPB Hook Registration Pattern

### Define Hooks in Main Class (Simple)
```php
// In main Header_Notice_Oop class
private function define_admin_hooks() {
    $plugin_admin = new Header_Notice_Oop_Admin( $this->get_plugin_name(), $this->get_version() );

    // Step 1: Register admin menu
    $this->loader->add_action( 'admin_menu', $plugin_admin, 'add_admin_menu' );
    
    // Step 2: Register settings
    $this->loader->add_action( 'admin_init', $plugin_admin, 'register_settings' );
    
    // Step 3: Enqueue admin assets
    $this->loader->add_action( 'admin_enqueue_scripts', $plugin_admin, 'enqueue_styles' );
    $this->loader->add_action( 'admin_enqueue_scripts', $plugin_admin, 'enqueue_scripts' );
}

private function define_public_hooks() {
    $plugin_public = new Header_Notice_Oop_Public( $this->get_plugin_name(), $this->get_version() );

    // Step 1: Display notice
    $this->loader->add_action( 'wp_head', $plugin_public, 'display_header_notice' );
    
    // Step 2: Enqueue public assets
    $this->loader->add_action( 'wp_enqueue_scripts', $plugin_public, 'enqueue_styles' );
    $this->loader->add_action( 'wp_enqueue_scripts', $plugin_public, 'enqueue_scripts' );
}
```

## WPPB Activation/Deactivation Pattern

### Simple Activator Class
```php
// includes/class-header-notice-oop-activator.php
class Header_Notice_Oop_Activator {

    public static function activate() {
        // Step 1: Set default options
        add_option( 'header_notice_oop_notice_text', '' );
        
        // Step 2: Set version option
        add_option( 'header_notice_oop_version', HEADER_NOTICE_OOP_VERSION );
        
        // Keep activation simple - no complex operations
    }
}
```

### Simple Deactivator Class
```php
// includes/class-header-notice-oop-deactivator.php
class Header_Notice_Oop_Deactivator {

    public static function deactivate() {
        // Step 1: Clean up temporary data if needed
        delete_transient( 'header_notice_oop_temp_data' );
        
        // Keep deactivation simple - don't remove user data
    }
}
```

## WordPress Coding Standards (WPPB OOP)

### Security in OOP Context
```php
// ✅ Method-level security checks
public function save_notice_settings() {
    // Step 1: Verify nonce
    if ( ! wp_verify_nonce( $_POST['_wpnonce'], $this->plugin_name . '_settings' ) ) {
        return false;
    }
    
    // Step 2: Check capabilities
    if ( ! current_user_can( 'manage_options' ) ) {
        return false;
    }
    
    // Step 3: Sanitize and save
    $notice_text = sanitize_textarea_field( $_POST['notice_text'] );
    update_option( $this->plugin_name . '_notice_text', $notice_text );
    
    return true;
}
```

### Simple Database Operations
```php
// ✅ Use WordPress functions within methods
private function get_notice_settings() {
    return array(
        'text'      => get_option( $this->plugin_name . '_notice_text', '' ),
        'enabled'   => get_option( $this->plugin_name . '_enabled', true ),
        'css_class' => get_option( $this->plugin_name . '_css_class', 'default-notice' )
    );
}

private function update_notice_setting( $key, $value ) {
    $option_name = $this->plugin_name . '_' . $key;
    return update_option( $option_name, $value );
}
```

## Development Guidelines (WPPB)

### WPPB Simplicity Rules
1. **Follow WPPB structure exactly** - don't deviate from the boilerplate organization
2. **Keep methods small and simple** - one method, one responsibility
3. **Use dependency injection** - pass dependencies through constructors
4. **Separate concerns** - admin in admin/, public in public/
5. **Use the loader pattern** - don't register hooks directly in classes

### Step-by-Step WPPB Development
1. **Start with WPPB generator** - Use wppb.me to generate the base structure
2. **Implement one class at a time** - Begin with the main plugin class
3. **Add functionality incrementally** - One method, test, repeat
4. **Keep templates separate** - Use partials for all HTML output
5. **Run PHPCS frequently** - Maintain WordPress coding standards

### WPPB Best Practices
- **Constructor injection** - Pass plugin name and version to all classes
- **Private methods** - Use private for internal class logic
- **Public methods** - Only expose what needs to be called externally
- **Method chaining** - Not required, keep calls simple and clear
- **Error handling** - Use WordPress functions like wp_die() appropriately

### Debugging WPPB with Xdebug
- Set breakpoints in class methods
- Inspect object properties and method calls
- Use Xdebug's step-through debugging in PHP 8.1
- Monitor hook registration through the loader pattern

## Remember (WPPB Specific)
- **Stick to WPPB structure** - don't create custom folder structures
- **Use the loader pattern** - all hooks go through the loader class
- **Keep classes focused** - admin logic in admin class, public logic in public class
- **Follow WPPB naming** - use exact class and method naming conventions
- **Run PHPCS with WordPress standards** - maintain consistent code quality
- **Test class interactions** - ensure proper dependency injection

This plugin demonstrates modern WordPress OOP development using the proven WordPress Plugin Boilerplate structure while maintaining simplicity and WordPress coding standards.
