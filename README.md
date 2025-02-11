# WordPress website lifecycle

:bulb: How to work with WordPress.

We run WordPress on Debian GNU/Linux operating system which runs on an UpCloud cloud instance.

### Division of labour

Who does what.

1. Editor manages the content and related settings.
2. Developer commits plugin and theme source code to GitHub and initiates deployment (CI/CD).
3. Viktor manages the operating system, webserver software, WordPress core, plugins, the theme,
   priviledged users, system settings, security, backup and migrations.

There is no web based administration.
WordPress installation is managed with git, **Composer** and WP-CLI on the command-line.

### More than the famous 5-minute installation

Our WordPress installation includes preparations for the next few **error-free years**.

These preparations are implemented in [MU plugins](/mu-plugins/).

### Working in a git repository

Our WordPress installation is stored in a git repository
and managed with Composer.

This is the starter template.
[szepeviktor/composer-managed-wordpress](https://github.com/szepeviktor/composer-managed-wordpress)

Custom plugins and themes live in separate git repositories.

**Purchased themes** can be customized using a child theme.

```bash
wp plugin install child-theme-configurator --activate
```

Keep the child theme in a git repository also.

### Onboarding for developers

Let's prevent working against each other!

- Don't write code changing WordPress core behavior anywhere else than **MU plugins**,
  - removing admin menus, admin bar elements
  - disabling emojis
  - disabling comments
  - disabling feeds
  - disabling embeds
  - mail settings and logging
  - WAF: authentication/login, HTTP and REST API security
  - comment form and contact form spam traps
  - media management
  - nav menu, translation and content caching
  - HTTP and HTML optimization
  - CDN support
- Plugin update check HTTP requests and updates itself are disabled
  because the whole WordPress installation is **managed with Composer**
- Plugin and theme update and WordPress management-related admin pages are removed
  (updated with Composer, administered with WP-CLI)
- WP-Cron is ran by a linux cron job (the default pseudo cron/web callback is disabled)
- Only things necessary for generating custom admin pages
  and generating HTML go into the **theme**
- Business logic (e.g. processing input from visitors) goes into **plugins**
- Please adhere to a coding standard of **your choice**
- Please avoid [discouraged functions](https://github.com/szepeviktor/debian-server-tools/blob/master/webserver/laravel/phpcs.xml#L18)
- We run static analysis on all source code
- PSR-4 autoloading is suggested (no need for `require` and custom class autoloading)
- WordPress core is installed in a separate subdirectory
- Please also see [hosting information for developers](https://github.com/szepeviktor/debian-server-tools/blob/master/Onboarding.md#onboarding-for-developers)

### List of documents

* [Software stack](/WordPress-stack.md)
* [Performance](/WordPress-performance.md)
* [Security](/WordPress-security.md)
* [Production environment](https://github.com/szepeviktor/debian-server-tools/blob/master/webserver/Production-website.md)

- WordPress installation: [szepeviktor/composer-managed-wordpress](https://github.com/szepeviktor/composer-managed-wordpress)
- [`wp-config`](/wp-config)
- _Alternative [WP-CLI installation](WP-CLI-installation.md)_
- MU plugins for core, theme and plugins: [/mu-plugins/](/mu-plugins) and how to install [Default plugins](/Plugins.md)
- Plugin starter: [szepeviktor/small-project](https://github.com/szepeviktor/small-project)
- Theme starter: [timber/starter-theme](https://github.com/timber/starter-theme/tree/2.x)
- Child theme starter: [/divi-child/](/divi-child)
- Feature plugins: [szepeviktor/wordpress-plugin-construction](https://github.com/szepeviktor/wordpress-plugin-construction)

* [Hooks in WordPress](/WordPress-hooks.md)
* [OOP for WordPress](/WordPress-OOP.md)
* Tools for development: [SentencePress](https://github.com/szepeviktor/SentencePress)
