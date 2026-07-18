## Introduction aux formulaires Django
Les formulaires sont un élément essentiel dans les applications web, car ils permettent aux utilisateurs d'interagir avec l'application et de fournir des données. Dans Django, les formulaires sont créés à l'aide de la classe `Form` du module `django.forms`. Cette classe fournit une manière simple et sécurisée de valider les données fournies par les utilisateurs.

### Création d'un formulaire
Pour créer un formulaire, il faut importer la classe `Form` et créer une nouvelle classe qui hérite de `Form`. Les champs du formulaire sont définis en tant qu'attributs de la classe. Par exemple, si nous voulons créer un formulaire pour recueillir les informations de contact d'un utilisateur, nous pouvons créer un formulaire comme suit :
```python
from django import forms

class ContactForm(forms.Form):
    nom = forms.CharField(label='Nom', max_length=100)
    email = forms.EmailField(label='Email', max_length=100)
    message = forms.CharField(label='Message', widget=forms.Textarea)
```
Dans cet exemple, nous avons créé un formulaire `ContactForm` avec trois champs : `nom`, `email` et `message`. Le champ `nom` est un champ de texte avec une longueur maximale de 100 caractères, le champ `email` est un champ de type email et le champ `message` est un champ de texte multiligne.

### Validation des données
L'une des fonctionnalités les plus importantes des formulaires Django est la validation des données. Lorsqu'un utilisateur soumet un formulaire, Django vérifie automatiquement les données fournies pour s'assurer qu'elles sont valides. Par exemple, si un utilisateur entre une adresse email incorrecte, Django affichera un message d'erreur pour indiquer que l'adresse email est invalide.

Pour valider les données, nous devons appeler la méthode `is_valid()` du formulaire. Si les données sont valides, cette méthode renvoie `True`, sinon elle renvoie `False`. Nous pouvons également utiliser la méthode `clean()` pour nettoyer les données et les rendre sécurisées pour utilisation.

### Affichage d'un formulaire
Pour afficher un formulaire, nous devons créer une vue qui instancie le formulaire et le rend dans un template. Par exemple, si nous voulons afficher le formulaire `ContactForm` dans une page web, nous pouvons créer une vue comme suit :
```python
from django.shortcuts import render
from .forms import ContactForm

def contact(request):
    if request.method == 'POST':
        form = ContactForm(request.POST)
        if form.is_valid():
            # Traitement des données
            return render(request, 'contact/success.html')
    else:
        form = ContactForm()
    return render(request, 'contact/form.html', {'form': form})
```
Dans cet exemple, nous avons créé une vue `contact` qui instancie le formulaire `ContactForm` et le rend dans un template `form.html`. Si le formulaire est soumis, nous vérifions si les données sont valides et traitons les données si elles le sont.

## Authentification Django
L'authentification est un élément essentiel dans les applications web, car elle permet de vérifier l'identité des utilisateurs et de gérer leurs comptes. Dans Django, l'authentification est gérée par le module `django.contrib.auth`.

### Création d'un utilisateur
Pour créer un utilisateur, nous devons importer la classe `User` du module `django.contrib.auth.models` et créer un nouvel objet `User`. Par exemple :
```python
from django.contrib.auth.models import User

user = User.objects.create_user('username', 'email@example.com', 'password')
```
Dans cet exemple, nous avons créé un nouvel utilisateur avec le nom d'utilisateur `username`, l'adresse email `email@example.com` et le mot de passe `password`.

### Connexion d'un utilisateur
Pour connecter un utilisateur, nous devons importer la fonction `authenticate` du module `django.contrib.auth` et appeler cette fonction avec le nom d'utilisateur et le mot de passe de l'utilisateur. Par exemple :
```python
from django.contrib.auth import authenticate

user = authenticate(request, username='username', password='password')
```
Dans cet exemple, nous avons connecté l'utilisateur avec le nom d'utilisateur `username` et le mot de passe `password`.

### Déconnexion d'un utilisateur
Pour déconnecter un utilisateur, nous devons importer la fonction `logout` du module `django.contrib.auth` et appeler cette fonction. Par exemple :
```python
from django.contrib.auth import logout

logout(request)
```
Dans cet exemple, nous avons déconnecté l'utilisateur actuellement connecté.

## Protection des pages web
Pour protéger les pages web, nous devons utiliser la décoration `@login_required` du module `django.contrib.auth.decorators`. Cette décoration vérifie si l'utilisateur est connecté avant d'accéder à la page web. Si l'utilisateur n'est pas connecté, il est redirigé vers la page de connexion. Par exemple :
```python
from django.contrib.auth.decorators import login_required

@login_required
def protected_page(request):
    # Code de la page web protégée
    return render(request, 'protected_page.html')
```
Dans cet exemple, nous avons protégé la page web `protected_page` en utilisant la décoration `@login_required`. Si l'utilisateur n'est pas connecté, il est redirigé vers la page de connexion.

## Exemple de projet
Pour illustrer les concepts présentés dans ce chapitre, nous allons créer un projet simple qui utilise les formulaires et l'authentification pour gérer les comptes utilisateurs. Le projet sera un système de gestion de contacts qui permet aux utilisateurs de créer des comptes, de se connecter et de gérer leurs contacts.

### Création du projet
Pour créer le projet, nous devons exécuter la commande suivante dans le terminal :
```bash
django-admin startproject contact_manager
```
Cette commande créera un nouveau projet Django appelé `contact_manager`.

### Création de l'application
Pour créer l'application, nous devons exécuter la commande suivante dans le terminal :
```bash
python manage.py startapp contacts
```
Cette commande créera une nouvelle application Django appelée `contacts`.

### Configuration de l'authentification
Pour configurer l'authentification, nous devons ajouter les lignes suivantes dans le fichier `settings.py` :
```python
INSTALLED_APPS = [
    # ...
    'django.contrib.auth',
    'django.contrib.contenttypes',
    # ...
]

AUTH_USER_MODEL = 'auth.User'
```
Ces lignes activent l'authentification dans le projet.

### Création des modèles
Pour créer les modèles, nous devons ajouter les lignes suivantes dans le fichier `models.py` de l'application `contacts` :
```python
from django.db import models
from django.contrib.auth.models import User

class Contact(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    name = models.CharField(max_length=100)
    email = models.EmailField(max_length=100)
```
Ces lignes créent un modèle `Contact` qui a un champ `user` qui référence le modèle `User` et des champs `name` et `email` pour stocker les informations de contact.

### Création des vues
Pour créer les vues, nous devons ajouter les lignes suivantes dans le fichier `views.py` de l'application `contacts` :
```python
from django.shortcuts import render, redirect
from django.contrib.auth import authenticate, login, logout
from .forms import ContactForm
from .models import Contact

def login_view(request):
    if request.method == 'POST':
        username = request.POST['username']
        password = request.POST['password']
        user = authenticate(request, username=username, password=password)
        if user is not None:
            login(request, user)
            return redirect('contacts:home')
    return render(request, 'login.html')

def logout_view(request):
    logout(request)
    return redirect('contacts:login')

def home_view(request):
    contacts = Contact.objects.filter(user=request.user)
    return render(request, 'home.html', {'contacts': contacts})
```
Ces lignes créent des vues pour la connexion, la déconnexion et la page d'accueil.

### Création des templates
Pour créer les templates, nous devons créer des fichiers `login.html`, `home.html` et `contact.html` dans le dossier `templates` de l'application `contacts`. Ces fichiers contiendront le code HTML pour les pages web.

### Exécution du projet
Pour exécuter le projet, nous devons exécuter la commande suivante dans le terminal :
```bash
python manage.py runserver
```
Cette commande lancera le serveur de développement et nous pourrons accéder au projet à l'adresse `http://localhost:8000`.

## Points clés
* Les formulaires Django sont créés à l'aide de la classe `Form` du module `django.forms`.
* Les champs du formulaire sont définis en tant qu'attributs de la classe.
* La validation des données est effectuée automatiquement par Django lors de la soumission du formulaire.
* L'authentification Django est gérée par le module `django.contrib.auth`.
* La décoration `@login_required` est utilisée pour protéger les pages web.
* Les modèles Django sont définis dans le fichier `models.py` de l'application.
* Les vues Django sont définies dans le fichier `views.py` de l'application.
* Les templates Django sont définis dans le dossier `templates` de l'application.