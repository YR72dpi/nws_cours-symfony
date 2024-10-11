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

# Les formulaire


## Création de formulaires

```php
// src/Form/CategoryType.php
namespace App\Form;

use App\Entity\Category;
use Symfony\Component\Form\AbstractType;
use Symfony\Component\Form\FormBuilderInterface;
use Symfony\Component\OptionsResolver\OptionsResolver;

class CategoryType extends AbstractType
{
    public function buildForm(FormBuilderInterface $builder, array $options): void
    {
        $builder->add('name');
    }

    public function configureOptions(OptionsResolver $resolver): void
    {
        $resolver->setDefaults([
            'data_class' => Category::class,
        ]);
    }
}
```

Normalement, symfony s'occupe de tout, mais il y a certaines choses à savoir. 

Si par exemple vous avez besoins de savoir si le formulaire traite d'une entité vide (comme lors d'un ajout), vous pouvez créer un fonction "_isNew_" dans l'entité comme ceci 

```php
public function isNew() : bool { return $this->getid() === null; }
```

Puis le récuperer comme ceci :

```php
public function buildForm(FormBuilderInterface $builder, array $options): void
    {
        $theEntity = $options["data"]
        $builder->add('name', options: [
            "required" => $theEntity->isNew()
        ]);
    }
```

## Les types

Il y a de nombreux types pour les champs d'un formulaire.
[Les voici](https://symfony.com/doc/current/reference/forms/types.html)

Les types hérites tous d'un parent commun, "_FormType_", ce qui implique qu'ils y ont des options, des fonctionnements, en commun aussi. Mais chaque type ont leurs options propres.