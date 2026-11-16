# Programmatio  en Python - Séance 4
## Itération définie, formatage de l'affichage et approfondissement des chaînes et des listes

**Durée :** 3 heures  
**Programme :** University of Helsinki — Python Programming MOOC 2026, Part 4

**Sections étudiées :**
- 4. Definite iteration
- 5. Print statement formatting
- 6. More strings and lists

**Support de cours :** https://programming-26.mooc.fi/part-4/

---

# 1. Objectifs de la séance

À la fin de cette séance, vous serez capables de :

- Parcourir et manipuler des collections de données.
- Utiliser `range()` et convertir un objet `range` en liste.
- Rechercher le meilleur ou le pire élément d'une liste selon un critère.
- Formater un affichage avec les paramètres `sep` et `end` de `print()`.
- Utiliser les f-strings pour construire des affichages structurés.
- Extraire des portions de chaînes et de listes avec le slicing.
- Comprendre l'immuabilité des chaînes de caractères.
- Utiliser les méthodes `count()` et `replace()`.
- Organiser un programme en plusieurs fonctions qui communiquent entre elles.

# 2. Rappel : parcourir une collection

Nous connaissons déjà les boucles `for`.

Une boucle `for` permet de parcourir les éléments d'une collection.

```python
numbers = [3, 2, 4, 5, 2]

for number in numbers:
    print(number)
````

Chaque élément est récupéré successivement, sans avoir besoin de gérer manuellement un indice.

On peut également parcourir une chaîne :

```python
name = "Python"
for character in name:    
    print(character)
```

# **3. Definite iteration**

## **3.1. Parcourir une collection**

Une collection est une structure qui contient plusieurs éléments. Les listes et les chaînes de caractères en sont deux exemples.

On peut parcourir une liste avec une boucle `for` :

```python
my_list = [3, 2, 4, 5, 2]
for item in my_list:    
    print(item)
```

Cette méthode est généralement préférable à une boucle `while` utilisant un indice lorsque l'on souhaite simplement traiter chaque élément.

En effet, avec `while`, il faudrait gérer soi-même la position :

```python
my_list = [3, 2, 4, 5, 2]
index = 0
while index < len(my_list):    
    print(my_list[index])    
    index += 1
```

Les deux programmes produisent le même résultat, mais la boucle `for` est plus simple à lire.

**À retenir :** utiliser directement `for element in collection` lorsque l'on souhaite parcourir les éléments sans avoir besoin de leurs indices.

## **3.2. La fonction** `range()`

La fonction `range()` permet de générer une séquence de nombres entiers.

Elle est notamment utile lorsque l'on connaît le nombre d'itérations nécessaires.

```python
for i in range(5):    
    print(i)
```

Résultat :

```shell
0
1
2
3
4
```

La borne supérieure est exclue.

On peut également préciser un début et une fin :

```python
for i in range(3, 7):    
    print(i)
```

Résultat :

```shell
3
4
5
6
```

Enfin, un troisième argument permet de définir le pas :

```python
for i in range(1, 9, 2):    
    print(i)
```

Résultat :

```
1
3
5
7
```

Le pas peut aussi être négatif :

```python
for i in range(6, 2, -1):    
    print(i)
```

Résultat :

```shell
6
5
4
3
```

## 3.3. Transformer `range` en liste

La fonction `range()` ne renvoie pas directement une liste, mais un objet de type `range`.

```python
numbers = range(2, 7)
print(numbers)
```

Résultat :

```python
range(2, 7)
```

Pour obtenir une véritable liste, on peut utiliser la fonction `list()` :

```python
numbers = list(range(2, 7))
print(numbers)
```

Résultat :

```python
[2, 3, 4, 5, 6]
```

Cette conversion est utile lorsque l'on souhaite conserver les valeurs générées dans une liste et les manipuler par la suite.

## **3.4. Trouver le meilleur ou le pire élément d'une liste**

Un problème courant en programmation consiste à identifier l'élément qui possède la meilleure ou la pire caractéristique selon un critère donné.

Par exemple :

- Le nombre le plus élevé.
- Le nombre le plus faible.
- Le mot le plus long.
- Le mot le plus court.
- L'étudiant ayant obtenu la meilleure note.

Pour résoudre ce problème, on peut utiliser une variable auxiliaire qui mémorise le meilleur élément trouvé jusqu'à présent.

### **Exemple : trouver le plus grand nombre**

```python
numbers = [12, 5, 27, 8, 19]
largest = numbers[0]
for number in numbers:    
    if number > largest:        
        largest = number
print(largest)
```

Résultat :

```shell
27
```

Comment fonctionne ce programme ?

1. On suppose initialement que le premier nombre est le plus grand.
2. On parcourt les éléments de la liste.
3. On compare chaque nombre avec le maximum actuel.
4. Si le nombre courant est supérieur, on met à jour `largest`.
5. À la fin, la variable contient le plus grand élément.

### **Exemple : trouver le mot le plus long**

```python
words = ["Python", "Java", "JavaScript", "C"]
longest = words[0]
for word in words:    
    if len(word) > len(longest):        
        longest = word
print(longest)
```

Résultat :

```shell
JavaScript
```

Le même principe peut être utilisé pour trouver le mot le plus court :

```python
shortest = words[0]
for word in words:    
    if len(word) < len(shortest):        
        shortest = word
print(shortest)
```

**Point important :** il faut choisir correctement la valeur initiale. Ici, on utilise le premier élément de la liste. Ces exemples supposent donc que la liste n'est pas vide.

# **4. Print statement formatting**

Jusqu'à présent, nous avons principalement utilisé `print()` de manière simple.

Python permet cependant de contrôler plus précisément la manière dont les informations sont affichées.

## **4.1. Plusieurs arguments dans** `print()`

Il est possible de passer plusieurs arguments à `print()`, séparés par des virgules.

```python
name = "Alice"
age = 22
print("Name:", name, "Age:", age)
```

Résultat :

```shell
Name: Alice 
Age: 22
```

Contrairement à la concaténation avec `+`, cette méthode accepte directement des valeurs de types différents.

Par exemple :

```python
number = 42
message = "The answer is"
print(message, number)
```

Résultat :

```shell
The answer is 42
```

Python ajoute automatiquement un espace entre les arguments.

## **4.2. Le paramètre** `sep`

Le paramètre `sep` permet de choisir le séparateur placé entre les arguments de `print()`.

Par défaut, ce séparateur est un espace.

```python
print("Python", "Java", "C++")
```

Résultat :

```shell
Python Java C++
```

On peut remplacer cet espace par un autre caractère :

```python
print("Python", "Java", "C++", sep=", ")
```

Résultat :

```shell
Python, Java, C++
```

On peut également supprimer complètement le séparateur :

```python
print("Hello", "World", sep="")
```

Résultat :

```shell
HelloWorld
```

Ou placer chaque argument sur une ligne différente :

```python
print("Python", "Java", "C++", sep="\n")
```

Résultat :

```shell
Python
Java
C++
```

Le caractère spécial `\n` représente un retour à la ligne.

## **5.3. Le paramètre** `end`

Par défaut, chaque appel à `print()` se termine par un retour à la ligne.

```python
print("Hello")
print("World")
```

Résultat :

```python
Hello
World
```

Le paramètre `end` permet de modifier ce comportement.

```python
print("Hello", end="")
print("World")
```

Résultat :

```shell
HelloWorld
```

On peut aussi ajouter un espace :

```python
print("Hello", end=" ")
print("World")
```

Résultat :

```shell
Hello World
```

Ou utiliser un autre caractère :

```python
print("Loading", end="...")
print("Done")
```

Résultat :

```shell
Loading...Done
```

**À retenir :**

- `sep` contrôle ce qui sépare les arguments.
- `end` contrôle ce qui est ajouté à la fin de l'affichage.

## **4.4. Les f-strings**

Les f-strings permettent d'insérer directement des variables dans une chaîne de caractères.

```python
name = "Alice"
age = 22
print(f"Hello {name}, you are {age} years old.")
```

Résultat :

```shell
Hello Alice, you are 22 years old.
```

On peut également utiliser une expression :

```python
number = 5
print(f"Double: {number * 2}")
```

Résultat :

```shell
Double: 10
```

Les f-strings peuvent être stockées dans des variables :

```python
name = "Alice"
age = 22
city = "Paris"
greeting = f"Hello {name}, you are {age} years old."
print(greeting + f" You live in {city}.")
```

## **4.5. Formater les nombres décimaux**

Par défaut, Python peut afficher beaucoup de chiffres après la virgule.

```python
number = 1 / 3
print(number)
```

Résultat :

```shell
0.3333333333333333
```

On peut contrôler la précision avec un spécificateur de format.

```python
print(f"{number:.2f}")
```

Résultat :

```shell
0.33
```

La notation `.2f` signifie que l'on souhaite afficher deux chiffres après la virgule.

Autres exemples :

```python
number = 3.141592
print(f"{number:.1f}")
print(f"{number:.2f}")
print(f"{number:.4f}")
```

Résultat :

```shell
3.1
3.14
3.1416 # Notez que python a arrondi au supérieur
```

Python arrondit la valeur affichée. La variable d'origine n'est pas modifiée.

## **4.6. Contrôler la largeur de l'affichage**

Les f-strings permettent également de réserver un certain nombre de caractères pour une valeur.

```python
names = ["Steve", "Jean", "Katherine", "Paul"]
for name in names:    
    print(f"{name:15} centre {name:>15}")
```

Résultat :

```shell
Steve           centre           Steve
Jean            centre            Jean
Katherine       centre       Katherine
Paul            centre            Paul
```

Dans cet exemple :

- `:15` réserve 15 caractères.
- `:>15` réserve 15 caractères et aligne le texte à droite.

On peut également utiliser :

| Format | Fonction                                        |
| ------ | ----------------------------------------------- |
| `:15`  | Largeur de 15 caractères, alignement par défaut |
| `:<15` | Alignement à gauche                             |
| `:>15` | Alignement à droite                             |
| `:^15` | Centrage                                        |

Ces possibilités sont particulièrement utiles pour afficher des tableaux dans le terminal.

# 5. More strings and lists

Cette section approfondit les opérations sur les chaînes et les listes.

Nous allons notamment étudier le slicing, l'immuabilité des chaînes et deux méthodes supplémentaires : `count()` et `replace()`.

## 5.1. Le slicing : extraire une portion

Le slicing permet d'extraire une partie d'une chaîne ou d'une liste.

La syntaxe générale est :

```python
sequence[start:stop]
```

- `start` : indice de départ, inclus.
- `stop` : indice de fin, exclu.

Exemple avec une chaîne :

```python
word = "exemplary"
print(word[3:7])
```

Résultat :

```shell
mpla
```

Le même principe fonctionne avec une liste :

```python
numbers = [3, 4, 2, 4, 6, 1, 2, 4, 2]
print(numbers[3:7])
```

Résultat :

```shell
[4, 6, 1, 2]
```

## **5.2. Utiliser un pas dans le slicing**

Comme avec `range()`, il est possible de préciser un pas.

La syntaxe devient :

```python
sequence[start:stop:step]
```

Exemple :

```python
word = "exemplary"
print(word[0:7:2])
```

Résultat :

```shell
eepa
```

Python récupère un caractère sur deux à partir de l'indice 0.

On peut aussi parcourir une liste à rebours :

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8]
print(numbers[6:2:-1])
```

Résultat :

```shell
[7, 6, 5, 4]
```

## **5.3. Omettre les indices**

Il n'est pas obligatoire de préciser les deux indices.

Si l'indice de départ est omis, Python commence au début de la séquence.

```python
word = "Python"
print(word[:3])
```

Résultat :

```shell
Pyt
```

Si l'indice de fin est omis, Python parcourt la séquence jusqu'à sa fin.

```python
print(word[3:])
```

Résultat :

```shell
hon
```

On peut également omettre les deux :

```python
print(word[:])
```

Cela permet d'obtenir une séquence contenant tous les éléments.

## **5.4. Inverser une chaîne ou une liste**

Le slicing permet d'inverser une séquence grâce à un pas négatif.

```python
word = "Python"
print(word[::-1])
```

Résultat :

```shell
nohtyP
```

Même principe avec une liste :

```python
numbers = [1, 2, 3, 4, 5]
print(numbers[::-1])
```

Résultat :

```shell
[5, 4, 3, 2, 1]
```

Cette technique est particulièrement pratique pour inverser une séquence sans écrire de boucle.

## **5.5. Les chaînes de caractères sont immuables**

Les chaînes de caractères sont dites **immuables** (*immutable*).

Cela signifie que leur contenu ne peut pas être modifié directement après leur création.

Par exemple :

```python
word = "Python"
word[0] = "J"
```

Ce programme provoque une erreur :

```shell
TypeError: 'str' object does not support item assignment
```

En revanche, les listes sont modifiables :

```python
numbers = [1, 2, 3]
numbers[0] = 10
print(numbers)
```

Résultat :

```shell
[10, 2, 3]
```

Il faut bien distinguer deux opérations.

Modifier une liste :

```python
my_list = [1, 2, 3]
my_list[0] = 10
```

Remplacer une chaîne par une nouvelle chaîne :

```python
my_string = "Hey"
my_string = my_string + "!"
print(my_string)
```

Résultat :

```shell
Hey!
```

Dans le second cas, la chaîne originale n'a pas été modifiée. Une nouvelle chaîne a été créée et affectée à la variable.

## **5.6. La méthode**`count()`

La méthode `count()` permet de compter le nombre d'occurrences d'un élément dans une chaîne ou une liste.

Exemple avec une chaîne :

```python
text = "banana"
print(text.count("a"))
```

Résultat :

```shell
3
```

On peut également rechercher une sous-chaîne :

```python
text = "How much wood would a woodchuck chuck?"
print(text.count("ch"))
```

Exemple avec une liste :

```python
numbers = [1, 2, 3, 1, 4, 5, 1, 6]
print(numbers.count(1))
```

Résultat :

```shell
3
```

**Attention :** `count()` ne compte pas les occurrences qui se chevauchent.

Par exemple :

```python
text = "aaaa"
print(text.count("aa"))
```

Résultat :

```shell
2
```

Même si l'on pourrait identifier trois occurrences de `"aa"` en autorisant les chevauchements, Python n'en compte que deux.

## **5.7. La méthode** `replace()`

La méthode `replace()` permet de remplacer une sous-chaîne par une autre.

```python
text = "Hi there"
new_text = text.replace("Hi", "Hello")
print(new_text)
```

Résultat :

```shell
Hello there
```

La méthode remplace toutes les occurrences correspondantes.

```python
sentence = "sheila sells seashells on the seashore"
print(sentence.replace("she", "SHE"))
```

Résultat :

```shell
SHEila sells seaSHElls on the seashore
```

### **Attention à l'immuabilité**

`replace()` ne modifie pas la chaîne originale. Elle renvoie une nouvelle chaîne.

Ce programme ne produit donc pas le résultat attendu :

```python
text = "Python is fun"
text.replace("Python", "Java")
print(text)
```

Résultat :

```shell
Python is fun
```

Pour conserver le résultat, il faut le stocker :

```python
text = "Python is fun"
text = text.replace("Python", "Java")
print(text)
```

Résultat :

```shell
Java is fun
```

## **5.8. Attention aux variables globales dans les fonctions**

Une fonction peut accéder à une variable définie en dehors d'elle. On appelle cela une variable globale.

Cependant, utiliser directement des variables globales dans les fonctions est généralement une mauvaise pratique.

Exemple problématique :

```python
name_list = ["Steve", "Jean", "Katherine", "Paul"]
def print_names():    
    for name in name_list:       
        print(name)
print_names()
```

La fonction dépend directement de la variable globale `name_list`.

Cela peut rendre le programme difficile à comprendre et à tester.

Il est préférable de transmettre les données à la fonction avec un paramètre :

```python
def print_names(names):    
    for name in names:        
        print(name)

students = ["Steve", "Jean", "Katherine", "Paul"]
print_names(students)
```

La fonction peut désormais fonctionner avec différentes listes :

```python
print_names(["Alice", "Bob"])
print_names(["Python", "Java", "C++"])
```

**À retenir :** privilégier les paramètres et les valeurs de retour plutôt que les variables globales.

# **6. Organiser un programme en plusieurs fonctions**

Un programme plus complexe ne devrait pas nécessairement être écrit dans un seul bloc de code.

Il est préférable de le diviser en plusieurs fonctions, chacune ayant une responsabilité précise.

## **6.1. Décomposer un problème**

Prenons un programme qui demande plusieurs nombres à l'utilisateur, puis les analyse.

On peut le diviser en trois fonctions :

1. Une fonction qui récupère les nombres.
2. Une fonction qui affiche les nombres.
3. Une fonction qui effectue leur analyse.

## **6.2. Transmettre des données entre fonctions**

Exemple :

```python
def input_numbers(how_many):
    numbers = []

    for i in range(how_many):
        number = int(input(f"Number {i + 1}: "))
        numbers.append(number)

    return numbers

def print_numbers(numbers):
    print("The numbers are:")

    for number in numbers:
        print(number)

def analyze(numbers):
    mean = sum(numbers) / len(numbers)
    smallest = min(numbers)
    greatest = max(numbers)

    return (
        f"There are {len(numbers)} numbers. "
        f"The mean is {mean}, "
        f"the smallest is {smallest} "
        f"and the greatest is {greatest}."
    )

numbers = input_numbers(5)

print_numbers(numbers)

result = analyze(numbers)
print(result)
```

Ce programme illustre plusieurs notions importantes :

- Une fonction peut recevoir des données grâce à ses paramètres.
- Une fonction peut construire une liste et la renvoyer avec `return`.
- Une fonction peut transmettre un résultat à une autre partie du programme.
- Les données peuvent circuler entre plusieurs fonctions sans utiliser de variables globales.

## **6.3. Le rôle d'une fonction principale**

Dans un programme plus important, on peut regrouper le déroulement général dans une fonction appelée `main()`.

```python
def calculate_mean(numbers):    
    return sum(numbers) / len(numbers)

def main():    
    numbers = [10, 20, 30, 40]    
    mean = calculate_mean(numbers)    
    print(f"Mean: {mean}")
main()
```

La fonction `main()` organise le déroulement du programme et appelle les fonctions auxiliaires.

Cette organisation permet de tester plus facilement chaque fonction séparément.

# **7. Exercices du MOOC**

## **7.1. Definite iteration**

Objectifs :

- Approfondir le parcours de listes et de chaînes.
- Manipuler `range()` et `list()`.
- Rechercher des éléments selon un critère.
- Identifier le meilleur ou le pire élément d'une collection.

Lien : [https://programming-26.mooc.fi/part-4/4-definite-iteration/](https://programming-26.mooc.fi/part-4/4-definite-iteration/?utm_source=chatgpt.com)

## **7.2. Print statement formatting**

Objectifs :

- Maîtriser les paramètres `sep` et `end`.
- Utiliser les f-strings.
- Formater les nombres et les chaînes.

Lien :\
[https://programming-26.mooc.fi/part-4/5-print-statement-formatting/](https://programming-26.mooc.fi/part-4/5-print-statement-formatting/?utm_source=chatgpt.com)

## **7.3. More strings and lists**

Objectifs :

- Utiliser le slicing avancé.
- Comprendre l'immuabilité des chaînes.
- Manipuler `count()` et `replace()`.
- Organiser un programme en plusieurs fonctions.
- Transmettre des données entre fonctions.

Lien : [https://programming-26.mooc.fi/part-4/6-strings-and-lists/](https://programming-26.mooc.fi/part-4/6-strings-and-lists/?utm_source=chatgpt.com)

Les exercices sont accessibles directement dans chaque section du MOOC. Les étudiants doivent suivre les consignes et les tests automatiques de la plateforme.

# **8. Mini-projet : analyseur de texte - troisième version**

Nous poursuivons le projet d'analyseur de texte commencé lors des séances précédentes.

L'objectif est maintenant de rendre le programme plus complet et mieux organisé.

## **8.1. Objectif**

Le programme doit demander un texte à l'utilisateur et effectuer plusieurs opérations :

- Afficher le texte inversé.
- Compter le nombre d'occurrences d'un caractère.
- Remplacer une expression par une autre.
- Afficher certaines portions du texte.
- Présenter les résultats de manière structurée.

Le programme doit utiliser les notions étudiées pendant cette séance.

## **8.2. Étape 1 : récupérer le texte**

Demander à l'utilisateur de saisir une phrase.

```python
text = input("Enter a text: ")
```

Afficher ensuite le texte saisi.

## **8.3. Étape 2 : inverser le texte**

Utiliser le slicing pour obtenir une version inversée de la chaîne.

Indice : le pas négatif permet de parcourir la chaîne à rebours.

## **8.4. Étape 3 : compter les occurrences**

Demander à l'utilisateur de saisir un caractère.

Utiliser `count()` pour déterminer combien de fois ce caractère apparaît dans le texte.

Attention : la méthode distingue les majuscules et les minuscules.

## **8.5. Étape 4 : remplacer une expression**

Demander à l'utilisateur :

- Une expression à rechercher.
- Une expression de remplacement.

Utiliser `replace()` pour produire une nouvelle version du texte.

Ne pas oublier que les chaînes sont immuables : il faut conserver le résultat de `replace()`.

## **8.6. Étape 5 : extraire une portion du texte**

Demander deux indices à l'utilisateur.

Utiliser le slicing pour afficher uniquement la portion correspondante.

Faire attention à la borne de fin, qui est exclue.

## **8.7. Étape 6 : organiser le programme**

Créer plusieurs fonctions :

- Une fonction pour afficher le texte inversé.
- Une fonction pour compter les occurrences.
- Une fonction pour remplacer une expression.
- Une fonction pour afficher une portion du texte.

Chaque fonction doit recevoir les informations dont elle a besoin en paramètres.

Éviter d'utiliser des variables globales.

## **8.8. Étape 7 : formater les résultats**

Utiliser les f-strings, `sep` et `end` pour présenter les résultats de manière lisible.

Exemple de présentation :

```shell
TEXT ANALYSIS
------------------------------

Original text:
Python is a programming language

Reversed text:
egaugnal gnimmargorp a si nohtyP

Character statistics:
Number of occurrences of 'a': 3

Replacement:
Python is a programming language

Extracted text:
programming

------------------------------
```

Les étudiants doivent produire eux-mêmes les résultats à partir du texte saisi.

# **9. Bilan de la séance**

| Notion                 | À retenir                                                         |
| ---------------------- | ----------------------------------------------------------------- |
| `range()`              | Génère une séquence de nombres                                    |
| `list()`               | Convertit une séquence en liste                                   |
| `largest` / `shortest` | Variables auxiliaires pour rechercher un élément selon un critère |
| `sep`                  | Définit le séparateur entre les arguments de `print()`            |
| `end`                  | Définit ce qui termine l'affichage de `print()`                   |
| f-strings              | Permettent de formater des chaînes                                |
| `.2f`                  | Contrôle le nombre de décimales affichées                         |
| `sequence[start:stop]` | Extrait une portion d'une séquence                                |
| `sequence[::-1]`       | Inverse une séquence                                              |
| Immuabilité            | Une chaîne ne peut pas être modifiée directement                  |
| `count()`              | Compte les occurrences                                            |
| `replace()`            | Renvoie une nouvelle chaîne avec des remplacements                |
| Paramètres             | Permettent de transmettre des données à une fonction              |
| `return`               | Permet de renvoyer un résultat                                    |
| `main()`               | Organise le déroulement général d'un programme                    |

Les trois chapitres et leurs objectifs sont ceux du MOOC officiel : 

- [Definite iteration](https://programming-26.mooc.fi/part-4/4-definite-iteration/)
- [Print statement formatting](https://programming-26.mooc.fi/part-4/5-print-statement-formatting/)
- [More strings and lists](https://programming-26.mooc.fi/part-4/6-strings-and-lists/)