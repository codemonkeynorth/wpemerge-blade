# WP Emerge Blade

Enables the use of Blade views in [WP Emerge](https://github.com/htmlburger/wpemerge).

## Quickstart

1. Run `composer require htmlburger/wpemerge-blade` in your theme directory
1. Add `\WPEmergeBlade\View\ServiceProvider` to your array of providers when booting WP Emerge:
    ```php
    WPEmerge::bootstrap( [
        'providers' => [
            \WPEmergeBlade\View\ServiceProvider::class,
        ],
    ] );
    ```
1. If you are using the [WP Emerge Starter Theme](https://github.com/htmlburger/wpemerge-theme) you can replace your theme views with the ones inside `theme/alternative/blade/`.

## Options

Default options:
```php
[
    // Automatically replace the default view engine for WP Emerge.
    'replace_default_engine' => true,
    
    // Pass .php views to the default view engine.
    // replace_default_engine must be true for this to take effect.
    'proxy_php_views' => true,
    
    // Options passed directly to Blade.
    'options' => [
        'views' => get_stylesheet_directory(),
        'cache' => get_stylesheet_directory() . DIRECTORY_SEPARATOR . 'cache' . DIRECTORY_SEPARATOR . 'blade',
    ],
]
```

You can change these options by specifying a `blade` key in your WP Emerge config array:
```php
WPEmerge::bootstrap( [
    // ... other WP Emerge options
    'blade' => [
        // ... other WP Emerge Blade options
        'options' => [
            // ... other Blade options
            'cache' => get_stylesheet_directory() . DIRECTORY_SEPARATOR . 'blade-cache',
        ],
    ],
] );
```

## Extending Blade

You can use the following to extend blade with a custom directive, for example:
```php
// WPEmerge::resolve() used for brevity's sake - use a Service Provider instead.
$blade = WPEmerge::resolve( WPEMERGEBLADE_VIEW_BLADE_VIEW_ENGINE_KEY );
$blade->compiler()->directive( 'mydirective', function( $expression ) {
    return "<?php echo 'MyDirective: ' . $expression . '!'; ?>";
} );
```
With this, you now have your very own custom Blade directive:
```blade
@mydirective('foobar')
```

More information on how you can extend Blade is available on [https://laravel.com/docs/5.4/blade#extending-blade](https://laravel.com/docs/5.4/blade#extending-blade)
