# WP Dependency Installer
* Contributors: [Andy Fragen](https://github.com/afragen), [Matt Gibbs](https://github.com/mgibbs189), [contributors](https://github.com/afragen/wp-dependency-installer/graphs/contributors)
* Tags: plugin, dependency, install
* Requires at least: 5.1
* Requires PHP: 5.6
* Stable tag: master
* Donate link: <https://thefragens.com/wp-dependency-installer-donate>
* License: MIT

This is a drop in class for developers to optionally or automatically install plugin dependencies for their own plugins or themes. It can install a plugin from wp.org, GitHub, Bitbucket, GitLab, Gitea, or a direct URL.

[Comprehensive information regarding WP Dependency Installer is available on the wiki.](https://github.com/afragen/wp-dependency-installer/wiki)

See also: [example plugin](https://github.com/afragen/wp-dependency-installer-examples).

## Description

You can use **composer** to install this package within your WordPress plugin / theme.

1. Within your plugin or theme root folder, run the following command:

```shell
composer require afragen/wp-dependency-installer
```

2. Then create a sample [**`wp-dependencies.json`**](https://github.com/afragen/wp-dependency-installer/wiki/Configuration#json-config-file-format) file

```js
[
  {
    "name": "GitHub Updater",
    "host": "github",
    "slug": "github-updater/github-updater.php",
    "uri": "afragen/github-updater",
    "branch": "develop",
    "required": true,
    "token": null
  },
  {
    "name": "Query Monitor",
    "host": "wordpress",
    "slug": "query-monitor/query-monitor.php",
    "uri": "https://wordpress.org/plugins/query-monitor/",
    "optional": true
  },
  {
    "name": "Local Development",
    "host": "WordPress",
    "slug": "local-development/local-development.php",
    "uri": "https://wordpress.org/plugins/local-development/",
    "required": true
  }
]
```

You will then need to update `wp-dependencies.json` to suit your requirements.

3. Finally add the following lines to your plugin or theme's `functions.php` file:

```php
require_once __DIR__ . '/vendor/autoload.php';
WP_Dependency_Installer::instance()->run( __DIR__ );
```

4. (optional) Take a look at some of built in [Hooks](https://github.com/afragen/wp-dependency-installer/wiki/Actions-and-Hooks) and [Functions](https://github.com/afragen/wp-dependency-installer/wiki/Helper-Functions) to further customize your plugin look and behaviour:

```php
/**
 * Display your plugin or theme name in dismissable notices.
 */
add_filter(
  'wp_dependency_dismiss_label',
  function( $label, $source ) {
    $label = basename(__DIR__) !== $source ? $label : __( 'Group Plugin Installer', 'group-plugin-installer' );
    return $label;
  }, 10, 2
);
```

That's it, happy blogging!

## Development

PRs are welcome against the `develop` branch.
