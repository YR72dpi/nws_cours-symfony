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

# Repositories

En Symfony, les repositories sont des classes utilisées pour interagir avec la base de données. Elles contiennent des méthodes qui permettent d'effectuer des requêtes SQL (via Doctrine ORM ou DBAL). Par défaut, chaque entité dans Symfony a son propre repository, qui hérite des fonctionnalités fournies par le `EntityRepository` de Doctrine.

## Méthodes

Dans un repository il y a, à disposition plusieurs, méthodes prédéfinies. Voici quelques-unes des plus courantes :

- **`find($id)`** : Retourne l'entité avec l'ID spécifié ou `null` si elle n'existe pas.
- **`findAll()`** : Retourne toutes les entités de ce type.
- **`findBy(array $criteria, array $orderBy = null, $limit = null, $offset = null)`** : Retourne un tableau d'entités correspondant à un ensemble de critères (par exemple, trouver tous les utilisateurs avec un rôle spécifique).
- **`findOneBy(array $criteria)`** : Retourne une seule entité correspondant aux critères donnés ou `null` si aucune entité ne correspond.
- **`getClassName()`** : Retourne le nom de la classe associée au repository.

## Utilisation des Repositories

Pour utiliser un repository dans un contrôleur ou un service, il suffit d'injecter l'entité correspondante dans le constructeur ou de la récupérer via le gestionnaire d'entités (`EntityManager`).

Exemple dans un contrôleur :

```php
use App\Repository\UserRepository;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;

class UserController extends AbstractController
{
    public function listArticle(
        ArticleRepository $articleRepository
    )
    {
        $articleList = $articleRepository->findAll();

        return $this->render('article/list.html.twig', [
            'articleList' => $articleList,
        ]);
    }
}
```

## Méthodes personnalisées

Vous pouvez également ajouter des méthodes spécifiques à vos besoins dans un repository.

Par exemple, pour trouver tous les utilisateurs actifs :

```php
class ArticleRepository extends ServiceEntityRepository
{
    public function findActiveArticles()
    {
        return $this->createQueryBuilder('a')
            ->andWhere('a.active = :active')
            ->setParameter('active', true)
            ->getQuery()
            ->getResult();
    }
}
```
