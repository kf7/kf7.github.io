---
layout: default
title: About
---
# About KF7

PHP-7-compatible replacement for [Kohana](https://github.com/kohana) and [Koseven](https://github.com/koseven) frameworks.

## Features

Fully compatible with PHP 7, modern and pure code:

- New syntax: namespaces, type declaration and [throwables](https://www.php.net/manual/en/class.throwable.php)
- Strict separation of static and dynamic classes and getter/setter methods
- More interfaces and "chainable" methods
- Less static and [magic methods](https://www.php.net/manual/en/language.oop5.magic.php)
- PHPDoc comments

[PSR](https://www.php-fig.org/psr/) compatible:

- PSR-12 coding style
- PSR-5, PSR-19 documentation
- PSR-4 autoloading
- PSR-3 logging
- PSR-16 caching
- ~~PSR-11 containers~~
- ~~PSR-7, PSR-15, PSR-17, PSR-18 HTTP routing~~

## Requirements

- PHP >= 7.2
- PHP extensions:
  - [mbstring](https://www.php.net/manual/en/book.mbstring.php)
  - [filter](https://www.php.net/manual/en/book.filter.php)
  - [hash](https://www.php.net/manual/en/book.fhash.php)
  - [iconv](https://www.php.net/manual/en/book.iconv.php)

## Structure

- `src` - source code (classes, interfaces)
- `tests` - unit tests
- `config` - configuration files
- `views` - templates
- `i18n` - translation and messages
- `media` - assets files (scripts, styles, images and etc.)
- `docs` - documentation
- `vendor` - Composer packages (dependencies)

## Backward incompatible changes

[Upgrading Kohana to Koseven](https://koseven.ga/documentation/kohana/upgrading-from-kohana)

Upgrading Koseven:

- Directories
  - `/classes` renamed to `/scr`
  - `/guide` renamed to `/docs`
  - `/utf8` and `/messages` are removed (messages moved into `/i18n`)
- Global constants (`SYSPATH`, `APPPATH` and etc.) are removed (use `Kohana\Filesystem` instead)
- Classes/interfaces are renamed
  ~~~php
  <?php
  class Kohana_Classname {
      <...>
  }
  ~~~
  ~~~php
  <?php
  class Classname extends Kohana_Classname {}
  ~~~
  changed to
  ~~~php
  <?php
  namespace Kohana;
  abstract class AbstractClassname
  {
      <...>
  }
  ~~~
  ~~~php
  <?php
  namespace Kohana;
  class Classname extends AbstractClassname
  {
  }
  ~~~
- `factory` and `instance` methods are replaced to [factory classes](https://designpatternsphp.readthedocs.io/en/latest/Creational/FactoryMethod/)
- Sepatated setters and getters: `Kohana::modules()` to `Kohana\Kohana::getModules()` and `Kohana\Kohana::setModules()`
- Initialize static classes implemented `Kohana\StaticInterface` at class autoloading
