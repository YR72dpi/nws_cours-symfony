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