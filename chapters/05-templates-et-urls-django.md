## Templates Django
Les templates sont des fichiers qui contiennent le code HTML et les balises de template qui permettent d'afficher des données dynamiques. Dans Django, les templates sont utilisés pour séparer la logique de présentation de la logique de l'application. Cela signifie que vous pouvez modifier l'apparence de votre application sans toucher au code Python.

### Création d'un template
Pour créer un template, vous devez créer un fichier HTML dans le répertoire `templates` de votre projet Django. Par exemple, si vous avez un projet nommé `mon_projet`, vous pouvez créer un répertoire `templates` dans le répertoire `mon_projet` et ajouter un fichier `index.html` à l'intérieur.

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
<head>
    <title>Page d'accueil</title>
</head>
<body>
    <h1>Bienvenue sur mon site web</h1>
</body>
</html>
```

### Utilisation des balises de template
Les balises de template sont utilisées pour afficher des données dynamiques dans votre template. Il existe plusieurs types de balises de template, notamment :

*   `{{ }}` : utilisé pour afficher des variables
*   `{% %}` : utilisé pour les instructions de contrôle (par exemple, des boucles ou des conditions)
*   `{# #}` : utilisé pour les commentaires

Par exemple, si vous avez une vue qui passe une variable `nom` à votre template, vous pouvez l'afficher comme suit :

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
<head>
    <title>Page d'accueil</title>
</head>
<body>
    <h1>Bonjour, {{ nom }} !</h1>
</body>
</html>
```

## URLs Django
Les URLs (Uniform Resource Locators) sont utilisées pour accéder aux différentes pages de votre application web. Dans Django, les URLs sont définies dans un fichier `urls.py` qui se trouve dans le répertoire de votre projet.

### Création d'une URL
Pour créer une URL, vous devez ajouter une ligne de code dans le fichier `urls.py` de votre projet. Par exemple, si vous avez une vue nommée `index` qui affiche la page d'accueil de votre site web, vous pouvez créer une URL comme suit :

```python
# urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

Dans cet exemple, la URL `/` (la racine du site web) est associée à la vue `index`. La fonction `path` prend trois arguments : la première est la chaîne de caractères qui correspond à la URL, la deuxième est la vue qui sera appelée lorsque la URL est accédée, et la troisième est le nom de la URL.

### Utilisation des paramètres dans les URLs
Vous pouvez également utiliser des paramètres dans les URLs pour transmettre des informations à vos vues. Par exemple, si vous avez une vue qui affiche les détails d'un produit, vous pouvez créer une URL comme suit :

```python
# urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('produits/<int:id>/', views.produit, name='produit'),
]
```

Dans cet exemple, la URL `/produits/123/` (où `123` est l'ID du produit) est associée à la vue `produit`. La fonction `path` utilise le motif `<int:id>` pour capturer l'ID du produit et le transmettre à la vue `produit`.

## Exemple concret
Supposons que vous êtes un développeur web qui crée un site web pour une entreprise de vente en ligne de produits locaux. Vous voulez créer une page qui affiche les détails d'un produit, y compris son nom, sa description et son prix.

Voici un exemple de code qui montre comment vous pouvez utiliser les templates et les URLs pour afficher les détails d'un produit :

```python
# models.py
from django.db import models

class Produit(models.Model):
    nom = models.CharField(max_length=255)
    description = models.TextField()
    prix = models.DecimalField(max_digits=10, decimal_places=2)

# views.py
from django.shortcuts import render
from .models import Produit

def produit(request, id):
    produit = Produit.objects.get(id=id)
    return render(request, 'produit.html', {'produit': produit})

# urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('produits/<int:id>/', views.produit, name='produit'),
]

# produit.html
<!DOCTYPE html>
<html>
<head>
    <title>Détails du produit</title>
</head>
<body>
    <h1>{{ produit.nom }}</h1>
    <p>{{ produit.description }}</p>
    <p>Prix : {{ produit.prix }} €</p>
</body>
</html>
```

Dans cet exemple, la vue `produit` récupère le produit à partir de la base de données en fonction de son ID, puis transmet le produit à la template `produit.html` pour afficher les détails du produit.

## Points clés
*   Les templates Django sont utilisés pour afficher des pages web dynamiques.
*   Les balises de template sont utilisées pour afficher des données dynamiques dans les templates.
*   Les URLs Django sont utilisées pour accéder aux différentes pages de l'application web.
*   Les paramètres peuvent être utilisés dans les URLs pour transmettre des informations aux vues.
*   Les templates et les URLs peuvent être utilisés ensemble pour créer des applications web dynamiques et interactives.