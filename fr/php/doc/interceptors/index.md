---
tpl   : doc
title : Intercepteurs de code pour PHP AOP
---

La lib [php-aop](/fr/php/doc) fournit un cadre de développement pour la programmation orienté aspect (AOP).
_php-aop_ se base sur un intercepteur de code pour effectuer l'interception (le pointcut).

Certains intercepteurs ne supportent pas toutes les fonctionnalités de _php-aop_.
La lib étant encore jeune, il y a pour l'instant que de 2 intercepteurs avec chacun ses qualités et ses défauts.


## Liste des intercepteurs

<table class="table table-bordered table-hover table-condensed table-striped">
  <tr>
    <td>[pecl-aop-interceptor](pecl-aop-interceptor)</td>
    <td>Recommandé, pour l'instant l'intercepteur le plus performant et qui supporte le plus de fonctionnalité de la lib _php-aop_.
    </td>
  </tr>
  <tr>
    <td>[patchwork-interceptor](patchwork-interceptor)</td>
    <td>Un intercepteur en version alpha réalisé pour la R&D.</td>
  </tr>
</table>


A faire :

<table class="table table-bordered table-hover table-condensed table-striped">
  <tr>
    <td>laravel-interceptor</td>
    <td>Pour utiliser _php-aop_ dans le framework _Laravel_.
    _Laravel_ utilise un container principal, ça pourrait offrir approche intéressante pour intercepter les appels de méthodes et propriétés de classes (peut être coupler avec les évènements).
    </td>
  </tr>
  <tr>
    <td>silex-interceptor</td>
    <td>Pour utiliser _php-aop_ dans le micro-framework [Silex](http://silex.sensiolabs.org/).
    Dans _Silex_ tout passe par le container principal basé sur _Pimple_.
    Passer par là me semble être un excellent moyen d'intercepter le code par une simple enveloppe (wrapper).
    </td>
  </tr>
  <tr>
    <td>symfony-interceptor</td>
    <td>Pour utiliser _php-aop_ dans le framework [Symfony](http://symfony.com).
    _Symfony_ utilisant un proxy, c'est parfait pour créer cet intercepteur vue qu'il est possible de réécrire les classes en cache et aussi de manipuler le proxy. Il existe d'ailleurs un [bundle apportant l'AOP dans Symfony](https://github.com/schmittjoh/JMSAopBundle).
    </td>
  </tr>
</table>


## Créer un intercepteur

Pour faciliter la création d'intercepteur de code, vous pouvez utiliser le  [skeleton-interceptor](https://github.com/aop-io/skeleton-interceptor) qui implémente toutes les méthodes nécessaires.

Il suffit de renommer `skeleton` par le nom que vous donnez à votre intercepteur et remplir les méthodes.

Ne vous souciez pas de la logique des points de jointures (est-ce que tel joint point a cette méthode, etc), cette logique est nativement gérée par la lib `php-aop`, remplissez simplement les méthodes du skeleton.

N'hésitez pas à vous inspirer des [autres intercepteurs](https://github.com/aop-io), ça aide.

Lorsque votre intercepteur est fonctionnel, si vous souhaitez le rendre public sur AOP.io contactez moi (email dans mon [profil Github](https://github.com/Nicolab) ou en ouvrant une [issue dans php-aop](https://github.com/aop-io/php-aop/issues/new)) pour que j'ajoute le repository `https://github.com/aop-io/votre-interceptor` et que je vous ajoute en tant que membre de  l'organisation [https://github.com/aop-io](https://github.com/aop-io) avec les accès complet au repository de votre intercepteur (push, merge, gestion des issues, etc).

