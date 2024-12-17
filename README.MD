# Python : Cours Complet avec Exemples Détaillés

## Table des Matières
1. [Classes en Python](#1-classes-en-python)
2. [Classes Instanciables](#2-classes-instanciables)
3. [Interaction avec l'Utilisateur](#3-interaction-avec-lutilisateur)
4. [Interface en Ligne de Commande (CLI) avec `argparse`](#4-interface-en-ligne-de-commande-cli-avec-argparse)
5. [Listes en Python](#5-listes-en-python)

---

## 1. Classes en Python

Les **classes** sont des modèles permettant de regrouper des données (attributs) et des comportements (méthodes) associés à des objets. Cela permet de structurer et d'organiser votre code de manière plus claire et modulaire.

### Concepts Importants :
- **Attributs** : Ce sont les données associées à un objet.
- **Méthodes** : Ce sont les fonctions définies à l'intérieur d'une classe et qui agissent sur ses attributs.
- **Constructeur (`__init__`)** : Une méthode spéciale appelée automatiquement lors de la création d'un objet.

### Exemple : Classe Simple
```python
class Person:
    def __init__(self, name, age):
        # Initialisation des attributs
        self.name = name
        self.age = age

    def greet(self):
        # Une méthode qui utilise les attributs
        return f"Hello, my name is {self.name} and I am {self.age} years old."

# Création d'un objet de la classe Person
person = Person("Alice", 30)
print(person.greet())
```

**Explication :**
- La classe `Person` possède deux attributs : `name` et `age`.
- La méthode `greet` retourne une chaîne formatée contenant ces attributs.
- Lorsqu'on instancie un objet (`person = Person(...)`), le constructeur `__init__` est automatiquement exécuté pour initialiser les attributs.

### Exemple : Ajout de Méthodes Supplémentaires
```python
class BankAccount:
    def __init__(self, account_holder, balance=0):
        self.account_holder = account_holder
        self.balance = balance

    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            return f"Deposited {amount}. New balance: {self.balance}"
        return "Invalid deposit amount."

    def withdraw(self, amount):
        if 0 < amount <= self.balance:
            self.balance -= amount
            return f"Withdrawn {amount}. Remaining balance: {self.balance}"
        return "Insufficient funds or invalid withdrawal amount."

# Utilisation de la classe
account = BankAccount("John", 1000)
print(account.deposit(500))  # Dépôt réussi
print(account.withdraw(200))  # Retrait réussi
print(account.withdraw(2000))  # Retrait échoué (fonds insuffisants)
```

**Explications supplémentaires :**
- Cette classe modélise un compte bancaire avec des opérations comme le dépôt et le retrait.
- Les conditions dans les méthodes permettent de gérer les erreurs (montants invalides, fonds insuffisants).

### Exemple : Héritage
L'héritage permet de créer des classes dérivées qui héritent des propriétés et des méthodes d'une classe parent.
```python
class Animal:
    def speak(self):
        return "I make a sound."

class Dog(Animal):
    def speak(self):
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"

# Utilisation
dog = Dog()
cat = Cat()
print(dog.speak())  # Output: Woof!
print(cat.speak())  # Output: Meow!
```

---

## 2. Classes Instanciables

Une **classe instanciable** est une classe que l'on peut utiliser pour créer des objets concrets. Ces objets sont appelés des instances de la classe. Pour qu'une classe soit instanciable, elle doit :

1. Être définie avec le mot-clé `class`.
2. Contenir un constructeur (`__init__`) pour initialiser les attributs de l'objet.
3. Avoir des méthodes pour manipuler ses données ou effectuer des actions.

### Exemple : Classe Instanciable
```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)

# Création d'instances de la classe Rectangle
rect1 = Rectangle(5, 10)
rect2 = Rectangle(3, 4)

print(f"Aire du rect1 : {rect1.area()}")       # Output: 50
print(f"Périmètre du rect2 : {rect2.perimeter()}")  # Output: 14
```

### Exemple Avancé : Gestion de Livres
```python
class Book:
    def __init__(self, title, author, pages):
        self.title = title
        self.author = author
        self.pages = pages

    def description(self):
        return f"'{self.title}' by {self.author}, {self.pages} pages."

# Liste de livres
library = [
    Book("1984", "George Orwell", 328),
    Book("Brave New World", "Aldous Huxley", 268),
    Book("Fahrenheit 451", "Ray Bradbury", 256)
]

for book in library:
    print(book.description())
```

**Résumé :** Les classes instanciables permettent de modéliser des entités du monde réel, comme des rectangles ou des livres, en encapsulant leurs données et comportements dans des objets.

---

## 3. Interaction avec l'Utilisateur

Créer des interactions utilisateur simples peut être fait en utilisant `input()` pour capturer des données saisies.

### Exemple : Saisie d'une Liste de Nombres
```python
print("Entrez des nombres séparés par des espaces :")
numbers = input("Votre saisie : ").split()
numbers = [int(num) for num in numbers]  # Convertir en entiers
print(f"Voici votre liste : {numbers}")
```

**Explication :**
- `input()` capture une chaîne de texte.
- La méthode `.split()` divise la chaîne en une liste d'éléments basés sur les espaces.
- Une compréhension de liste est utilisée pour convertir chaque élément en un entier.

### Exemple : Menu de Sélection
```python
def menu():
    print("Menu Principal")
    print("1. Option 1")
    print("2. Option 2")
    print("3. Quitter")

    choice = input("Entrez votre choix : ")
    if choice == '1':
        print("Vous avez choisi l'Option 1")
    elif choice == '2':
        print("Vous avez choisi l'Option 2")
    elif choice == '3':
        print("Au revoir!")
    else:
        print("Choix invalide.")

menu()
```

---

## 4. Interface en Ligne de Commande (CLI) avec `argparse`

Le module `argparse` est utile pour créer des programmes en ligne de commande où les arguments sont passés lors de l'exécution.

### Exemple : Script CLI pour Calculer des Opérations Mathématiques
```python
import argparse

def main():
    parser = argparse.ArgumentParser(description="Calculatrice CLI")
    parser.add_argument("operation", choices=['add', 'subtract', 'multiply', 'divide'], help="Opération à effectuer")
    parser.add_argument("num1", type=float, help="Premier nombre")
    parser.add_argument("num2", type=float, help="Deuxième nombre")

    args = parser.parse_args()

    if args.operation == 'add':
        result = args.num1 + args.num2
    elif args.operation == 'subtract':
        result = args.num1 - args.num2
    elif args.operation == 'multiply':
        result = args.num1 * args.num2
    elif args.operation == 'divide':
        if args.num2 != 0:
            result = args.num1 / args.num2
        else:
            result = "Erreur : division par zéro"

    print(f"Résultat : {result}")

if __name__ == "__main__":
    main()
```

**Comment exécuter :**
Lancez le script avec des arguments comme suit :
```bash
python script.py add 5 10
```

---

## 5. Listes en Python

Les listes permettent de regrouper plusieurs éléments dans une seule variable et offrent de nombreuses méthodes pour manipuler les données.

### Exemple : Listes avec Boucles et Conditions
```python
names = ["Alice", "Bob", "Charlie"]

# Parcours des éléments avec une boucle
for name in names:
    if len(name) > 3:
        print(f"{name} a plus de 3 lettres.")
    else:
        print(f"{name} a 3 lettres ou moins.")
```


