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

# Structure

La structure d'un projet Symfony est bien organisée pour faciliter le développement d'applications web robustes et maintenables. Voici un aperçu général de cette structure :

## 1. Dossier src/

Ce dossier contient le code principal de l'application, y compris les contrôleurs, les entités, les formulaires, les services, etc.

- Controller/ : Contient les classes de contrôleurs qui gèrent les requêtes HTTP, les manipulent et retournent une réponse. Chaque contrôleur représente généralement une action spécifique (par exemple, afficher une page ou traiter un formulaire).

- Entity/ : Contient les entités représentant les objets métiers et leur correspondance avec les tables de la base de données via Doctrine ORM.

- Repository/ : Contient les classes qui implémentent la logique de recherche pour les entités. Doctrine Repository est utilisé pour interagir avec la base de données.

- Form/ : Contient les classes qui gèrent les formulaires, définissant les champs et les règles de validation.

- Service/ : Contient les services réutilisables dans l'application.

## 2. Dossier config/

Ce dossier contient tous les fichiers de configuration de l'application :

- packages/ : Contient des fichiers de configuration pour les bundles et services (Doctrine, Twig, Security, etc.).
    
- routes/ : Contient la définition des routes de l'application.

- services.yaml : Définit la configuration des services de l'application (injection de dépendances, autowiring, etc.).

## 3. Dossier templates/

Contient les fichiers de templates Twig. Ces fichiers définissent le rendu HTML des pages générées par l'application. Vous trouverez des fichiers comme base.html.twig qui définissent la structure globale des pages.

## 4. Dossier public/

Le seul dossier accessible directement par le navigateur. Il contient :

- index.php : Le point d'entrée principal de l'application. C'est ici que les requêtes sont redirigées pour être traitées par Symfony.
    
- Les ressources publiques comme des fichiers CSS, JavaScript et images.

## 5. Dossier var/

Contient les fichiers temporaires générés par l'application :

- cache/ : Les fichiers de cache de l'application pour améliorer la performance.

- log/ : Les logs d'exécution de l'application.

## 6. Dossier vendor/

Ce dossier est géré par Composer et contient toutes les dépendances et bibliothèques externes utilisées par Symfony, telles que les bundles, les composants Symfony, etc.

## 7. Dossier bin/

Contient les scripts exécutables, comme console, qui est l'interface en ligne de commande de Symfony pour gérer les tâches du framework (génération d'entités, migration, etc.).

## 8. Dossier tests/

Contient les tests unitaires, fonctionnels ou d'intégration de votre application. Symfony encourage les bonnes pratiques de tests, et ce dossier est destiné à contenir les classes de tests.

## 9. Fichier .env

Contient les variables d'environnement, comme les informations de connexion à la base de données ou des paramètres spécifiques à chaque environnement (dev, prod, test).

## 10. Fichier composer.json

Ce fichier définit les dépendances du projet et est utilisé par Composer pour gérer les paquets. Il contient également des informations sur la configuration autoload.