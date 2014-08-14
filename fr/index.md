---
tpl   : default
title : Programmation Orienté Aspect
---

<div class="panel panel-default">
  <div class="panel-body row">
    <div class="col-md-6">
      <img
        class="pull-left marg6"
        src="/assets/img/icon/middleware.png"
        alt="Middleware">
      <h2 class="pull-left">Middleware</h2>
      <div class="clearfix"></div>
        L'Aop permet d'agir avant (before), autour (around)
        et après (after) une portion de code (fonction, méthode ou propriété de classe) en interceptant l'accès à cette portion de code.
        <br><br>
        <span class="fa fa-life-ring"></span> Le type d'interception supporté
        dépend de l'intercepteur utilisé. Certains intercepteurs tels que
        <a href="/fr/php/doc/interceptors/pecl-aop-interceptor" title="PECL AOP interceptor">pecl-aop-interceptor</a> peuvent intercepter les fonctions utilisateurs,
        les fonctions PHP natives, les méthodes de classes (statiques et objets)
        ainsi que les propriétés.
    </div><!-- /.col-md-6 -->
    <div class="col-md-6">
```php
Aop::addAround('Article::add()', function($jp) {

  $jp->setArgs( MyValidator::validateArticle($jp->getArgs()) );

  // execute Article::get()
  $jp->proceed();

  $article          = $jp->getReturnValue();
  $article->content = substr($article->content, 0, 140);

  Mailing::send($article, 'Un nouvel article a été publié.');
});
```
</div></div></div><!-- Fix: indent for markdown parser -->
<div class="panel panel-default">
  <div class="panel-body row">
    <div class="col-md-6">
      <img
        class="pull-left marg6"
        src="/assets/img/icon/intuitive.png"
        alt="API simple et intuitive">
      <h2 class="pull-left">Intuitif</h2>
      <div class="clearfix"></div>
        Des méthodes simples et flexibles pour améliorer la productivité.<br>
        Un code métier facile à maintenir épuré de tous les aspects techniques
        (cache, log, debug, ...).
        <br><br>
        Le raisonnement en programmation orienté objet,
        peut vulgairement se résumer à <b>Je veux</b>.
        <br><br>
        Je veux :
        <ul>
          <li>me concentrer sur le code métier (exemple créer un article, modifier, supprimer)</li>
          <li>intercepter l'appel de cette fonction pour remplacer sa valeur de retour
          selon le contexte</li>
          <li>intercepter et logger les erreurs</li>
            <li>gérer finement le cache de toute mon application</li>
    			<li>changer la valeur de la propriété de cette classe selon le contexte</li>
          <li>ajouter un debug en environnement de développement</li>
          <li>transformer le comportement pour faciliter mes tests unitaires</li>
          <li>...</li>
        </ul>
    </div><!-- /.col-md-6 -->
    <div class="col-md-6">
```php
Aop::addAround('User::login()', function(AroundMethodJoinPoint $jp) {

  $jp->setArgs(['Nico', 'some password']);
  $jp->getArgs(); // [0 => 'Nico', 1 => 'some password']

  // proceed the execution of User::login()
  $jp->proceed();

  $user           = $jp->getReturnValue();
  $user->username = htmlspecialchars($user->username);

  $jp->setReturnValue($user);
});

User::login();
```

```php
Aop::addBefore('Email::send()', $callback);
Aop::addAround('User::save()', $callback);
Aop::addAfter('Article::someProperty', $callback);
Aop::addAfterReturn('Article::get*()', $callback);
Aop::addAfterThrow('*::*', $callback);
```
</div></div></div><!-- Fix: indent for markdown parser -->
<div class="panel panel-default">
  <div class="panel-body row">
    <div class="col-md-6">
      <img
        class="pull-left marg6"
        src="/assets/img/icon/branch.png"
        alt="Intercepter du code avec l'AOP">
      <h2 class="pull-left">Agir sans toucher le code métier</h2>
      <div class="clearfix"></div>
      L'AOP permet d'ajouter une fonctionnalité dans un code métier
      sans y insérer une seule ligne de code à l'intérieur.
      La portion de code est interceptée lors de son exécution (pointcut)
      et vous prenez le contrôle via une fonction de rappel (advice).
      <br><br>
      Exemple d'utilisation, considérons un site ayant :
      <ul>
        <li>son propre système de connexion et de session utilisateur</li>
        <li>et un blog propulsé par WordPress</li>
      </ul>
      Lorsqu'un utilisateur se connecte à son compte via votre blog Wordpress,
      avec l'AOP il est simple de le connecter aux applications tierces utilisées
      sur votre site en interceptant la méthode de connexion
      (ici celle de WordPress pour l'exemple).
      <br><br>
      Inversement si l'utilisateur se connecte via votre site,
      vous pouvez le connecter à WordPress et aux autres applications utilisées
      sur votre site (exemple un forum phpBB). Idem pour la déconnection, etc
      <br><br>
      On peut intercepter le code avant (before) son exécution, après (after) et autour (around).
      <br>
      Dans cet exemple nous interceptons la fonction de connexion de WordPress `wp_signon()`
      (http://codex.wordpress.org/Function_Reference/wp_signon).
      <br>
      L'interception est de type "around" (autour) pour
      avoir accès aux arguments et traiter soit même l'exécution de la fonction.
    </div>
    <div class="col-md-6">
```php
// Intercepte la fonction de connection de WordPress.
Aop::addAround('wp_signon()', function($jp) {

  // tous les arguments passés à la fonction
  // wp_signon() de WordPress
  $args = $jp->getArgs();

  // l'argument $credentials de WordPress
  // voir http://codex.wordpress.org/Function_Reference/wp_signon
  $credentials = $args[0];

  // procèder à l'execution normale
  // de "wp_signon()" (la fonction interceptée)
  $jp->proceed()

  // récupérer sa valeur de retour
  $wpUser = $jp->getReturnValue();

  // si l'utilisateur est identifié à Wordpress
  if( !is_wp_error($wpUser) ) {

    // connecter l'utilisateur
    // à votre propre gestionnaire d'utilisateur
    // exemple
    $user->login(
      $credentials['user_login'],
      $credentials['user_password']
    );
  }
});
```
</div></div></div><!-- Fix: indent for markdown parser -->