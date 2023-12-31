# Filament Blog - Sellarix

Module can be purchased: https://checkout.anystack.sh/sellarix-fillament-blog

This package provides a full blog module:

Functionality available:

- Multiple Post Types
- Blog Categories
- Blog Posts
- Blog Tags
- Author Connection
- Latest Posts
- Widget for latest posts

Responsive livewire with tailwind and darkmode. 

Backend configuration uses Fillament. 

## Requirements

-   PHP 8.1
-   [Filament 3](https://github.com/laravel-filament/filament)

## Dependencies

-   [filament/spatie-laravel-media-library-plugin](https://github.com/filamentphp/spatie-laravel-media-library-plugin)
-   [laravel/scout](https://github.com/laravel/scout)
-   [codewithdennis/filament-select-tree](https://github.com/CodeWithDennis/filament-select-tree)


## Installation

You can publish the config file with:

```bash
php artisan vendor:publish --tag="blog-config"
```

You can publish the view resource files with:

```bash
php artisan vendor:publish --tag="blog-views"
```

Dont forget to run your migrations:

```bash
php artisan migrate
```

### Auto register plugin against multiple panels

From within your ``config/blog.php``  you can set auto_apply to true and define the names of each panel to auto register against


```php
'fillament' => [
    'auto_apply' => true,
    'panels' => [
        'admin'
    ]
],

```

you can also define the blog route domain or prefix via the config:

```php
'routes' => [
    'prefix' => '',
    'domain' => '',
],
```

From within the config you can define the author model config

```php
'author' => [
    'author_model' => User::class
],
```





That's it! You can now see your blog on the frontend and start adding posts from your admin panel.


Author:
- Sellarix: https://sellarix.com
- github_url: https://github.com/sellarix/laravel-blog
- linkedin_url: https://www.linkedin.com/company/sellarix-ltd/
