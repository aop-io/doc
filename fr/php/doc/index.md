---
tpl   : doc
title : Documentation de PHP AOP
---


## AOP ?

L'_AOP_ ("Aspect Oriented Programming", en français : "Programmation Orienté Aspect") est un paradigme de programmation.

Tout comme la _POO_ propose un style de programmation avec ses caractéristiques, l'_AOP_ en propose un autre avec d'autres caractéristiques.

Pour faire court, l'_AOP_ propose un style de programmation pour intercepter du code et en changer le comportement.

L'_AOP_ permet de rendre son code encore plus modulaire en séparrant le code métier et les aspects techniques (préoccupations transversales) tels que la gestion du cache, log, debug, ...

A noter que l'_AOP_ s'utilise parfaitement en programmation orienté objet (POO), tout comme en programmation procédurale.

Cette documentation n'ayant pas pour but d'expliquer en détail le concept de l'_AOP_, si vous souhaitez en savoir plus n'hésitez pas à consulter la [page dédiée à l'AOP sur Wikipedia](http://fr.wikipedia.org/wiki/Programmation_orient%C3%A9e_aspect).


## PHP AOP

[PHP-AOP](https://github.com/aop-io/php-aop) est une lib PHP qui implémente le paradigme de l'AOP
(Aspect Oriented Programming).

Une seule dépendance, [l'intercepteur de code](interceptors).

_PHP-AOP_ fournit une API complète et facile à utiliser pour la _programmation orienté aspect_ en PHP.

Conçu en tant qu'une couche d'abstraction, _PHP-AOP_ peut fonctionner avec plusieurs intercepteurs de code PHP.
Ainsi, il est possible d'augmenter et d'adapter les capacités d'interception tout en conservant une API unique respectant le paradigme de l'AOP.

Pour l'instant l'intercepteur le plus complet est basé sur l'extension [PECL AOP-PHP](interceptors/pecl-aop-intercepteur). D'autres [intercepteurs sont attendus](interceptors).

Liens utiles :
  * [PHP-AOP sur GitHub](https://github.com/aop-io/php-aop)
  * [L'API doc](/api/php) pour obtenir l'ensemble des fonctionnalités de la lib _PHP-AOP_.

La prochaine section de cette documentation explique comment [intercepter du code avec la lib PHP-AOP](interception.html).