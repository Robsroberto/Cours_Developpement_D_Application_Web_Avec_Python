## Concepts de base de Python
Python est un langage de programmation puissant et facile à apprendre, qui est devenu très populaire dans le monde du développement web. Pour commencer à créer des applications web dynamiques avec Django, il est essentiel de comprendre les concepts de base de Python.

### Types de données
Python dispose de plusieurs types de données de base, qui sont les éléments fondamentaux de tout programme. Les principaux types de données en Python sont :
* Les entiers (int) : représentent des nombres entiers, tels que 1, 2, 3, etc.
* Les flottants (float) : représentent des nombres à virgule flottante, tels que 3.14 ou -0.5.
* Les chaines de caractères (str) : représentent des séquences de caractères, telles que "Bonjour" ou 'Bonjour'.
* Les booléens (bool) : représentent des valeurs logiques, telles que True (vrai) ou False (faux).
* Les listes (list) : représentent des collections de valeurs, telles que [1, 2, 3] ou ["a", "b", "c"].
* Les tuples (tuple) : représentent des collections de valeurs immuables, telles que (1, 2, 3) ou ("a", "b", "c").

### Structures de contrôle
Les structures de contrôle permettent de gérer le flux d'exécution d'un programme. Les principaux types de structures de contrôle en Python sont :
* Les conditions (if/elif/else) : permettent de prendre des décisions en fonction de conditions spécifiques.
* Les boucles (for/while) : permettent de répéter des instructions plusieurs fois.

Exemple de condition :
```python
x = 5
if x > 10:
    print("x est supérieur à 10")
elif x == 5:
    print("x est égal à 5")
else:
    print("x est inférieur à 10")
```
Exemple de boucle :
```python
fruits = ["mangue", "banane", "orange"]
for fruit in fruits:
    print(fruit)
```
### Fonctions
Les fonctions sont des blocs de code qui peuvent être appelés plusieurs fois dans un programme. Elles permettent de réutiliser du code et de rendre les programmes plus modulaires.

Exemple de fonction :
```python
def bonjour(nom):
    print("Bonjour, " + nom)

bonjour("Amadou")
```
### Modules
Les modules sont des fichiers qui contiennent des fonctions, des classes et des variables qui peuvent être importées dans d'autres programmes. Les modules permettent de réutiliser du code et de partager des fonctionnalités entre plusieurs programmes.

Exemple d'importation de module :
```python
import math

print(math.pi)
```
### Exercices pratiques
Pour mieux comprendre les concepts de base de Python, il est essentiel de pratiquer. Voici quelques exercices pratiques :
* Créez un programme qui demande à l'utilisateur de saisir son nom et son âge, puis affiche un message de bienvenue avec son nom et son âge.
* Créez un programme qui calcule la somme de deux nombres saisis par l'utilisateur.
* Créez un programme qui affiche la liste des jours de la semaine.

## Utilisation de Python dans le développement web
Python est un langage de programmation très populaire dans le développement web, en particulier avec le framework Django. Django est un framework de développement web qui permet de créer des applications web robustes et scalables.

### Exemple d'utilisation de Python dans le développement web
Supposons que nous voulions créer une application web qui permet aux utilisateurs de créer des comptes et de se connecter. Nous pourrions utiliser Python et Django pour créer cette application.

Exemple de code :
```python
from django.shortcuts import render
from django.http import HttpResponse

def inscription(request):
    if request.method == "POST":
        # Traitement de l'inscription
        return HttpResponse("Inscription réussie")
    else:
        return render(request, "inscription.html")
```
## Points clés
* Les types de données de base en Python sont les entiers, les flottants, les chaines de caractères, les booléens, les listes et les tuples.
* Les structures de contrôle permettent de gérer le flux d'exécution d'un programme.
* Les fonctions permettent de réutiliser du code et de rendre les programmes plus modulaires.
* Les modules permettent de réutiliser du code et de partager des fonctionnalités entre plusieurs programmes.
* Python est un langage de programmation très populaire dans le développement web, en particulier avec le framework Django.
* Django est un framework de développement web qui permet de créer des applications web robustes et scalables.