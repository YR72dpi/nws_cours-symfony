<details>
    <summary>Table des matières</summary>

- [Introduction](README.md)
- [Structure](structure.md)
- [Getting Started](getting-started.md)
- [Console](console.md)
- [Controller](controller.md)
- [Doctrine](doctrine.md)
- [Models](models.md)
- [Migration](migration.md)
- [Repositories](repositories.md)
- [Pratiques](pratiques.md)

</details>

# Let's go ! 🏁

## Prérequis

A avoir d'installer :
1. __XAMP__ / __LAMP__ / __WAMP__
2. __Composer__

## Initialiser un projet Symfony

```
# Cette commande uniquement créera le minimum de Symfony pour faire une API
# Il créer le projet dans un dossier appelé "le_nom_de_ton_projet"
composer create-project symfony/skeleton:"7.1.*" le_nom_de_ton_projet

# change directory
cd le_nom_de_ton_projet

# Créer une surcouche pour ajouter le "front" 
composer require webapp
```