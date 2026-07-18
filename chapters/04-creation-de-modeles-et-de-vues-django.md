## Création de modèles de données
Les modèles de données sont des représentations de vos données dans la base de données. Ils sont utilisés pour interagir avec la base de données et pour valider les données. Dans Django, les modèles sont définis dans le fichier `models.py` de votre application.

### Définition d'un modèle
Un modèle est défini en utilisant la classe `Model` de Django. Vous devez définir les champs de votre modèle en utilisant les classes de champs de Django, telles que `CharField`, `IntegerField`, `DateTimeField`, etc.

```python
from django.db import models

class Livre(models.Model):
    titre = models.CharField(max_length=200)
    auteur = models.CharField(max_length=100)
    date_parution = models.DateField()
```

Dans cet exemple, nous définissons un modèle `Livre` avec trois champs : `titre`, `auteur` et `date_parution`.

### Types de champs
Django propose plusieurs types de champs pour vos modèles. Voici quelques-uns des types de champs les plus couramment utilisés :

* `CharField` : un champ de caractères avec une longueur maximale
* `IntegerField` : un champ entier
* `DateTimeField` : un champ de date et d'heure
* `BooleanField` : un champ booléen
* `ForeignKey` : un champ qui fait référence à un autre modèle

```python
from django.db import models

class Auteur(models.Model):
    nom = models.CharField(max_length=100)
    prenom = models.CharField(max_length=100)

class Livre(models.Model):
    titre = models.CharField(max_length=200)
    auteur = models.ForeignKey(Auteur, on_delete=models.CASCADE)
```

Dans cet exemple, nous définissons un modèle `Auteur` et un modèle `Livre` avec un champ `auteur` qui fait référence au modèle `Auteur`.

## Création de vues
Les vues sont des fonctions qui gèrent les requêtes HTTP et renvoient des réponses HTTP. Dans Django, les vues sont définies dans le fichier `views.py` de votre application.

### Définition d'une vue
Une vue est définie en utilisant la fonction `view` de Django. Vous devez définir la logique de votre vue dans cette fonction.

```python
from django.shortcuts import render
from .models import Livre

def liste_livres(request):
    livres = Livre.objects.all()
    return render(request, 'liste_livres.html', {'livres': livres})
```

Dans cet exemple, nous définissons une vue `liste_livres` qui renvoie une liste de tous les livres dans la base de données.

### Types de vues
Django propose plusieurs types de vues pour gérer les requêtes HTTP. Voici quelques-uns des types de vues les plus couramment utilisés :

* `View` : une vue qui gère les requêtes HTTP et renvoie des réponses HTTP
* `TemplateView` : une vue qui renvoie un template HTML
* `ListView` : une vue qui renvoie une liste d'objets
* `DetailView` : une vue qui renvoie un objet unique

```python
from django.views.generic import ListView
from .models import Livre

class ListeLivreView(ListView):
    model = Livre
    template_name = 'liste_livres.html'
```

Dans cet exemple, nous définissons une vue `ListeLivreView` qui renvoie une liste de tous les livres dans la base de données.

## Interaction avec la base de données
Django propose une API pour interagir avec la base de données. Vous pouvez utiliser cette API pour créer, lire, mettre à jour et supprimer des objets dans la base de données.

### Création d'objets
Vous pouvez créer des objets dans la base de données en utilisant la méthode `create` de Django.

```python
from .models import Livre

livre = Livre(titre='Le Petit Prince', auteur='Antoine de Saint-Exupéry')
livre.save()
```

Dans cet exemple, nous créons un objet `Livre` et le sauvegardons dans la base de données.

### Lecture d'objets
Vous pouvez lire des objets dans la base de données en utilisant la méthode `get` de Django.

```python
from .models import Livre

livre = Livre.objects.get(titre='Le Petit Prince')
```

Dans cet exemple, nous lisons un objet `Livre` avec le titre 'Le Petit Prince' dans la base de données.

### Mise à jour d'objets
Vous pouvez mettre à jour des objets dans la base de données en utilisant la méthode `save` de Django.

```python
from .models import Livre

livre = Livre.objects.get(titre='Le Petit Prince')
livre.titre = 'Le Nouveau Titre'
livre.save()
```

Dans cet exemple, nous mettons à jour un objet `Livre` avec le titre 'Le Petit Prince' dans la base de données.

### Suppression d'objets
Vous pouvez supprimer des objets dans la base de données en utilisant la méthode `delete` de Django.

```python
from .models import Livre

livre = Livre.objects.get(titre='Le Petit Prince')
livre.delete()
```

Dans cet exemple, nous supprimons un objet `Livre` avec le titre 'Le Petit Prince' dans la base de données.

## Points clés
* Les modèles de données sont des représentations de vos données dans la base de données.
* Les vues sont des fonctions qui gèrent les requêtes HTTP et renvoient des réponses HTTP.
* Django propose une API pour interagir avec la base de données.
* Vous pouvez créer, lire, mettre à jour et supprimer des objets dans la base de données en utilisant les méthodes de Django.
* Les types de champs les plus couramment utilisés sont `CharField`, `IntegerField`, `DateTimeField`, `BooleanField` et `ForeignKey`.
* Les types de vues les plus couramment utilisés sont `View`, `TemplateView`, `ListView` et `DetailView`.