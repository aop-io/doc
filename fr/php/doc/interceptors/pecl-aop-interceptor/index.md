---
tpl   : doc
title : Intercepteur PECL AOP
---

Intercepteur utilisant l'extension PHP [PECL AOP](https://github.com/AOP-PHP/AOP) pour la [lib PHP AOP.io](https://github.com/aop-io/php-aop) (php-aop).

Fournit une couche d'abstration à l'extension _PECL AOP_,
avec de nombreuses fonctionnalités pour aller plus loin dans la manipulation de l'AOP avec PHP,
au-delà des possibilités de l'extension de _PECL_.

La documentation qui suit concidaire que vous avez déjà installé la [lib PHP de AOP.io](https://github.com/aop-io/php-aop).


## Démarrage

### Installer PECL AOP

Vous pouvez au choix utiliser _pecl_

```sh
    sudo pecl install aop-beta
```

ou

Téléchargez l'extension _AOP PHP_ depuis Github, compilez et ajoutez l'extension à votre _php.ini_

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


Maintenant, vous pouvez ajouter la ligne suivante à votre _php.ini_ pour activer l'extension _AOP_

```ini
    extension=AOP.so
```

Plus de documentation sur le [repository PECL AOP](https://github.com/AOP-PHP/AOP).


### Installer pecl-aop-interceptor

Téléchargez [pecl-aop-interceptor](https://github.com/aop-io/pecl-aop-interceptor/archive/master.zip) (et configurez votre autoloader) ou utilisez _composer_ `require: "aop-io/pecl-aop-interceptor"`.


### Utilisation

```php
use Aop\Aop;

// Init
$aop = new Aop([ 'php_interceptor' => '\PeclAop\PeclAopInterceptor']);
```

L'extension _PECL AOP_ supporte le selecteur wilcard, exemple :

```php
Aop::addBefore('MyClass::get*()', function($jp) {
  // votre hack ici
});
```

La syntaxe des sélecteurs de point de coupe (pointcut) de l'extension _PECL AOP_
est documentée sur la page [PECL AOP (pointcuts syntax)](https://github.com/AOP-PHP/AOP/blob/master/doc/Contents/chapter2.md#pointcuts-syntax).

A part les sélecteurs supportés et leurs syntaxes, l'utilisation de _php-aop_ est identique aux autres intercepteurs.
