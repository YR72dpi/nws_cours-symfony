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

# Controller ⚙

## La base

```php
// src/Controller/LuckyController.php
namespace App\Controller;

use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Attribute\Route;

class LuckyController
{
    #[Route('/lucky/number/{max}', name: 'app_lucky_number')]
    public function number(int $max): Response
    {
        $number = random_int(0, $max);

        return new Response(
            '<html><body>Lucky number: '.$number.'</body></html>'
        );
    }
}
```

La ligne ```#[Route('/lucky/number/{max}', name: 'app_lucky_number')]``` est un _attribut_.
- ```app_lucky_number``` et le nom de la route
    - Doit etre __unique__
    - Ecrit en __snake_case__
- ```{max}``` sert à dire qu'il y a un paramêtre d'url attendu comme ceci : ```/lucky/number/18```
- ```int $max``` sert à récuperer la valeur dans la fonction, "_int_" pour dire que ca doit être un entier
- ``` return new Response(...);``` sert à renvoyer une réponse
    - Il y a différentes manières pour renvoyer une réponse [Voir +](https://symfony.com/doc/current/components/http_foundation.html#response)

## Assigner une url à un Controller


```php
// src/Controller/LuckyController.php
namespace App\Controller;

use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Attribute\Route;

#[Route('/article', name: 'app_article_')]
class LuckyController
{
    #[Route('/voir', name: 'voir')]
    public function number(): Response {}

    #[Route('/ajouter', name: 'ajouter')]
    public function number(): Response {}

    #[Route('/modifier/{id}', name: 'modifier')]
    public function number(int $max): Response {}

    #[Route('/supprimer/{id}', name: 'supprimer')]
    public function number(int $max): Response {}
}
```

Ce qui donne : 

| Route | Url |
|--|--|
| app_article_voir | /article/voir |
| app_article_ajouter | /article/ajouter |
| app_article_modifier | /article/modifier |
| app_article_supprimer | /article/supprimer |
