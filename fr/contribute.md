---
tpl   : doc
title : Contribuer
---

## Documentation

Si vous le souhaitez, vous avez la possibilité de participer à la documentation de l'AOP.

Il existe plusieurs manières de contribuer à la documentation, soit directement en éditant les fichiers sur [Github](https://github.com/aop-io/doc), soit de manière plus traditionnelle, [en faisant un fork du projet](https://github.com/aop-io/doc/fork) puis un pull request.

Pour traduire la documentation dans une nouvelle langue, créez un dossier correspondant à la nouvelle langue et conservez le même nommage de fichiers que la doc _fr_ (la doc la plus à jour).

Les noms de fichiers doivent être en anglais.

Exemple pour l'espagnol : `/doc/es`

Les commits doivent être en anglais aussi pour faciliter le maintien de l'ensemble de la doc.

Exemples de commits :

```sh
git commit interception.md -m "[fr] Fix typo in interception.md"
```

```sh
git commit interception.md -m "[es] Translate interceptor.md"
```

```sh
git commit interception.md -m "[en] Translate contribute.md#documentation"
```


## Intercepteur

Voir [créer un intercepteur](/fr/php/doc/interceptors/#cr-er-un-intercepteur).