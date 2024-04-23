# Filament Blog - Sellarix


---
- name: Sellarix
- github_url: https://github.com/sellarix/laravel-blog
- linkedin_url: https://www.linkedin.com/company/sellarix-ltd/
---

This package provides a full blog module for both frontend livewire components and backend filament management

_Functionality available:_

- Multiple Post Types
- Blog Categories
- Blog Posts
- Blog Tags
- Author Connection
- Latest Posts
- Widget for latest posts


## Requirements

Requirements are included as part of the composer requirements but follow installation for each as additional steps.

-   PHP 8.1
-   [Filament 3](https://filamentphp.com/docs/3.x/panels/installation)
-   [Livewire 3] (https://livewire.laravel.com/docs/installation)
-   [Tailwind 3](https://tailwindcss.com/docs/guides/laravel) Install tailwind via the laravel documentation

Make sure you have the following tailwind plugins installed

```js
require('@tailwindcss/forms'),
require('@tailwindcss/typography'),
require('@tailwindcss/line-clamp')
```

## Dependencies

Again you will need to follow the install steps of the following dependencies

-   [filament/spatie-laravel-media-library-plugin](https://github.com/filamentphp/spatie-laravel-media-library-plugin)
-   [laravel/scout](https://github.com/laravel/scout)
-   [codewithdennis/filament-select-tree](https://github.com/CodeWithDennis/filament-select-tree)


## Installation

You can publish the config file with:

You will need to register the blog plugin directly within your panel provider. 

```php
->plugins([
    \Sellarix\Blog\Filament\BlogPlugin::make()
])
```

Then you can do either of the following

1. Run the following command to install the blog module

```bash 
php artisan router:install #we use a router module to handle routing
php artisan blog:install #will ask to run migrations and publish required files
```
2. Run the standard commands to install the blog module

```bash
php artisan vendor:publish --tag="blog-config"
php artisan vendor:publish --tag="blog-views"
php artisan migrate
```

### Optional: 

You can also add our router plugin to show the routes in your admin panel

```php
->plugins([
    \Sellarix\Router\Filament\RouterPlugin::make() // this is optional if you want to show the routes in your admin
])
```

## configuration

If you do not intend to use melisearch or algolia, please make sure you set the following env vars in your ```.env```

We use the Scout driver for internal blog searches

```env
SCOUT_DRIVER=database
```

Define the blog prefix and domain within the config file ```config/blog.php```

```php
'routes' => [
    'prefix' => '',
    'domain' => '',
],
```

From within the config you can define the author model config this is the user model it must contain a name field.

```php
'author' => [
    'author_model' => User::class
],
```

If you want to show share buttons on the widgets and view pages you can set the following in the config file

```php
'show_share' => true,
```

That's it! You can now see your blog on the frontend and start adding posts from your admin panel.


### Additional 

To handle redirects:

add the following middleware to your app/kernel.php

```php
    protected $middleware = [
        ...
        \Sellarix\Router\Middleware\DatabaseRouter::class,
    ];
```

Add the following to your theme for tailwind users, to give a shine to the tags

```json
theme: {
    extend: {
        animation: {
            shine: "shine 1s",
        },
        keyframes: {
            shine: {
                "100%": {left: "125%"},
            },
        }
    },
},
```

using tailwind your ```postcss.config.js``` must also include the following

```js
export default {
    plugins: {
        "postcss-import": {},
        "tailwindcss/nesting": {},
        tailwindcss: {},
        autoprefixer: {},
    },
};
```

If you are using our in-built css assets make sure you define theme/colours within your ```tailwind.config.js```
Change the colours accordingly to match your theme.

```json
 theme: {
    extend: {
        colors: {
          "primary": {
                "25": "#e7eefd",
                    "50": "#b8ccf9",
                    "100": "#89aaf5",
                    "200": "#5a87f1",
                    "300": "#2B65EE",
                    "400": "#114CD4",
                    "500": "#0F41B6",
                    "600": "#0e3ba5",
                    "700": "#0a2a76",
                    "800": "#061947",
                    "900": "#020818",
            },
            "secondary": {
                "25": "#e5f5ff",
                    "50": "#b3e2ff",
                    "100": "#80ceff",
                    "200": "#4dbaff",
                    "300": "#1aa7ff",
                    "400": "#009AFA",
                    "500": "#008de6",
                    "600": "#006eb3",
                    "700": "#004f80",
                    "800": "#002f4d",
                    "900": "#00101a",
            },
        }
    },
},
```
