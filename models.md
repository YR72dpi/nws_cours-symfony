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

# Models

Dans le framework Symfony, les _models_ sont appelé _Entity_ et se trouve dans ```./src/Entity/```. Les entity se nomment par leur sujet. Exemple : "_Article.php_"

Pour en créer une _Entity_ :
```bash
php bin/console make:entity
```

```php
namespace App\Entity;

use App\Repository\ConferenceRepository;
use Doctrine\ORM\Mapping as ORM;

#[ORM\Entity(repositoryClass: ConferenceRepository::class)]
class Conference
{
    #[ORM\Column(type: 'integer')]
    #[ORM\Id, ORM\GeneratedValue()]
    private $id;

    #[ORM\Column(type: 'string', length: 255)]
    private $city;

    // ...

    public function getCity(): ?string
    {
        return $this->city;
    }

    public function setCity(string $city): self
    {
        $this->city = $city;

        return $this;
    }

    // ...
}
```

Suivez ensuite les instructions en focntion de ce que vous voulez créer.

[Voir +](https://symfony.com/doc/current/the-fast-track/en/8-doctrine.html#creating-entity-classes)