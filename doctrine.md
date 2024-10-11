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

# Doctrine 🗺 

Doctrine est un outil de gestion de base de données utilisé dans Symfony. Plus précisément, c'est un ORM (Object-Relational Mapping), ce qui signifie qu'il permet de lier les objets de ton code PHP aux tables de ta base de données de manière automatique.

Voici une explication simple du fonctionnement de Doctrine dans Symfony :

1. __Entités__ : Dans ton code, tu crées des entités, qui sont des classes PHP représentant des tables dans la base de données. Par exemple, si tu as une table "User" dans ta base de données, tu auras une classe "User" dans ton code.

2. __Mappage__ : Doctrine fait le lien entre tes entités (tes classes PHP) et les tables dans la base de données. Cela signifie que chaque propriété de ton entité (comme name, email, etc.) correspond à une colonne dans une table.

3. __Requêtes simplifiées__ : Au lieu d'écrire des requêtes SQL manuellement, tu utilises Doctrine pour interagir avec la base de données via des objets PHP. Doctrine s'occupe de traduire ces actions en SQL. Par exemple, pour récupérer tous les utilisateurs, tu n'as pas besoin d'écrire "SELECT * FROM users", tu fais simplement $userRepository->findAll().

4. __Gestion des relations__ : Doctrine gère aussi les relations entre les entités (par exemple, un utilisateur peut avoir plusieurs commandes). Ces relations peuvent être définies facilement dans les entités avec des annotations.

Doctrine te permet de travailler avec la base de données en utilisant des objets PHP, ce qui rend le code plus propre et plus facile à maintenir.
