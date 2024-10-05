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

# Migration

Une migration dans Symphony est le fait de dire à doctrine d'interpréter les entités puis de créer une table par entité avec toutes les propriétés qu'il y a dans celle-ci.

Chaque variable présent dans une entité sera donc une colonne dans votre table. Si la variable est typée comme étant en entier alors il y aura un entier dans la colonne qui est destiné. Pareillement pour les strings ou chaîne de caractère, les dates les boulets et cetera.

Pour faire une relation, le type de la variable sera la classe de l'entié liées. La valeur présente alors dans la colonne sera l'id de l'entité liées.

## Faire une migration

### Methode bourrin

La première méthode ne doit être utilisée qu'en dev et pour des changement simple.
```bash
php bin/console doctrine:schema:update --force
```

Cette commande est à utiliser pour des changements simples ou rapides dans une base de données locale, comme pendant le développement.

Elle met à jour le schéma de la base de données directement en fonction de vos entités. Par exemple, si vous ajoutez un champ à une entité, cette commande va créer la colonne correspondante dans la table.

Le problème est qu'elle ne gère pas bien les changements complexes. De plus, elle ne conserve pas d'historique des modifications de schéma, donc difficile à utiliser en production si vous voulez faire un retour à l'ancien schema.

### Method Gentleman

Recommandé pour tout changement structurel sur la base de données, en particulier si vous travaillez en équipe ou si vous avez plusieurs environnements (développement, test, production).

Cette methode vous informera aussi s'il y a des problèmes au niveau du mapping et des liaisons entre entité.

__1er étape :__
```bash
# Si vous avez le maker-bundle, en dev
php bin/console make:migration

# Sinon, avec la commande de doctrine
php bin/console doctrine:migration:diff
```
Crée un fichier de migration qui décrit les changements à appliquer à la base de données (ajout, suppression de colonnes, modification d'index, etc.).

__2ème étape :__

```bash
php bin/console doctrine:migration:migrate
```

Applique les migrations enregistrées dans votre base de données, garantissant une traçabilité et une reproductibilité des changements.