---
tpl   : doc
title : Interception de code avec PHP AOP
---

## Aop::AddBefore()

Ajoute l'advice _avant_ l'exécution d'une action.

Signature de la méthode [Aop::addBefore()](/api/php/class-aop-aop.html#_addBefore) :

```php
Aop::AddBefore(
  string $selector,
  callable $callback,

  // Arguments facultatifs
  array $options = [],
  int $kind      = null,
  string $name   = null
);
```

Exemple, ajouter l'advice _avant_ l'exécution d'une méthode :

```php
Aop::addBefore('Article::add()', function($jp) {

  $args = $jp->getArgs();

  $jp->setArgs( SomeValidator::validateArticle($args) );
});
```

Dans cet exemple, considérons que nous avons un validateur `SomeValidator::validateArticle()` qui vérifie que les données sont valides et qui fait quelques pré-traitement, par exemple le validateur crée l'URL de l'article à partir du titre pour avoir une belle URL (slug).

Si la validation échoue alors une `Exception` PHP est levée, la méthode `$jp->setArgs()` n'est donc pas exécutée compte tenu qu'une exception PHP a interrompu l'éxecution du code.

Dans le cas où il n'y a pas d'erreur, la méthode `$jp->setArgs()` change les arguments que la méthode
`Article::add()` va recevoir, par ceux retournés par le validateur `SomeValidator::validateArticle()`.

Dans ce contexte :
  * le kind est [Aop::KIND_BEFORE_METHOD](/api/php/class-aop-kindconstantinterface.html#KIND_BEFORE_METHOD)
  * le _JoinPoint_ fournit à l'advice est [\Aop\JoinPoint\BeforeMethodJoinPoint](/api/php/class-aop-joinpoint-beforemethodjoinpoint.html)


## Aop::addAround()

Ajoute l'advice _autour_ de l'exécution d'une action.

Signature de la méthode [Aop::addAround()](/api/php/class-aop-aop.html#_addAround) :

```php
Aop::addAround(
  string $selector,
  callable $callback,

  // Arguments facultatifs
  array $options = [],
  int $kind      = null,
  string $name   = null
);
```

Exemple, ajouter l'advice _autour_ d'une méthode :

```php
Aop::addAround('Article::get()', function($jp) {

  $args = $jp->getArgs();
  $id   = intval($args[0]);

  // si le cache existe
  if(Cache::has('article-'.$id)) {

    // Le cache sera retourné sans exécuter
    // la méthode d'origine "Article::get()"
    $jp->setReturnValue(Cache::get('article-'.$id));

  }else{

    // execute la méthode d'origine "Article::get()"
    $jp->proceed();

    // récupère la valeur de retour de "Article::get()"
    $article = $jp->getReturnValue();

    // ajoute la valeur de retour en cache
    // au prochain appel c'est le cache qui sera retourné
    Cache::add('article-'.$id, $article);
  }
});
```

Dans cet exemple, nous avons ajouté un système de cache sans toucher à la méthode `Article::get()`.
Ainsi le code métier est intact, la méthode `Àrticle::get()` ne s'occuppe que de récupérer un article donné.

Dans ce contexte :
  * le kind est [Aop::KIND_AROUND_METHOD](/api/php/class-aop-kindconstantinterface.html#KIND_AROUND_METHOD)
  * le _JoinPoint_ fournit à l'advice est [\Aop\JoinPoint\AroundMethodJoinPoint](/api/php/class-aop-joinpoint-aroundmethodjoinpoint.html)

Ce qui concerne la stratégie de cache est traité hors du code métier, ce qui rend la méthode `Article::get()` plus simple à maintenir et notre code est plus modulaire car nous avons séparé un aspect technique du code métier.

A partir de là, par exemple il est très simple en environnement de développement, de désactiver le cache et d'ajouter un système de debug, sans toucher au code métier :)


## Aop::addAfterReturn()

Ajoute l'advice _après le retour_ d'une valeur.

Signature de la méthode [Aop::addAfterReturn()](/api/php/class-aop-aop.html#_addAfterReturn) :

```php
Aop::addAfterReturn(
  string $selector,
  callable $callback,

  // Arguments facultatifs
  array $options = [],
  int $kind      = null,
  string $name   = null
);
```

Exemple, ajouter l'advice _après le retour_ de la valeur d'une méthode :

```php
Aop::addAfterReturn('Article::save()', function($jp) {

  $article = $jp->getReturnValue();

  // Met à jour le cache
  Cache::set('article-'.$article->id, $article);
});
```

Dans cet exemple, nous mettons à jour le cache d'un article lorsque celui est modifié dans la base de données.

Dans ce contexte :
  * le kind est [Aop::KIND_AFTER_METHOD_RETURN](/api/php/class-aop-kindconstantinterface.html#KIND_AFTER_METHOD_RETURN)
  * le _JoinPoint_ fournit à l'advice est [\Aop\JoinPoint\AfterMethodReturnJoinPoint](/api/php/class-aop-joinpoint-aftermethodreturnjoinpoint.html)


## Aop::addAfterThrow()

Ajoute l'advice _après la levée d'une exception_.

Signature de la méthode [Aop::addAfterThrow()](/api/php/class-aop-aop.html#_addAfterThrow) :

```php
Aop::addAfterThrow(
  string $selector,
  callable $callback,

  // Arguments facultatifs
  array $options = [],
  int $kind      = null,
  string $name   = null
);
```

Exemple, ajouter l'advice _après une erreur_ sur l'une des méthodes natives de l'extension [PDO](http://php.net/manual/fr/class.pdo.php) incluse dans PHP :

```php
Aop::addAfterThrow('PDO::*()', function($jp) {

  $log->error($jp->getException()->getMessage());
});
```

Dans cet exemple, nous ajoutons un log d'erreur à chaque erreur générée par les méthodes de `PDO`.

Dans ce contexte :
  * le kind est [Aop::KIND_AFTER_METHOD_THROW](/api/php/class-aop-kindconstantinterface.html#KIND_AFTER_METHOD_THROW)
  * le _JoinPoint_ fournit à l'advice est [\Aop\JoinPoint\AfterMethodThrowJoinPoint](/api/php/class-aop-joinpoint-aftermethodthrowjoinpoint.html)


Même chose avec les fonctions PHP natives de l'extension [mysqli](http://php.net/manual/fr/book.mysqli.php) incluse dans PHP :

```php
Aop::addAfterThrow('mysqli_*()', function($jp) {

  $log->error($jp->getException()->getMessage());
});
```

Dans cet exemple, nous ajoutons un log d'erreur à chaque erreur générée par les fonctions `mysqli` de PHP.

Dans ce contexte :
  * le kind est [Aop::KIND_AFTER_FUNCTION_THROW](/api/php/class-aop-kindconstantinterface.html#KIND_AFTER_FUNCTION_THROW)
  * le _JoinPoint_ fournit à l'advice est [\Aop\JoinPoint\AfterFunctionThrowJoinPoint](/api/php/class-aop-joinpoint-afterfunctionthrowjoinpoint.html)


## Aop::addAfter()

Ajoute l'advice _après_ une action.

Cette méthode fournit un `JoinPoint` équivalent `Aop::addAfterReturn()` + `Aop::addAfterThrow()`
réunies en un seul objet.

`Aop::addAfter()` offre donc les mêmes possibilités que `Aop::addAfterReturn()` et `Aop::addAfterThrow()`.

Signature de la méthode [Aop::addAfter()](/api/php/class-aop-aop.html#_addAfter) :

```php
Aop::addAfter(
  string $selector,
  callable $callback,

  // Arguments facultatifs
  array $options = [],
  int $kind      = null,
  string $name   = null
);
```

Exemple, ajouter l'advice _après_ la modification d'une propriété :

```php
Aop::addAfter('User::logged', function($jp) {

  $logged = $jp->getPropertyValue();

  if($logged) {
    $chat->list->add($user);
    $chat->sendMessage($user->username.' a rejoint le salon.');
  }else{
    $chat->list->remove($user);
    $chat->sendMessage($user->username.' a quitté le salon.');
  }
});
```

Dans cet exemple considérons qu'il s'agisse d'un chat de discussion, lorsque la propriété `User::$logged` est modifiée :
  * nous mettons à jour la liste des connectés
  * puis nous envoyons un message à tous les connectés pour signaler que l'utilisateur rentre ou quitte le salon de discussion

Dans ce contexte :
  * le kind est [Aop::KIND_AFTER_PROPERTY_WRITE](/api/php/class-aop-kindconstantinterface.html#KIND_AFTER_PROPERTY_WRITE)
  * le _JoinPoint_ fournit à l'advice est [\Aop\JoinPoint\AfterPropertyWriteJoinPoint](/api/php/class-aop-joinpoint-afterpropertywritejoinpoint.html)

