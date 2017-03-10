---
layout: post 
comments: true
title: Creating Composer Package
---

Composer is the *defacto* standard for managing dependencies in PHP world. Dependency management helps you organize your code, bundle them as packages and make the code easily sharable.

Most of the beginer PHP developer find composer to be overwhelming. In this post we'll try to try to understand composer and create a **Library Package**.

### Prerequisites

* Composer
* Namespace
* PSR-4 (Autoload)
* git, packagist, semver


#### Namespace

Although namespace is not necessarily required for composer, it's advised to create your package in it's own namespace so that your classes doesn't collide with others'.

#### PSR-4 (Autoload)

PSR-4 provides a clean way to autoload our classes.

#### Git and Packagist and Semver

Composer utilizes `git tag` for package version. packagist.org is the default registry where you register the location of your git repo for the library. You should follow semver for versioning.



##  Creating the Package

Before wrapping the libaray into a package, we need to create it first.

### Directory Structure

Our project root will be `demopackage`.  And we'll create our library class in src directory. For simplicity we'll just create a single Demo class. But we can create as many classes as the library requires.

Demo.php

```php
<?php
  
namespace Bakhari\DemoPackage;

class Demo
{
  public function run()
  {
    return "I'm Running!";
  }
}
```

After creating the Demo.php our directory structure should look like:

```
demopackage
└── src
    └── Demo.php
```



### package.json

package.json is the file that defines your project directory as composer package. We can use `composer init` for creating it.

```
$ composer init

  Welcome to the Composer config generator

This command will guide you through creating your composer.json config.

Package name (<vendor>/<name>) [bdryagya/demopackage]: bakhari/demopackage
Description []: Composer Demo Library
Author [Yagya Chaudhary <mail@bdryagya.com.np>, n to skip]:
Minimum Stability []: stable
Package Type (e.g. library, project, metapackage, composer-plugin) []: library
License []: MIT

Define your dependencies.

Would you like to define your dependencies (require) interactively [yes]? no
Would you like to define your dev dependencies (require-dev) interactively [yes]? no

{
    "name": "bakhari/demopackage",
    "description": "Composer Demo Library",
    "type": "library",
    "license": "MIT",
    "authors": [
        {
            "name": "Yagya Chaudhary",
            "email": "mail@bdryagya.com.np"
        }
    ],
    "minimum-stability": "stable",
    "require": {}
}

Do you confirm generation [yes]?
```

This generates a composer.json file in your project root directory and the directory structure should look like:

```
demopackage
├── composer.json
└── src
    └── Demo.php
```



### Autoloading class

Next, we'll define PSR-4 autoload for our library classes. Edit your composer.json file and add the autoload.

```
{
    "name": "bakhari/demopackage",
    "description": "Composer Demo Library",
    "type": "library",
    "license": "MIT",
    "authors": [
        {
            "name": "Yagya Chaudhary",
            "email": "mail@bdryagya.com.np"
        }
    ],
    "minimum-stability": "stable",
    "require": {},
    "autoload": {
        "psr-4": {
            "\\Bakhari\\DemoPackage\\": "src/"
        }
    }
}
```

The autoload binds the the namespace `Bakhari\DemoPackage` to directory 'src' that means whenever `Bakhari\DemoPackage` is referenced it searches the class in 'src' directory.



### Further Reading

* [Composer](https://getcomposer.org)
* [PHP Namespaces](http://php.net/manual/en/language.namespaces.php)
* [PSR](http://www.php-fig.org/psr/)
* [Semantic Versioning](http://semver.org/#semantic-versioning-200)
