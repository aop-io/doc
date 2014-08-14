---
tpl   : doc
title : PECL AOP interceptor
---


Interceptor using [PECL AOP extension](https://github.com/AOP-PHP/AOP) for [PHP AOP.io lib](https://github.com/aop-io/php-aop) (php-aop).

Provides an abstraction layer of 'PECL AOP extension',
with many features to go further in the handling of the AOP with PHP.
Beyond the possibilities of the _PECL_ extension.

This package is an adapter for [PHP AOP.io lib](https://github.com/aop-io/php-aop) (an abstraction layer easy to use). The doc below assumes that you have already installed the [PHP AOP.io lib](https://github.com/aop-io/php-aop).

See [pecl-aop-interceptor on Github](https://github.com/aop-io/pecl-aop-interceptor).


## Getting Started

### Install PECL AOP

You can use _pecl_

```sh
    sudo pecl install aop-beta
```

or

Download the AOP PHP extension from github, compile and add the extension to your _php.ini_

```sh
    #Clone the repository on your computer
    git clone https://github.com/AOP-PHP/AOP
    cd AOP
    #prepare the package, you will need to have development tools for php
    phpize
    #compile the package
    ./configure
    make
    #before the installation, check that it works properly
    make test
    #install
    make install
```

Now you can add the following line to your _php.ini_ to enables AOP extension

```ini
    extension=AOP.so
```

More doc on [PECL AOP repository](https://github.com/AOP-PHP/AOP).


### Install pecl-aop-interceptor

Download [pecl-aop-interceptor](https://github.com/aop-io/pecl-aop-interceptor/archive/master.zip) (and configure your autoloader) or use composer `require: "aop-io/pecl-aop-interceptor"`.


### Usage

```php
use Aop\Aop;

// Init
$aop = new Aop([ 'php_interceptor' => '\PeclAop\PeclAopInterceptor']);
```

The _PECL AOP_ extension support the wilcard selector, example:

```php
Aop::addBefore('MyClass::get*()', function($jp) {
  // your hack here
});
```

The syntax of pointcuts selectors of _PECL AOP_ extension is documented on the page [PECL AOP (pointcuts syntax)](https://github.com/AOP-PHP/AOP/blob/master/doc/Contents/chapter2.md#pointcuts-syntax).

The usage of the AOP abstraction layer is documented on [AOP.io](http://aop.io).

