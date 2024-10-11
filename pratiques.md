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


# Bonne pratique

hormis les bonnes pratiques de syntaxe fondamental de PHP ou les algorithmes trop compliqué ou pas assez atomisés, il y a certaines bonne pratiques qu'il serait intéressant de connaitre.

## Petit rappel des ```case```

| Code | Case appropié |
|------------|------------|
| Les classe | PascalCase |
| Les variables | camelCase |
| Noms de routes | snake_case |
| Les constantes | UPPERCASE |


## Log

Dans le cas où vous aurait besoin de déboguer quelque chose en prod, vous devez garder une trace de l'erreur. Et au lieu de l'afficher au client et de lui demander un screen vous pouvez les mettre dans les logs d'erreur.

Vous avez differents types de log :
```php
$logger->info();
$logger->error();
$logger->debug();
$logger->critical();
```

Une manière de les utiliser si si vous avez une erreur lors de la validation d'un formulaire.

```php
use Psr\Log\LoggerInterface;

...

    public function __construct(
        private LoggerInterface $logger
    ) {}

    public function new(
        Request $request, 
        LoggerInterface $logger
    ): Response
    {
        $task = new Task();
        $form = $this->createForm(TaskType::class, $task);
        $form->handleRequest($request);
        if ($form->isSubmitted() && $form->isValid()) {
            try {

                // Traitement et sauvegarde de donné

                return $this->redirectToRoute('task_success');
            } catch(\Throwablee $err) {
                $this->logger->error(
                    "Erreur lors de la tâche", 
                    ['exception' => $e]
                );
                return $this->redirectToRoute('task_failed');
            }

        }
        
        return $this->render('task/new.html.twig', [  
            'form' => $form,
        ]);
    }

```

Pensez à mettre un maximum de contexte dans le log : route name, id du compte, etc...

[Voir plus](https://symfony.com/doc/current/logging.html#using-a-logger-inside-a-service)

## Cache

Il y a deux types de cache. Celui [côté client](https://symfony.com/doc/current/http_cache.html) et [côté serveur](https://symfony.com/doc/current/cache.html).

Coté serveur il y a deux manière de gérer la duré de vie du cache :

### Cache Serveur

#### Cache par tag

Avec ```TagAwareCacheInterface;``` vous pourrez gérer le cache à partie d'un tag. C'est-à-dire que le cache est lié à un tag qui devras être invalidé dès que sont contenu pourrait être modifié.

Imaginons que vous mettez en cache les données retourné par un "_findAll_" particulièrement lourd. Ces données sont lié à un tag _x_. Dès lors que vous rajoutez/supprimez/modifiez quelque choses de ce repository, dans un crud par exemple, vous devez invalider le tag.

[Voir plus sur le cache par tag](https://symfony.com/doc/current/cache.html#using-cache-tags)

#### Cache par temps

Il y a aussi le cache par temps. Les données retournées sont enregistrer _x_ secondes avec d'être automatiquement invalidé, récupéré et remis en cache.

```php
    // Route de votre controller

    public function cachedAction(
        AdapterInterface $cachePool,
        TrucRepository $trucRepository
    ): Response
    {
        $cachedTrucList = $cachePool->get(
            'my_cache_key', 
            function (ItemInterface $item) use ($trucRepository): string {
                $item->expiresAfter(3600); // Cache expire après 1 heure (3600 secondes)

                $computedValue = $trucRepository->findAll();

                // C'est le contenu de cette variable retourné à 
                // la fonction de callBack qui sera mis en cache
                return $computedValue;
            }
        );

        return $this->render("template.html.twig", [
            "cachedTrucList" => $cachedTrucList
        ]);
    }


```

### Cache Client

Cache temporel demandé dans le head de la réponse.

```php

  // Route de votre controller

    public function cachedAction(
        AdapterInterface $cachePool,
        TrucRepository $trucRepository
    ): Response
    {
        $cachedTrucList = $cachePool->get(
            'my_cache_key', 
            function (ItemInterface $item) use ($trucRepository): string {
                $item->expiresAfter(3600); // Cache expire après 1 heure (3600 secondes)

                $computedValue = $trucRepository->findAll();

                // C'est le contenu de cette variable retourné à 
                // la fonction de callBack qui sera mis en cache
                return $computedValue;
            }
        );

        $response = $this->render("template.html.twig", [
            "cachedTrucList" => $cachedTrucList
        ]);

        $response->setPublic()->setMaxAge(3600);
        $response->headers->addCacheControlDirective('must-revalidate', true);

        return $response;
    }

```

[Voir plus sur le cache par temps](https://symfony.com/doc/current/cache.html)
