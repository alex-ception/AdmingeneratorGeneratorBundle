# Installation via composer

---------------------------------------

### 1. Download files

Add Admingenerator to your `composer.json`:

```json
"require": {
    "cedriclombardot/admingenerator-generator-bundle": "dev-master"
},
```

Then run `php composer.phar update` command.

> **Note:** If you're getting **no matching package found** error then you must also add `"minimum-stability": "dev"` to your **composer.json** file.
    
### 2. Enable bundles

Admingenerator has a dependency on KnpMenuBundle and WhiteOctroberPagerfantaBundle.

> **Note:** there are also some optional dependencies, each is described in corresponding feature`s doc. This guide describes only the minimal-setup. 

Enable Admingenerator and its dependencies in your `app/AppKernel.php`:

```php
<?php 
public function registerBundles()
{
    $bundles = array(
        // ...
        new Admingenerator\GeneratorBundle\AdmingeneratorGeneratorBundle(),
        new Knp\Bundle\MenuBundle\KnpMenuBundle(),
        new WhiteOctober\PagerfantaBundle\WhiteOctoberPagerfantaBundle(),
    );
}
```

### 3. Basic configuration

Choose your model manager - add following lines to `app/config/config.yml`:

```yaml
admingenerator_generator:
    # choose only one
    use_propel:           false
    use_doctrine_orm:     true
    use_doctrine_odm:     false
```

Enable translation of KnpMenu - add following lines to `app/config/config.yml`:</p>

```yaml
knp_menu:
    twig:
        template: AdmingeneratorGeneratorBundle:KnpMenu:knp_menu_trans.html.twig
```

Choose basic admingenerator template - with or without assetic.

```yaml
admingenerator_generator:
    # choose and uncomment only one
#    base_admin_template: AdmingeneratorGeneratorBundle::base_admin.html.twig
#    base_admin_template: AdmingeneratorGeneratorBundle::base_admin_assetic_less.html.twig
```

### (Optional) Configure Assetic & YUI comperssor

By default, the `base_admin.html.twig` uses YUI Compressor to minify assets and combine them into one file (less HTTP requests).

In order to properly install and configure YUI Compressor follow [this article](http://symfony.com/doc/current/cookbook/assetic/yuicompressor.html)

> See also [Asset Management](http://symfony.com/doc/current/cookbook/assetic/asset_management.html) cookbook entry.

### Install assets

To install assets in your web directory run:

`php app/console assets:install web --symlink`

> **Note:** We recommend installing assets with `--symlink` option, however you may use the `--hardcopy` option instead.

### (Optional) Dump assets

If you're useing assetic for asset management dump your assets by running:

`php app/console assetic:dump`