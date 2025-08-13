# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

# WordPress Project Root Context

This is a WordPress development environment containing multiple plugin development approaches and a full WordPress installation for testing and development purposes.

## System Requirements & Environment

### Required Specifications
- **PHP Version**: 7.4 or greater (prefer PHP 8.1+ for optimal performance)
- **Database**: MySQL 8.0+ OR MariaDB 10.5+
- **Web Server**: Apache with mod_rewrite module enabled
- **Protocol**: HTTPS support required for all production environments
- **WordPress Link**: Include wordpress.org link on client sites

### Development Environment Standards
- **Local Server**: Laravel Valet with Nginx
- **PHP Version**: 8.1 with Xdebug enabled for debugging
- **Debug Settings**: Enable WP_DEBUG and WP_DEBUG_LOG in development
- **CLI Tools**: Use wp-cli for WordPress operations
- **Code Standards**: PHPCS with WordPress coding standards (required)

## Common Development Commands

### WordPress CLI (WP-CLI)
```bash
# Plugin management
wp plugin list                    # List installed plugins
wp plugin activate [plugin-name]  # Activate a plugin
wp plugin deactivate [plugin-name] # Deactivate a plugin

# Theme management  
wp theme list                     # List installed themes
wp theme activate [theme-name]    # Activate a theme

# Database operations
wp db export backup.sql           # Export database
wp db import backup.sql           # Import database

# WordPress updates
wp core update                    # Update WordPress core
wp plugin update --all            # Update all plugins
```

### Code Quality & Validation
```bash
# WordPress Coding Standards (PHPCS)
phpcs --standard=WordPress [file/directory]           # Check coding standards
phpcbf --standard=WordPress [file/directory]          # Fix coding standards

# Plugin/theme validation
wp plugin path [plugin-name]                          # Get plugin directory path
wp theme path [theme-name]                            # Get theme directory path
```

### Local Development with Valet
```bash
valet park                        # Park current directory for Valet
valet restart                     # Restart Valet services
valet links                       # List all Valet sites
```

### Debugging Commands
```bash
# WordPress debug log
tail -f wp-content/debug.log      # Monitor debug log in real-time
```

## Development Philosophy

### Keep It Simple (KISS Principle)
- **NEVER over-complicate solutions** - choose the simplest approach that works
- Break complex problems into simple, manageable steps
- Use WordPress native functions before custom solutions
- Prefer readable code over clever code
- Document the "why" behind complex decisions

### Step-by-Step Approach
- Always break tasks into small, actionable steps
- Complete one step fully before moving to the next
- Test each step individually when possible
- Provide clear explanations for each implementation decision

## WordPress Core Principles

### Fundamental Rules
- **NEVER modify WordPress core files** - use hooks, filters, and the Plugin API instead
- **ALWAYS follow WordPress coding standards** - use PHPCS with WordPress ruleset
- **Keep solutions simple** - don't over-engineer or add unnecessary complexity
- Prioritize security, performance, and accessibility in all implementations
- Use WordPress native functions over custom solutions when available

### Plugin API & Extensibility
- Utilize WordPress' robust Plugin API for all customizations
- Reference the Plugin Developer Handbook for best practices
- Create child themes instead of modifying parent themes directly
- Use WordPress hooks (actions/filters) for all functionality extensions

## Project Architecture

This WordPress development environment demonstrates multiple plugin development methodologies with comprehensive architectural examples.

### High-Level Architecture
This repository serves as a complete WordPress development training environment with:
- **Full WordPress Installation**: Complete WordPress 6.x setup with database configuration
- **Multiple Plugin Architectures**: Side-by-side comparison of procedural vs OOP approaches
- **Theme Development**: WordPress block themes and traditional themes
- **Development Tools**: Pre-configured for Laravel Valet with PHP 8.1 and Xdebug

### Plugin Development Approaches

#### Procedural Architecture (`header-notice-procedural/`)
```
header-notice-procedural/
├── header-notice-procedural.php    # Main plugin file with simple hooks
├── includes/
│   ├── functions.php               # Core functionality functions  
│   ├── admin.php                   # Admin interface functions
│   └── frontend.php                # Frontend display functions
├── assets/                         # CSS/JS assets
└── languages/                      # Translation files
```

**Key Characteristics:**
- Traditional WordPress hook/filter patterns using `add_action()` and `add_filter()`
- All functions prefixed with `hnp_` to avoid naming conflicts
- Simple procedural flow: register hooks → define functions → execute
- Perfect for smaller plugins or developers familiar with traditional PHP

#### Object-Oriented Architecture (`header-notice-oop/`)
```
header-notice-oop/
├── header-notice-oop.php                    # Bootstrap file
├── includes/
│   ├── class-header-notice-oop.php          # Main plugin class
│   ├── class-header-notice-oop-loader.php   # Hook management system
│   ├── class-header-notice-oop-i18n.php     # Internationalization
│   ├── class-header-notice-oop-activator.php # Plugin activation
│   └── class-header-notice-oop-deactivator.php # Plugin deactivation
├── admin/
│   ├── class-header-notice-oop-admin.php    # Admin functionality class
│   └── partials/                            # Admin template files
├── public/
│   ├── class-header-notice-oop-public.php   # Public-facing functionality
│   └── partials/                            # Public template files
└── languages/
```

**Key Characteristics:**
- WordPress Plugin Boilerplate (WPPB) structure from wppb.me
- Separation of concerns: admin logic separate from public logic
- Hook loader pattern for organized hook management
- Class-based architecture with dependency injection
- Scalable for larger, more complex plugins

### Theme Architecture
The project includes multiple WordPress theme approaches:
- **Block Themes**: Modern FSE themes using `theme.json` and HTML templates
- **Classic Themes**: Traditional PHP-based themes with template hierarchy
- **Hybrid Approaches**: Themes supporting both classic and block editor features

## Code Quality Standards

### Security Requirements (All Plugins)
- Validate and sanitize ALL user input
- Use prepared statements for database queries
- Implement proper user capability checks
- Never trust data from $_GET, $_POST, or $_REQUEST without validation
- Use WordPress security functions (wp_nonce_field, current_user_can, etc.)

### Performance Standards (All Plugins)
- Implement WordPress object caching for expensive operations
- Use transients for temporary data storage
- Optimize database queries to avoid performance bottlenecks
- Minimize HTTP requests through proper asset management

## Testing & Deployment

### Quality Assurance
- Test across multiple WordPress versions
- Validate with WordPress coding standards tools (PHPCS)
- Use staging environments for testing
- Implement proper backup strategies

### Documentation Requirements
- Document all custom hooks and filters
- Maintain README files for each plugin
- Include installation and configuration instructions
- Document any third-party dependencies

## Resources & Support

### Primary Resources
- **WordPress Codex**: Comprehensive WordPress documentation
- **Plugin Developer Handbook**: Plugin development best practices
- **WordPress Plugin Boilerplate**: https://wppb.me/ for OOP plugin structure

### Support Channels
- **HelpHub**: Encyclopedia of all things WordPress
- **WordPress Blog**: Latest updates and news
- **WordPress Planet**: News aggregator for WordPress blogs
- **WordPress Support Forums**: Community support and troubleshooting
- **WordPress IRC**: Real-time chat support (#wordpress on irc.libera.chat)

### Development Tools & Standards
- **PHPCS**: Required for all code - use WordPress coding standards ruleset
- **Xdebug**: Available for debugging (PHP 8.1)
- **WP-CLI**: For WordPress management and automation
- **Valet**: Local development server with Nginx
- **Code Validation**: Always run PHPCS before committing code

## Directory-Specific Context

### Plugin Development Context Files
When working in specific plugin directories, Claude will load additional architectural guidance:

- **`/wp-content/plugins/header-notice-procedural/`** → Loads `claude-procedural-details.md`
  - Traditional WordPress procedural patterns and hook/filter usage
  - Function naming conventions with `hnp_` prefix
  - Simple file organization and development workflow

- **`/wp-content/plugins/header-notice-oop/`** → Loads `claude-opp-details.md`
  - WordPress Plugin Boilerplate (WPPB) structure and conventions
  - Object-oriented architecture with class-based approach
  - Hook loader pattern and dependency injection

### Theme Development Context Files  
- **`/wp-content/themes/untitled folder/`** → Loads theme-specific CLAUDE.md
  - WordPress block theme development using Full Site Editing (FSE)
  - Theme.json configuration and HTML template usage
  - Block pattern and template part development

### Working with Multiple Architectures
This project demonstrates both approaches side-by-side:
1. **When to use Procedural**: Smaller plugins, simple functionality, traditional WordPress developers
2. **When to use OOP**: Complex plugins, team development, scalable architecture requirements
3. **Architecture Consistency**: Never mix approaches within a single plugin - choose one and stick with it

## Final Notes

- If you have suggestions, ideas, comments, or find bugs, refer to the Support Forums
- Each plugin directory contains specific architectural guidelines
- Maintain consistency within each plugin's chosen development approach
- Always reference the appropriate context file for the plugin you're working on

