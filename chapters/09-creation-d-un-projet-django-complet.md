## Création d'un projet Django complet
La création d'un projet Django complet nécessite la mise en pratique de tous les concepts appris dans les chapitres précédents. Dans ce chapitre, nous allons créer une application web complète qui inclut des modèles, des vues, des templates, des formulaires et une authentification.

### Définition du projet
Notre projet s'appellera "E-commerce" et consiste en une plateforme de vente en ligne de produits. Nous allons créer une application web qui permet aux utilisateurs de se connecter, de consulter les produits, de les ajouter au panier et de passer commande.

### Création du projet Django
Pour créer le projet Django, nous allons utiliser la commande `django-admin startproject` suivie du nom du projet :
```bash
django-admin startproject e-commerce
```
Cela va créer un nouveau répertoire `e-commerce` contenant les fichiers et les dossiers nécessaires pour le projet.

### Création de l'application
Dans le projet `e-commerce`, nous allons créer une nouvelle application appelée `produits` :
```bash
python manage.py startapp produits
```
Cela va créer un nouveau répertoire `produits` contenant les fichiers et les dossiers nécessaires pour l'application.

### Définition des modèles
Les modèles sont des représentations de données dans la base de données. Dans notre cas, nous allons créer deux modèles : `Produit` et `Commande`. Le modèle `Produit` aura les champs suivants :
* `nom`
* `description`
* `prix`
* `quantite`

Le modèle `Commande` aura les champs suivants :
* `date`
* `total`
* `produits` (une liste de produits)

Voici le code pour les modèles :
```python
# models.py
from django.db import models

class Produit(models.Model):
    nom = models.CharField(max_length=255)
    description = models.TextField()
    prix = models.DecimalField(max_digits=10, decimal_places=2)
    quantite = models.IntegerField()

class Commande(models.Model):
    date = models.DateTimeField(auto_now_add=True)
    total = models.DecimalField(max_digits=10, decimal_places=2)
    produits = models.ManyToManyField(Produit)
```
### Création des vues
Les vues sont des fonctions qui traitent les requêtes HTTP et renvoient des réponses. Nous allons créer les vues suivantes :
* `liste_produits` : affiche la liste des produits
* `details_produit` : affiche les détails d'un produit
* `commande` : permet de passer commande

Voici le code pour les vues :
```python
# views.py
from django.shortcuts import render, redirect
from .models import Produit, Commande
from .forms import CommandeForm

def liste_produits(request):
    produits = Produit.objects.all()
    return render(request, 'produits/liste.html', {'produits': produits})

def details_produit(request, pk):
    produit = Produit.objects.get(pk=pk)
    return render(request, 'produits/details.html', {'produit': produit})

def commande(request):
    if request.method == 'POST':
        form = CommandeForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('liste_produits')
    else:
        form = CommandeForm()
    return render(request, 'produits/commande.html', {'form': form})
```
### Création des templates
Les templates sont des fichiers HTML qui affichent les données. Nous allons créer les templates suivants :
* `liste.html` : affiche la liste des produits
* `details.html` : affiche les détails d'un produit
* `commande.html` : permet de passer commande

Voici le code pour les templates :
```html
<!-- liste.html -->
{% extends 'base.html' %}

{% block content %}
  <h1> Liste des produits </h1>
  <ul>
    {% for produit in produits %}
      <li>
        {{ produit.nom }} ({{ produit.prix }})
      </li>
    {% endfor %}
  </ul>
{% endblock %}
```

```html
<!-- details.html -->
{% extends 'base.html' %}

{% block content %}
  <h1> Détails du produit </h1>
  <p> Nom : {{ produit.nom }} </p>
  <p> Description : {{ produit.description }} </p>
  <p> Prix : {{ produit.prix }} </p>
{% endblock %}
```

```html
<!-- commande.html -->
{% extends 'base.html' %}

{% block content %}
  <h1> Passer commande </h1>
  <form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit"> Commander </button>
  </form>
{% endblock %}
```
### Création des formulaires
Les formulaires permettent aux utilisateurs de saisir des données. Nous allons créer un formulaire pour la commande :
```python
# forms.py
from django import forms
from .models import Commande

class CommandeForm(forms.ModelForm):
    class Meta:
        model = Commande
        fields = ('date', 'total', 'produits')
```
### Authentification
L'authentification permet aux utilisateurs de se connecter et de se déconnecter. Nous allons utiliser les vues et les templates de Django pour l'authentification :
```python
# views.py
from django.contrib.auth import login, logout, authenticate
from django.contrib.auth.forms import AuthenticationForm

def connexion(request):
    if request.method == 'POST':
        form = AuthenticationForm(request, request.POST)
        if form.is_valid():
            username = form.cleaned_data.get('username')
            password = form.cleaned_data.get('password')
            user = authenticate(username=username, password=password)
            if user is not None:
                login(request, user)
                return redirect('liste_produits')
    else:
        form = AuthenticationForm()
    return render(request, 'connexion.html', {'form': form})

def deconnexion(request):
    logout(request)
    return redirect('liste_produits')
```
### URLs
Les URLs permettent de mapper les vues aux adresses web. Nous allons créer les URLs suivantes :
```python
# urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('produits/', views.liste_produits, name='liste_produits'),
    path('produits/<pk>/', views.details_produit, name='details_produit'),
    path('commande/', views.commande, name='commande'),
    path('connexion/', views.connexion, name='connexion'),
    path('deconnexion/', views.deconnexion, name='deconnexion'),
]
```
## Points cles
* La création d'un projet Django complet nécessite la mise en pratique de tous les concepts appris dans les chapitres précédents.
* Les modèles représentent les données dans la base de données.
* Les vues traitent les requêtes HTTP et renvoient des réponses.
* Les templates affichent les données.
* Les formulaires permettent aux utilisateurs de saisir des données.
* L'authentification permet aux utilisateurs de se connecter et de se déconnecter.
* Les URLs permettent de mapper les vues aux adresses web.