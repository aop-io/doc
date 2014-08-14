---
tpl   : doc
title : Intercepteur Patchwork
---

Intercepteur utilisant [stream wrapper](http://php.net//manual/fr/class.streamwrapper.php) de PHP via le package [Patchwork](https://github.com/antecedent/patchwork).

Cet intercepteur a été créé seulement pour la R&D concernant la possibilité de passer par un gestionnaire de protocole et de flux PHP (stream wrapper), il ne supporte pas les interceptions de type "around", ni l'interception des propriétés.

Utilisez le simplement pour votre propre R&D (ou faire mumuse) ou pour vous inspirer lors de la création d'un intercepteur.

La lib _Patchwork_ n'étant pas créé pour l'usage de l'AOP, cet intercepteur n'a pas d'avenir. Cependant passer par une _stream wrapper_ de PHP pour créer un intercepteur est une solution viable !

Si vous vous sentez le courage (ou le besoin) de créer un intercepteur basé sur _stream wrapper_, <a target="_blank" href="http://nicolab.net" title="Nicolas Talle">faites moi signe</a>, je vous aiderai ;)

Voir [patchwork-interceptor sur Github](https://github.com/aop-io/patchwork-interceptor).


## Démarrage

### Installer pecl-aop-interceptor

Téléchargez [patchwork-interceptor](https://github.com/aop-io/patchwork-interceptor/archive/master.zip) (et configurez votre autoloader) ou utilisez _composer_ `require: "aop-io/patchwork-interceptor"`.


### Utilisation

```php
use Aop\Aop;

// Init
$aop = new Aop([ 'php_interceptor' => '\PatchworkInterceptor\PatchworkInterceptor']);
```

L'utilisation de la couche d'abstraction [PHP-AOP](http://aop.io/fr/php/doc) est documentée [AOP.io](http://aop.io).


