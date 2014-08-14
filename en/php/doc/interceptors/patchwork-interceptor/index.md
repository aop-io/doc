---
tpl   : doc
title : Patchwork interceptor
---

Interceptor using [stream wrapper](http://php.net//manual/en/class.streamwrapper.php) of PHP via the [Patchwork](https://github.com/antecedent/patchwork) package.

This interceptor was created only for _R&D_ concerning the possibility of going through a protocol handler and PHP stream (stream wrapper), it does not support the interception of "around" kind, nor the interception of properties.

Use just for your own _R&D_ (or playing) or to inspire you when creating an interceptor.

The lib _Patchwork_ is not being created for use of AOP, so this interceptor has no future. However, the PHP _stream wrapper_ to create an interceptor is a viable solution!

See [patchwork-interceptor on Github](https://github.com/aop-io/patchwork-interceptor).


## Getting Started

### Install pecl-aop-interceptor

Download [patchwork-interceptor](https://github.com/aop-io/patchwork-interceptor/archive/master.zip) (and configure your autoloader) or use composer `require: "aop-io/patchwork-interceptor"`.


### Usage

```php
use Aop\Aop;

// Init
$aop = new Aop([ 'php_interceptor' => '\PatchworkInterceptor\PatchworkInterceptor']);
```

The usage of the [PHP-AOP](http://aop.io/en/php/doc) abstraction layer is documented on [AOP.io](http://aop.io).

