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

Pour faire un formulaire, vous avez la commande ```php bin/console make:form```. Vous choisissez son nom et s'il faut la lié à une entité ou pas. Si lié, vous retrouverz les attributs de votre entité dans le form.

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

Si par exemple vous avez besoins de savoir si le formulaire traite une entité vide (comme lors d'un ajout), vous pouvez créer un fonction "_isNew_" dans l'entité comme ceci 

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

## Champ de formulaire qui n'est pas dans l'entité

Imaginons que vous avez besoins de sauvegarder un fichier. Vous avec un champs ```fileName``` dans votre entité qui est un _string_.

Dans le _formType.php_, ce que vous pouvez faire c'est :
1. commentez le ```->add("fileName")``` (on s'en occupera plus tard).

2. Créer un champ de fichier avec ```->add("realFileInput", FileType::class)``` .

3. Lors de la validation du formulaire, gérer le fichier puis enregistrez le nom du fichier avec ```->setFileName($nomDuFichier)``` en le formatant comme vous voulez, comme par exemple avec le __SluggerInterface__ qui vous permettera de formater le nom en _camelCase_.

Au point trois il risque d'il y avoir une erreur car "_realFileInput_" n'éxiste pas dans l'entité. Pour passer cette erreur vous devez ajouter la propriété suivante :

```php 
use Symfony\Component\Form\Extension\Core\Type\FileType;

...

->add("realFileInput", FileType::class, [
    "mapped" => false
])
```

[Voir la doc](https://symfony.com/doc/current/reference/forms/types/file.html)