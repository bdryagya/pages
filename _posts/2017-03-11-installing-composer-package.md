---
layout: post
comments: true
title: Installing Composer Package
---

We can install composer package in two way. The first, we define our dependencies in `require` block of `composer.json` and run `composer install`. And the other we can require the package on the fly by running `composer require vendor/package`, which install the package and updates composer.json as well.

### Prerequisites

* Composer

## Finding the Package

We can use `composer search <package>` or goto [https://packagist.org](https://packagist.org) and search the required package.

```
$ composer search demopackage
bakhari/demopackage Composer Demo Library
fuelphp/demo-package FuelPHP demo component
azrodin/demo-package Demo Laravel 4 Package. Create for learning purposes...
sham/demo-package descripción del paquete de ejemplo
hoangtube/demo-package This is the first package i've ever make
addic-programmer/demo-package The Laravel Framework.
```



## Installing the package

Once we find required package we can install it with `composer require bakhari/demopackage`.

```
$ composer require bakhari/demopackage
Using version ^1.0 for bakhari/demopackage
./composer.json has been updated
Loading composer repositories with package information
Updating dependencies (including require-dev)
Nothing to install or update
Generating autoload files
```

Since we've not specified any version constraint, it'll download the latest release of the package. More on version can be found at [https://getcomposer.org/doc/articles/versions.md](https://getcomposer.org/doc/articles/versions.md)

The installation process, installs the dependency in `vendor/<vendorname>/<package>` directory by default. And now we can see `composer.lock` file in our root directory, which contains a copy of information of packages installed along with version constraints. Since we exclude `vendor` directory in our project repo, it's recommended to keep `composer.lock` commited in project repo. It instructs composer to use the defined version when we run `composer install` in our project somewhere else(staging, production, other environment).

At the end of the installation composer generates the autoload files reading the `autoload` block of the package's `composer.json`. Basically it registers autoload function using `spl_autoload_register`.

## Using the Package

Now as we have installed the package, we can use it as any other regular class.

```php
<?php

# Autoloader
require __DIR__ . '/vendor/autoload.php';

use Bakhari\DemoPackage\Demo;

$demo = new Demo;

echo $demo->run() . PHP_EOL;

```

## Package info and Updates

We can query installed packages using `composer show`. We can find detail of a particular package with `composer show vendor/packagename`

```
$ composer show bakhari/demopackage
name     : bakhari/demopackage
descrip. : Composer Demo Library
keywords :
versions : * 1.0.0
type     : library
license  : MIT License (MIT) (OSI approved) https://spdx.org/licenses/MIT.html#licenseText
source   : [git] https://github.com/bdryagya/demopackage.git 435234cc51fd5cfa46e72a3fae357e2ff4d16c57
dist     : [zip] https://api.github.com/repos/bdryagya/demopackage/zipball/435234cc51fd5cfa46e72a3fae357e2ff4d16c57 435234cc51fd5cfa46e72a3fae357e2ff4d16c57
names    : bakhari/demopackage

autoload
psr-4
Bakhari\DemoPackage\ => src/
```

We can see if any updates of the installed packages are available with `composer show -l`. If we want to update the package, we can run `composer update vendor/packagename`.

