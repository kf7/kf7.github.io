# Kohana framework 7

PHP-7-compatible replacement for [Kohana](https://github.com/kohana)/[Koseven](https://github.com/koseven) framework.

## Features

Fully compatible with PHP 7, modern and pure code:

- Namespaces, type declarations, `Throwable` errors/exceptions
- Strict separation of classes into static and dynamic
- Maximum "chainable" methods
- Minimum static and [magic methods](https://www.php.net/manual/en/language.oop5.magic.php)
- PHP polyfills

[PSR](https://www.php-fig.org/psr/) compatible:

- PSR-1, PSR-12 coding style
- PSR-4 autoloading
- ~~PSR-3 logging~~
- ~~PSR-11 containers~~
- ~~PSR-16 caching~~
- ~~PSR-7, PSR-15, PSR-17, PSR-18 HTTP routing~~

## Requirements

- PHP >= 7.1
- PHP extensions:
  - [mbstring](https://www.php.net/manual/en/book.mbstring.php)
  - [filter](https://www.php.net/manual/en/book.filter.php)
  - [iconv](https://www.php.net/manual/en/iconv.installation.php)
- Composer packages:
  - [symfony/polyfill](https://github.com/symfony/polyfill)
  - ~~[psr/log](https://packagist.org/packages/psr/log)~~
  - ~~[psr/container](https://packagist.org/packages/psr/container)~~
  - ~~[psr/simple-cache](https://packagist.org/packages/psr/simple-cache)~~
  - ~~[psr/http-message](https://packagist.org/packages/psr/http-message)~~
  - ~~[psr/http-factory](https://packagist.org/packages/psr/http-factory)~~
  - ~~[psr/http-client](https://packagist.org/packages/psr/http-client)~~
  - ~~[psr/http-server-middleware](https://packagist.org/packages/psr/http-server-middleware)~~

## Packages

A package is the basic structure for applications and modules.

### Structure

Common directories:

- `src`_*_ - source files (classes, interfaces)
- `tests`_*_ - unit tests
- `config` - configuration files
- `views` - templates
- `i18n` - translation/message files
- `media` - assets files (images, fonts, scripts, styles)
  - `public` - public files
- `vendor` - external packages (dependencies)
- `docs` - documentation

System:

- `src/System/Kohana.php`_*_ - framework manager extended `KF7\System\AbstractKohana`

Module:

- `src/{Module}/Module.php`_*_ - module manager extended `KF7\System\AbstractModule`

Application:

- `src/Application/Application.php`_*_ - application manager extended `KF7\System\AbstractApplication`
- `cache` - temp/cache files
- `logs` - error logs

_*_ - required directories and files



## Backward incompatible changes

[Upgrading Kohana to Koseven](https://koseven.ga/documentation/kohana/upgrading-from-kohana).

Upgrading Koseven to KF7, breaking changes:

- Package directories:
  - Renamed `classes` to `scr`
  - Deleted `messages`, messages moved into `i18n` files
- Package sources must be in namespace with prefix `{Vendor}\{Package}\`:
  - `{Vendor}` is vendor/contributor name, for framework packages it's `KF7`
  - `{Package}` is package name where class/interface was defined, main packages: system - `System`, application - `Application`
- Package must contain implementation of `KF7\System\PackageInterface`:
  - System: `class KF7\System\Kohana extends KF7\System\AbstractKohana`
  - Application: `class KF7\Application\Application extends KF7\System\AbstractApplication`
  - Module: `class {Vendor}\{Package}\Module extends KF7\System\AbstractPackage` instead deleted file `init.php`
- Global constants removed, replace them with
  - `dirname($_SERVER['PHP_SELF'])` instead `DOCROOT`
  - `KF7\System\Kohana::getPath()` instead `SYSPATH`
  - `KF7\Application\Application::getPath()` instead `APPPATH`
- New class extension

  ~~~php
  class KO7_Module_Classname {
      <...>
  }
  class Module_Classname extends KO7_Module_Classname {}
  ~~~

  changed to

  ~~~php
  namespace KF7\Module;
  abstract class AbstractClassname
  {
      <...>
  }
  class Classname extends AbstractClassname
  {
  }
  ~~~

- Removed `factory`/`instance` methods, create [factory classes](https://designpatternsphp.readthedocs.io/en/latest/Creational/FactoryMethod/)
- Sepatate setter and getter methods: `KO7::modules()`
- Initialize stratic classes implemented `KF7\System\StaticInterface` at loading.
