# Perfect WordPress AI Builder

A comprehensive WordPress development environment demonstrating multiple plugin architecture approaches and AI-assisted development workflows.

## 🎥 YouTube Tutorial

This repository supports the YouTube video: **https://youtu.be/mckUYWT0RLo**

Watch the complete tutorial to see how AI can accelerate WordPress plugin development using both procedural and object-oriented approaches.

## 🏗️ Project Overview

This WordPress development environment showcases:

- **Complete WordPress Installation** - Full WordPress 6.x setup ready for development
- **Dual Architecture Demos** - Side-by-side comparison of procedural vs OOP plugin development
- **AI-Optimized Workflow** - Pre-configured with Claude Code instructions for intelligent development assistance
- **Professional Standards** - Follows WordPress coding standards with PHPCS integration

## 🚀 Quick Start

### Prerequisites

- **PHP 8.1+** with Xdebug enabled
- **MySQL 8.0+** or MariaDB 10.5+
- **Laravel Valet** (recommended) or Apache with mod_rewrite
- **WP-CLI** for WordPress management
- **PHPCS** with WordPress coding standards

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/eirichmond/perfect-wordpress-ai-builder
   cd perfect-wordpress-ai-builder
   ```

2. **Set up local development** (using Valet)
   ```bash
   valet park
   valet restart
   ```

3. **Configure WordPress**
   - Set up your database connection in `wp-config.php`
   - Run WordPress installation through the web interface

4. **Install development tools**
   ```bash
   # WordPress CLI operations
   wp plugin list
   wp theme list
   
   # Code quality checks
   phpcs --standard=WordPress [plugin-directory]
   ```

## 📁 Project Structure

```
perfect-wordpress-ai-builder/
├── CLAUDE.md                           # AI development instructions
├── claude-procedural-details.md        # Procedural approach guidance
├── claude-opp-details.md              # OOP approach guidance
├── prompt.txt                          # Original project requirements
└── wp-content/
    ├── plugins/
    │   ├── header-notice-procedural/   # Traditional procedural plugin
    │   └── header-notice-oop/         # Object-oriented plugin
    └── themes/
        └── [various WordPress themes]
```

## 🛠️ Plugin Architectures Demonstrated

### Procedural Architecture (`header-notice-procedural/`)

Traditional WordPress development using:
- Hook and filter patterns with `add_action()` and `add_filter()`
- Prefixed functions (`hnp_*`) to avoid conflicts
- Simple file organization
- Perfect for smaller plugins and traditional PHP developers

**Structure:**
```
header-notice-procedural/
├── header-notice-procedural.php    # Main plugin file
├── includes/
│   ├── functions.php               # Core functionality
│   ├── admin.php                   # Admin interface
│   └── frontend.php                # Frontend display
└── assets/                         # CSS/JS files
```

### Object-Oriented Architecture (`header-notice-oop/`)

Modern WordPress Plugin Boilerplate (WPPB) structure featuring:
- Class-based architecture with dependency injection
- Separation of concerns (admin vs public logic)
- Hook loader pattern for organized management
- Scalable for complex, enterprise-level plugins

**Structure:**
```
header-notice-oop/
├── header-notice-oop.php                    # Bootstrap file
├── includes/
│   ├── class-header-notice-oop.php          # Main plugin class
│   ├── class-header-notice-oop-loader.php   # Hook management
│   └── [additional classes]
├── admin/                                   # Admin functionality
└── public/                                  # Public-facing code
```

## 🤖 AI Development Features

### Claude Code Integration

This repository is optimized for AI-assisted development with:

- **Context-Aware Instructions** - Detailed guidance in `CLAUDE.md`
- **Architecture-Specific Guidance** - Separate instruction files for each approach
- **WordPress Standards Enforcement** - Automated code quality requirements
- **Step-by-Step Development** - Broken down into manageable tasks

### Development Commands

```bash
# WordPress CLI operations
wp plugin activate [plugin-name]
wp plugin deactivate [plugin-name]
wp core update

# Code quality validation
phpcs --standard=WordPress [file/directory]
phpcbf --standard=WordPress [file/directory]

# Debug monitoring
tail -f wp-content/debug.log
```

## 📋 Plugin Requirements Implemented

### Core Functionality
- ✅ **Header Notice Display** - Customizable notices at the top of every page
- ✅ **Three Notice Types** - General (green), Warning (black), Error (red)
- ✅ **Admin Controls** - Full WordPress dashboard integration
- ✅ **Expiration System** - Timezone-aware automatic expiration

### Technical Features
- ✅ **Security** - Proper nonce verification and input sanitization
- ✅ **Performance** - Optimized database queries and caching
- ✅ **Responsive Design** - Mobile, tablet, and desktop compatibility
- ✅ **WordPress Standards** - Full compliance with coding standards

### Administrative Interface
- ✅ **User-Friendly Forms** - Intuitive admin interface
- ✅ **Capability Checks** - Administrator-only access (`manage_options`)
- ✅ **Form Validation** - Comprehensive input validation and sanitization
- ✅ **Settings API** - WordPress options API integration

## 🎯 Learning Objectives

This project demonstrates:

1. **Architecture Comparison** - When to use procedural vs OOP approaches
2. **WordPress Best Practices** - Security, performance, and standards compliance
3. **AI-Assisted Development** - How AI can accelerate WordPress development
4. **Professional Workflow** - From requirements to deployment

## 🔧 Development Philosophy

### KISS Principle (Keep It Simple)
- Choose the simplest approach that works
- Break complex problems into manageable steps
- Use WordPress native functions before custom solutions
- Prioritize readable code over clever code

### WordPress Core Principles
- **Never modify WordPress core** - Use hooks, filters, and Plugin API
- **Follow coding standards** - PHPCS with WordPress ruleset
- **Security first** - Validate, sanitize, and escape all data
- **Performance matters** - Optimize queries and implement caching

## 📚 Resources

- **WordPress Codex** - Comprehensive WordPress documentation
- **Plugin Developer Handbook** - Best practices guide
- **WordPress Plugin Boilerplate** - https://wppb.me/
- **WordPress Coding Standards** - https://developer.wordpress.org/coding-standards/

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Follow WordPress coding standards (`phpcs --standard=WordPress`)
4. Commit your changes (`git commit -m 'Add amazing feature'`)
5. Push to the branch (`git push origin feature/amazing-feature`)
6. Open a Pull Request

## 📄 License

This project is licensed under the GPL v2 or later - see the WordPress licensing requirements.

## 🎬 YouTube Channel

For more WordPress development tutorials and AI-assisted coding workflows, subscribe to: **https://www.youtube.com/@elliottrichmondwp**

---

**Built with ❤️ using Claude Code and WordPress best practices**