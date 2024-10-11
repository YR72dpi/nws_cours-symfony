<details>
    <summary>Table des matières</summary>

- [Introduction](README.md)
- [Structure](structure.md)
- [Getting Started](getting-started.md)
- [Console](console.md)
- [Controller](controller.md)
- [Formulaire](form.md)
- [Doctrine](doctrine.md)
- [Models](models.md)
- [Migration](migration.md)
- [Repositories](repositories.md)
- [Pratiques](pratiques.md)

</details>

# Console 💻

``` bash
php bin/console 
```

## Les commandes "make"

Symfony Maker vous aide à créer des __commandes__ vides, des __contrôleurs__, des classes de __formulaire__, des __tests__ et plus encore, afin que vous puissiez oublier d'écrire du code standard. Ce bundle suppose que vous utilisez une structure de répertoire Symfony 6.4 standard, mais de nombreuses commandes peuvent générer du code dans n'importe quelle application.

``` bash
composer require --dev symfony/maker-bundle
```

Avec le "_--dev_", les commandes du type "_php bin/console make:..._"
ne sont utilisable qu'en dev.

__Exemple :__

La commande ```php bin/console make:migration``` fonctionnera uniquement en dev mais pas en prod.

Son équivalent en pour la prod sera : ```php bin/console doctrine:migration:diff```
