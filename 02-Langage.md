# Chapitre 2. Langage

[toc]

Cf. [documentation en ligne](https://docs.python.org/3.7/contents.html)

> Les commentaires dans les programmes débutent avec le caractère # et s'étendent jusqu'à la fin de la ligne.

Python est un langage à *typage dynamique*: les variables ne sont pas déclarées explicitement mais implicitement lors d'une affectation (le type est alors celui qui *correspond* au mieux à la valeur fournie).

> **Attention:** une nouvelle affectation de la variable avec un type différent change le type de celle-ci.

Tous les types de données correspondent à des classes. Le type d'un objet s'obtient avec la commande:

```python
type(3.2)
type("a") # ou type('a')
```

## 2.1 Valeur littérale

### 2.1.1 Nombre

> Le nombre d'octets pour représenter une données n'est pas spécifié. Le système alloue dynamiquement autant d'espaces que nécessaire (ou possible),

- Les nombres entiers:  `int`. Les valeurs peuvent être spécifiées en base décimale, octale, hexadécimale ou binaire:

```python
a = 10 # décimal
a = 0o123 # octal (=83)
a = 0xa3 # hexadécimal (=163)
a = 0b10010011 # binaire (=147)
```

- Les nombres réels (virgule flottante): `float`

```python
b = 4.1
b = .4
b = 4.
b = 3e8
```

> Remarque: Python peut parfois changer lui-même la notation d'un nombre (il choisit toujours la notation la plus économique)

### 2.1.2. Booléen

Les booléens: `bool`. 

Les deux valeurs possibles sont `True` et `False`.

### 2.1.3. Chaîne de caractères

Les chaînes de caractères (séquence de texte): `str`.

Elles ne sont pas modifiables et ne peuvent contenir que des éléments de type `str`.

```python
ma_chaine = str() # chaîne vide
ma_chaine = "" # chaîne vide
ma_chaine = """ma chaîne qui peut s'étendre
sur plusieurs lignes"""
ma_chaine = "bonjour"
ma_chaine = 'bonjour'
```

> Il n'existe pas de type spécifique pour un caractère seul, ce dernier est traité comme n'importe quelle autre chaîne.

Bien que n'étant pas une séquence, une chaîne supporte un grand nombre de méthodes/syntaxes identiques:

```python
ma_chaine[0] # 1er caractère
for c in ma_chaine: # boucle sur les caractères
  print(c, end='') 
ma_chaine[1:3] # caractères 1 et 2
ma_chaine[:2] # 2 premiers caractères
min(ma_chaine) # caractère avec le code le plus petit
max(ma_chaine) # caractère avec le code le plus grand
ma_chaine.index('b') # Position de la 1ère occurrence
ma_chaine.count('b') # Nombre d'occurrences
"abc" in ma_chaine # Vérifier si la sous-chaîne est présente
"abc" not in ma_chaine # Vérifier si la sous-chaîne est absente
```

La méthode `split()` permet de découper une chaîne en fonction d'un séparateur:

```python
a = '1+2'
b = a.split('+') # b contient ['1', '2']
```

Quelques méthodes spécifiques:

```python
list(ma_chaine) # convertir en liste, 1 caractère par élément
ma_chaine.upper() # convertir en majuscules
ma_chaine.lower() # convertir en minuscules
ma_chaine.capitalize() # 1ère lettre en majuscule
ma_chaine.title() # 1ère lettre de chaque mot en majuscule
ma_chaine.center(10) # Centrer en ajoutant des espaces
ma_chaine.center(10, '*') # Centrer en ajoutant des *
'epsilon'.endswith('on') # True ou False
​'epsilon'.startswith('on') # True ou False
​'Eta'.find('ta') # comme index avec des sous-chaînes, -1 si non trouvé
​'Eta'.rfind('ta') # idem depuis la fin
​'kappa'.find('a', 2) # chercher depuis l'index 2
​'lambda30'.isalnum() # si uniquement des lettres et des chiffres
​'lambda30'.isalpha() # si uniquement des lettres
​'lambda30'.isdigit() # si uniquement des chiffres
​'lambda30'.islower() # si minuscules
​'lambda30'.isupper() # si majuscules
​'lambda30'.isspace() # si espaces
​','.join(['a', 'b', 'c']) # joindre les éléments str en une chaîne avec , comme séparateur
​'phi chi\npsi'.split() # sépare dans une séquence
​'  tau  '.lstrip() # supprime les espaces/fin de ligne à gauche
​'  tau  '.rstrip() # supprime les espaces/fin de ligne à droite
​'  tau  '.strip() # supprime les espaces/fin de ligne à droite et à gauche
​'www.cisco.com'.lstrip('w.') # supprime les w et . à gauche
​'this is it'.replace('it', 'are') # remplace toutes les occurrences
​'this is it'.replace('it', 'are', 1) # remplacement 1ère occurrence
```

Substitution dans une chaîne:

- Méthode *format*:

```python
print("Mohamed a {} ballons".format(27)) 
​print("Est-ce que ton {} {}?".format("chien", "mort"))
```

- Depuis Python 3.6, il est possible d'utiliser les chaînes de formatage (préfixe *f*):

```python
name = "Fred"
​f"He said his name is {name!r}." # name!r est équivalent à repr(name) 
​
​width = 10
​precision = 4
​value = decimal.Decimal("12.34567")
​f"result: {value:{width}.{precision}}"  # nested fields
​
​today = datetime(year=2017, month=1, day=27)
​f"{today:%B %d, %Y}"
​
​number = 1024
​f"{number:#0x}"  # using integer format specifier
```

- Opérateur de substitution (%):

```python
"le résultat est %d" % 2 # Une seule substitution
​"la %s des %d nombres vaut %.2f" % ('somme', 3, 12.333)    # 3 arguments: tuple
​"Date: %(jour)02d/%(mois)02d/%(annee)04d" % {'jour':1,'mois':2,'annee':2013} # dictionnaire
```

> Ce type de substitution est considéré moins robuste que les deux autres.

Pour convertir entre le code Unicode et un seul caractère:

```python
ord('a') # récupérer le code Unicode
chr(945) # récupérer le caractère
```

### 2.1.4. Conversions

Certaines conversions entre types sont implicites:

- `int` vers `float` :

```python
4 + 3.5 # 4 est transformé en float pour le calcul
```

- `int` vers `bool` :

```python
if a==True:
  print("OK")
else:
  print("NON")
```

D'autres nécessitent d'utiliser explicitement des fonctions: `int()`, `float()` ou `str()` 

```python
int("13")
float("4.2")
str(15)
int(4.5) # float vers int
```

## 2.2 Variable

Elle permet de mémoriser une valeur en permettant son accès à partir d'un nom. Il est donc préférable d'utiliser un nom explicite (sans espace, ne commençant pas par un chiffre): Python recommande d'utiliser des noms uniquement avec des minuscules et de séparer les mots par des `_`.

Portée:

- Une variable définie dans une fonction n'est pas accessible en dehors de celle-ci (i.e. variable *locale*).

- Une variable définie en dehors d'une fonction n'est accessible qu'en lecture dans le corps de celle-ci. Réassigner une nouvelle valeur dans la fonction revient à créer une nouvelle variable locale (avec le même nom).

- Pour étendre la portée d'une variable au cœur des fonctions, il faut la déclarer avec le mot-clé `global`. 

Les variables de type:

- **scalaire** ne permettent de stocker qu'une seule valeur

- **vectoriel** permet de stocker plusieurs données à la fois (parfois de types différents).

## 2.3. Opérateur

Quelques opérateurs arithmétiques spécifiques à Python:

| Opérateur | Signification           | Exemple                                            |
| --------- | ----------------------- | -------------------------------------------------- |
| `**`      | puissance               | `2**3`(résultat en `int` ou `float` selon les cas) |
| `/`       | division réelle         | `5/2`(=2.5, résultat toujours du type `float`)     |
| `//`      | quotient de la division | `5//2`(=2, résultat de type `int`)                 |

> Attention: les opérateurs `//` et `%` peuvent aussi s'utiliser sur des `float` (`//` donne en `float` la valeur de l'entier inférieur ou égal)

Les opérateurs ont des priorités. À priorités égales, l'évaluation d'une expression se fait de la gauche vers la droite (sauf pour l'opérateur `**`)

Pour les chaînes de caractères:

- Opérateurs arithmétiques (concaténation/répétition):

```python
"Raphael "+"Grosbois" # donne "Raphael Grosbois"
"James"*3 # donne "JamesJamesJames"
```

- Opérateurs de comparaison:

```python
15 <= x < 19 # valeur dans une plage
'alpha' < 'alphabet' # compare les codes des 1er carac non idem
ch1 == ch2
ch1 != ch2
```

- Opérateur de substitution (`%`):

```python
"le résultat est %d" % 2 # Une seul substitution
​"la %s des %d nombres vaut %.2f" % ('somme', 3, 12.333)    # 3 arguments: tuple
​"Date: %(jour)02d/%(mois)02d/%(annee)04d" % {'jour':1,'mois':2,'annee':2013} # dictionnaire
```

Les opérateurs booléens sont les suivants:

- la conjonction (*et*): `and`

- la disjonction (*ou*): `or`

- la négation (*non*): `not`

Les opérateurs binaires: `&` (conjonction, *et*), `|`  (disjonction, *ou*), `~` (négation), `^` (ou exclusif), `>>` (décalage à droite), `<<` (décalage à gauche).

## 2.4. Séquence

Il s'agit d'un type de données *vectoriel* permettant de stocker plusieurs valeurs pouvant être parcourues de manière séquentielle ()élément par élément).

### 2.4.1. Liste

Les éléments peuvent être de type différents (même s'ils sont généralement de même type).

```python
ma_liste = list() # vide
ma_liste = [] # vide
ma_liste = [1, 3.14, "bonjour"] # éléments séparés par des virgules
ma_liste[0] # 1er élément
ma_liste[-1] # dernier élément
ma_liste[-2] # avant dernier
ma_liste[6:9] # (sous-)liste avec éléments 6, 7 et 8
ma_liste[1:10:2] # liste avec éléments 1, 3, 5, 7, 9
```

La longueur de la liste:

```python
l = len(ma_liste)
```

- Pour compléter la liste:

```python
ma_liste.append(4) # ajouter un élément à la fin
ma_liste.insert("bonjour", 4) # insérer en position 4 (décaler à droite)
ma_liste.extend(liste2) # concaténer une liste à la fin
```

- Pour vider la liste:

```python
element = ma_liste.pop() # extraire le dernier élément
del ma_liste[1] # supprimer un seul élément (décaler à gauche)
del ma_liste[1:3] # supprimer les éléments 1 et 2
del ma_liste # supprimer la liste
```

- Parcourir les éléments:

```python
# foreach
for e in ma_liste:
  print(e)

# énumération
for i, item in enumerate(ma_liste):
  print(i, item)
```

- Somme de tous les éléments:

```python
sum([1, 3, 5, 6]) # donne 15
```

- pour vérifier la présence/absence d'un élément:

```python
5 not in ma_liste
5 in ma_liste
pos = ma_liste.index(5) # position 1ère occurrence
```

- pour permuter 2 éléments:

```python
ma_liste[0], ma_liste[4] = ma_liste[4], ma_liste[0]
```

- Copier une liste:

```python
liste2 = liste1[:] # liste entière
liste2 = liste1[2:7] # éléments 2 à 6
liste2 = liste1[:7] # éléments 0 à 6
liste2 = liste1[7:] # éléments à partir de 7
```

- Trier:

```python
['omega', 'alpha', 'gamme'].sort() # tri dans la même liste
sorted(['omega', 'alpha', 'gamme']) # donne une nouvelle liste
sorted(['omega', 'alpha', 'gamme'], reverse=True) # tri inversé
```

- Combiner 2 listes (en une liste de tuples):

```python
liste1 = ['a', 'b', 'c']
liste2 = [1, 2, 3]
z = zip(liste1, liste2) # création d'un générateur
liste3 = liste(z) # donne [('a', 1), ('b', 2), ('c', 3)]
```

- Décombiner:

```python
l1, l2 = zip(*liste3)
```

- Compréhensions:

```python
carres = [x**2 for x in range(10)] # boucle for
​liste = [x for x in liste1 if x%2 != 0] # boucle for avec un if
​liste = [1 if x%2 == 0 else 0 for x in range(10) ] # if avant for permet d'utiliser else
​echiquier = [[VIDE for i in range(8)] for j in range(8)] # 2D
```

### 2.4.2. P-uplet (tuple)

C'est une liste non modifiable d'éléments qui peuvent être de types différents.

```python
mon_tuple = tuple() # vide
mon_tuple = () # vide
mon_tuple = { "bonjour", 46, 3.14, "demain" }
tuple2 = 1., .5, .25, .125 # parenthèses non obligatoires
tuple3 = (1,) # ne pas oublier la virgule si 1 seul élément
tuple4 = tuple2 + tuple3 # concaténation
```

Utilisation de tuples:

```python
x, y, z = 1, 2, 4 # assignations multiples
data[1], data[2] = data[2], data[1] # permutation
```

> Le module `collections` permet de définir des p-uplets nommés (`namedtuple`):
> 
> ```python
> from collections import namedtuple
> Personne = namedtuple('Personne', ['nom', 'prenom', 'jour', 'mois', 'annee'])
> 
> p = Personne('Paul', 'Dupont', 3, 'mars', 1980)
> print('Mon nom est {} {}, je suis né le {} {} {}'.format(p.nom, p.prenom, p.jour, p.mois. p,annee))
> ```
> 
> Ce type construit de données permet d'éviter la création d'une classe qui n'aurait pas de méthode.

### 2.4.3. Tableau

Le type `array` permet de stocker des éléments du même type (spécifié lors de la création). C'est un *enrobage* autour du type tableau bas niveau (ex: en *C*). 

Il est cependant préférable d'utiliser le type `list` lorsque possible (le module `array` n'est d'ailleurs pas chargé par défaut).

```python
import array

a = array.array('B', [1, 2, 3, 4]) # B: unsigned int
```

### 2.4.4. Séquence d'octets

Elles sont principalement utilisées lors de communications (liaisons série, Bluetooth...)

`bytes`: séquence d'entiers sous la forme d'octets non signés et immuables. L'exemple typique est une suite de caractères ASCII. Ils s'utilisent quasiment comme des chaînes de caractères (préfixées de `b`)

2 principaux types:

```python
a = b'12' # 2 octets '1' (=49) et '2'(=50)
a = b'\x0f\x12' # 2 octets: 15 et 18
a = bytes(10) # 10 octets à 0
a = bytes(range(20)) # 20 octets valeurs allant de 0 à 19
```

Conversions:

- entre séquence et entiers:

```python
a = bytes([12]) # 1 entier vers 1 octet
a = bytes([46, 46, 46]) # 3 entiers vers 3 octets
a[0] # octet vers entier (valeur du premier élément)
[b for b in a] # liste d'entiers
```

- entre une séquence d'octets et chaîne de caractères:

```python
bytes("Coucou", 'ascii') # ou 'utf-8'
b'Coucou'.decode('ascii') # ou 'utf-8'
```

- entre séquence d'octets et représentation en chaîne hexadécimale:

```python
a = bytes.fromhex('0F 1206') # 3 octets (espaces non pris en compte)
hex(a[0]) # séquence vers chaîne
{:02x}.format(a[0])
```

`bytearray`: version modifiable des `bytes`. N'est utilisable qu'après une initialisation avec un constructeur et ne peut contenir que des entiers compris entre 0 et 255.

```python
a = bytearray()
a = bytearray(10) # 10 octets initialisés à 0
a = bytearray(range(20))
a = bytearray(b'Hi!')
```

## 2.5. Set

C'est un ensemble d'éléments uniques non ordonnés

- Création depuis une liste:

```python
s = set(['a', 'b', 'c', 'a']) # set de 3 éléments
```

- Ajout/suppression:

```python
s.add('e') # ajouter un élément
s.pop() # supprimer un élément (aléatoire ?)
```

## 2.6. Dictionnaire

Il s'agit d'un type de données *vectoriel* qui permet de stocker des éléments sous la forme de couples:

clé / valeur

La classe associée s'appelle `dict`. C'est une table de hachage où les clés et valeurs peuvent être de n'importe quel type.

> Un dictionnaire débute et se termine par les caractères respectifs `{` et `}` et chaque couple s'écrit au format `clé : valeur`.

- Création d'un dictionnaire:

```python
mon_dict = dict() # vide
mon_dict = {} # vide
mon_dict = { 'lundi':'monday', 'mardi':'tuesday'} # clé/valeur séparées par :
```

- Valeur d'un élément:

```python
mon_dict['lundi'] # valeur associée à la clé 'lundi' (erreur si n'existe pas)
mon_dict.get('lundi') # valeur ou None
mon_dict.get('lundi', 'message') # valeur ou 'message' si clé n'existe pas
```

- Ajouter un élément:

```python
mon_dict['mercredi'] = 'wednesday'
```

- Supprimer un élément:

```python
del mon_dict['mardi']
```

- Supprimer le dictionnaire:

```python
del mon_dict
```

- Pour parcourir les éléments:

```python
for key in mon_dict:
  print("{} -> {}".format(key, mon_dict[key]))
```

ou

```python
for key, val in mon_dict.items():
  print(key, val)
```

ou

```python
# mon_dict.keys() retourne une liste de clés
for key in sorted(mon_dict.keys()): # tri des clés
  print(key, '->', mon_dict[key])
# mon_dict.values() retourne une liste de valeurs
for v in mon_dict.values():
  print(v)
```

> Attention: l'ordre d'affichage n'est pas nécessairement celui d'entrée.

## 2.7. Exécution conditionnelle

La structure if/elif/else:

```python
if a<=0:
  print('a est négatif')
elif a==0:
  print('a est nul')
else:
  print('a est positif')
```

> Bien que déconseillé, il est possible de placer une unique instruction après le caractère `: ` (sans aller à la ligne)
> 
> ```python
> if a<=0: print('a est négatif')
> elif a==0: print('a est nul')
> else: print('a est positif')
> ```

## 2.8. Boucle

Boucle while:

```python
while True:
  pass
```

Boucle for:

```python
for i in range(100): # 0, 1, ..., 99
  print(i)
```

ou

```python
for i in range(2,8): # 2, 3, ..., 7
  print(i)
```

ou

```python
for i in range(2,8,3): # 2, 5, 8
  print(i)
```

Les deux mots-clé `continue` et `break` permettent respectivement de passer directement à l'itération suivante et de sortir de la boucle.

> Ces 2 types de boucles peuvent être suivis d'une structure `else` qui est toujours exécutée, que la boucle ait itéré ou non:
> 
> ```python
> i=1
> while i<5:
>   print(i, end=' ')
>   i+=1
> else:
>   print("else", i)
> # 1 2 3 4 "else" 5
> ```
> 
> ou
> 
> ```python
> for i in range(5):
>   print(i, end=' ')
> else:
>   print("else", i)
> # 0 1 2 3 4 "else" 4
> ```

> Attention: Il faut nécessairement une instruction après un `if`, `while` et `for`. Dans le cas contraire, il suffit d'utiliser l'instruction `pass`.

## 2.9. Fonction

Elle sert dans les cas suivants:

- pour factoriser: si un fragment de code apparaît plus d'une fois à plusieurs endroits du programme.

- pour segmenter: si une portion de code devient trop grande à lire ou comprendre.

- pour la collaborer: si le développement du code doit être réparti entre plusieurs programmeurs.

La déclaration se fait avec le mot-clé `def` (i.e. *define*):

```python
def mhello():
  print('hello')

def somme(a, b, c):
  print(a, '+', b, '+', c, '=', str(a+b+c))
```

> Attention: il n'est pas possible d'appeler une fonction avant qu'apparaisse sa déclaration.

Fonctions qui s'appliquent sur d'autres fonctions:

- `map()`:  prend une fonction et ses entrées et retourne un itérateur contenant les résultats de la fonction appliquées aux entrées.

```python
m = map(lambda x:x**2, [1, 2, 3, 4]) # fonction classique ou lambda
print(list(m))
```

- `filter()`: prend une fonction et ses entrées et retourne un itérateur contenant uniquement les entrées pour lesquelles la fonction a retourné `True` :

```python
f = filter(lambda x:x%2==0, [1, 2, 3, 4]) # fonction classique ou lambda
print(list(f))
```

### 2.9.1. Fonctions prédéfinies

Certaines fonctions sont directement définies dans le langage:

- `print`

- `del`

- `type`

- `len`

### 2.9.2. Argument

Lors de l'invocation, les arguments (paramètres) peuvent être de type:

- positionnels (dans le même ordre que dans la déclaration):

```python
somme(2,4,6)
```

- mot-clés (ordre arbitraire):

```python
somme(c=6, b=4, a=2)
```

>  Les deux types ne peuvent être mixés que si l'on commence avec la forme positionnelle.
> 
> ```python
> somme(2, c=6, b=4) # a=2
> ```

Il est aussi possible de spécifier des valeurs par défaut pour certains paramètres lors de la déclaration:

```python
def presentation(prenom, nom="Dupont"):
  print("Bonjour, je m'appelle,", prenom, nom, ".")
```

### 2.9.3. Valeur de retour

L'instruction `return` seule est optionnelle et permet de terminer (prématurément) une fonction sans aucune valeur de retour. Si l'on tente de récupérer la valeur de retour, on obtient `None`

### 2.9.4. Lambda fonction

C'est une fonction anonyme (même s'il est possible de la mémoriser dans une variable) qui se déclare avec le mot-clé `lambda`:

```python
two = lambda : 2 # pas d'argument, retourne 2
sqr = lambda x : x*x # 1 argument
pwr = lambda x,y : x**y # 2 arguments

for i in range(-2, 3):
  print(sqr(i), pwr(i, two()))
```

## 2.10. Itérateur/générateur

Un itérateur doit fournir deux méthodes `__iter__` (retourne l'objet lui-même, appelé une fois à l'initialisation) et `__next__()` (appelé à chaque itération, retourne `StopIteration` si plus aucune valeur).

Utilisation d'un iterateur:

```python
e = next(mon_iter) # 1 seul élément

for e in mon_iter: # boucle sur tous les element
  print(e)
```

Un exemple de générateur est la plage de nombres `range` (elle est appelée plusieurs fois en fournissant en valeur différente à chaque fois puis finit par signaler la fin de la série):

```python
range(1, 10, 2) # chiffres impairs de 1 à 9
```

Pour construire un générateur, on peut utiliser:

- l'instruction `yield` qui est l'équivalent de `return` dans une fonction qui conserve l'état courant (les variables gardent leurs valeurs jusqu'à l'appel suivant)

```python
def powersOf2(n):
  pow = 1
  for i in range(n):
    yield pow
    pow *= 2
```

- avec une syntaxe semblable à une compréhension de liste:

```python
genr = (1 if x%2==0 else 0 for x in range(10))
```

Un générateur s'utilise:

- dans le contexte d'une boucle `for` (avec l'opérateur `in`):

```python
for v in powersOf2(8):
  print(v)
for v in genr: # ou directement for v in (1 if x%2...)
  print(v)
```

- dans une compréhension de liste ou converti en liste à l'aide de la fonction `list()`:

```python
t = [x for x in powersOf2(5)]
t2 = list(powersOf2(5))
```

> Attention: contrairement à une fonction, un générateur ne peut pas être appelé directement.

## 2.11. Module

C'est un fichier qui contient du code Python et qui peut être importé depuis un autre. On peut y trouver des variables, fonctions et classes.

> La variable `__name__` permet de savoir si le module est exécuté directement (`__name__=='__main__'`) ou s'il est importé depuis un autre (`__name__=='__nomdumodule__'`)
> 
> ```python
> if __name__ == '__main__':
>   # code à n'exécuter que si
>   # le module est utilisé directement
>   # (i.e. non importé depuis un autre)
> ```

Contenu:

- la première ligne du module débute par un *shebang*:

```python
#!/usr/bin/env python3
```

- Ensuite on retrouve la *docstring* (chaîne pouvant être multiligne):

```python
""" description du module """
```

> Cette documentation peut être consultée à l'aide de la variable `__doc__`:
> 
> ```python
> import monmodule
> 
> print(monmodule.__doc__)
> ```
> 
> ou depuis la console Python:
> 
> ```python
> >>> help(monmodule)
> ```

L'initialisation d'un module correspond aux ligne d'instruction en dehors des déclarations de fonctions et classes. Elle ne s'effectue que la première fois que le module est utilisé.

Il n'existe pas de moyen de cacher des variables ou fonctions internes mais, par convention, ces dernières sont considérées comme privées lorsque préfixées par `_` ou `__`.

```python
__ma_variable_privee = 5
def __ma_fonction_privee():
  pass
```

La liste des répertoires (modifiable) dans lequel Python recherche un module est donnée par la variable `path` (module `sys`):

```python
from sys import path

path.append('../modules')
```

La recherche s'arrête dès qu'un premier module avec le nom correspondant est trouvé. Il existe 2 façons d'importer un module:

- **Méthode 1**: l'espace de noms importé reste distinct du courant

```python
import math # module math (=espace de noms)

print(math.sin(math.pi/2)) # méthode et variable de l'espace de noms math
```

> Il est possible de renommer l'espace de noms importé (=alias, le nom du module original n'est alors plus utilisable):
> 
> ```python
> import math as M # M devient le nouvel espace de nom
> 
> print(M.sin(M.pi/2))
> ```

- **Méthode 2:** fusion de certaines parties dans l'espace de noms courant (la dernière redéfinition l'emporte)

```python
from math import sin,pi

print(sin(pi/2))
```

> Il est possible de renommer les parties importées:
> 
> ```python
> from math import pi as PI, sin as sine
> ```

> Attention: même si ce n'est pas conseillé, il est possible d'importer le contenu de tout un module dans l'espace de noms courant:
> 
> ```python
> from math import *
> ```

Pour lister le contenu d'un module (ordre alphabétique):

```python
import math

liste = dir(math) # fournit une liste
print(liste)
```

## 2.12. Package

C'est un container (module qui contient des sous-modules) qui s'apparente souvent à un répertoire qui contient:

- obligatoirement un fichier d'initialisation (parfois vide): `__init__.py`,

- 0, 1 ou plusieurs modules,

- 0, 1 ou plusieurs sous-packages.

> Pour gagner de la place, il est possible de compresser un package en un fichier *zip*: 
> 
> ```python
> from sys import path
> 
> path.append('../monpackage.zip')
> ```
> 
> Le package s'utilise de la même manière que s'il n'était pas compressé.

## 2.13. Exception

Elle est *levée* lorsque Python ne sait pas quoi faire avec un code: le programme s'arrête en affichant un message, sauf si cette dernière est gérée.

Les exceptions sont hiérarchiques et possèdent un nom (63 prédéfinis dans python 3): `BaseException` (racine), `Exception` (erreur dans le code), `ImportError`, `ValueError`, `KeyboardInterrupt` (<kbd>Ctrl</kbd> + <kbd>c</kbd>), `ArithmeticError`, `OverflowError` (nombre trop grand), `ZeroDivisionError`, `AssertionError` (assertion qui échoue), `LookupError` (référence à une collection invalide), `MemoryError` (manque de RAM), `KeyError` (accès à un élément de collection inexistant), `IndexError` (accès à un élément de séquence non existant)...

Pour gérer une exception:

- Méthode simple (groupée):

```python
try:
  # Instruction pouvant
  # lever une exception
except:
  # Instruction en cas d'exception
```

- Méthode détaillée:

```python
try:
  # Instruction pouvant
  # lever une exception
except ZeroDivisionError:
  # Instruction en cas d'exception 1
except ValueError:
  # Instruction en cas d'exception 2
except:
  # pour les autres exceptions
```

> Les différentes exceptions sont évaluées dans l'ordre où elles sont écrites (attention à la hiérarchie): il faut commencer par les exceptions les plus précises et terminer par les plus générales.

- Méthode combinée:

```python
try:
  # Instruction pouvant
  # lever une exception
except (IndexError, ValueError):
  # Instruction en cas d'exception
```

Il est possible d'ajouter 2 branchements supplémentaires qui sont exécutés respectivement si aucune exception n'est levée et dans tous les cas:

```python
try:
  # code pouvant lever une exception
except:
  # si exception levée
else:
  # si aucune exception
finally:
  # dans tous les cas
```

Pour lever manuellement une exception:

```python
raise ZeroDivisionError # n'importe où dans le code
raise # uniquement dans un except (relève la même exception)
```

Une assertion peut aussi lever une exception (`AssertionError`) en cas d'erreur:

```python
assert x>=0.0
```

Les exceptions sont, elles-mêmes, des classes:

- pour obtenir plus d'information sur une exception:

```python
try:
  # code pouvant lever une exception
except Exception as e:
  print(e)
  print(e.__str__())
```

- il est possible de créer une sous-classe d'une exception existante:

```python
class PizzaError(Exception):
  def __init__(self, pizza='Unknown', message=''):
    Exception.__init__(self,message)
    self.pizza = pizza

class TooMuchCheeseError(PizzaError):
  def __init__(self, pizza='Unknown', cheese='>100', message=''):
    PizzaError.__init__(self, pizza, message)
    self.cheese = cheese

def makePizza(pizza, cheese):
  if pizza not in ['margherita', 'capricciosa', 'calzone']:
    raise PizzaError
  if cheese > 100:
    raise TooMuchCheeseError
  print("Pizza ready !")

try:
  makePizza('margherita', 110)
except TooMuchCheeseError as tmce:
  print(tmce, ':', tmce.cheese)
except PizzaError as pe:
  print(pe, ':', pe.pizza)
```

## 2.14. Classe

Instanciation d'un objet:

```python
mon_objet = MaClasse()
```

Pour savoir si un objet est une instance d'une certaine classe:

```python
isinstance(obj, classe)
```

Pour savoir si 2 objets sont les mêmes (i.e. référencent vers le même emplacement mémoire):

```python
objet1 is objet2
```

Création de la classe:

- Le constructeur s'appelle `__init__`,

- Le paramètre `self` correspond à l'objet en cours de création.

- Les variables de classe se créée nécessairement en dehors de toute méthode. Elles existent même si aucun objet n'a été instancié.
  Pour obtenir une liste des variables de classe:
  
  ```python
  print(MaClasse.__dict__)
  ```

- Les propriétés de type *variable d'instance* se créée à tout moment (de préférence dans le constructeur) en utilisant `self`.
  
  > 2 objets d'une même classe peuvent avoir des propriétés différentes (une `AttributeError` est levée si on essaye d'accéder à une variable d'instance qui n'existe pas).
  > La liste des propriétés d'un objet peut s'obtenir en consultant le dictionnaire `__dict__`:
  > 
  > ```python
  > print(monobj.__dict__)
  > ```

- L'encapsulation peut s'obtenir en préfixant le nom d'une propriété ou d'une méthode par `__` (*mangling*).
  
  > Une telle propriété ou méthode n'est pas réellement privée: python l'a seulement renommée automatiquement sous la forme `_Class__maPropriete`.

- Le constructeur et les méthodes ont nécessairement un premier paramètre qui se nomme (de préférence) `self`.

- La méthode qui est invoquée lorsqu'on utilise un objet comme paramètre de la fonction `print` s'appelle `__str__`.

```python
class MaClasse():
  """Documentation de la classe, accessible via MaClasse.__doc__ """

  Counter = 0 # variable de classe

  def __init__(self): # constructeur
    self.__stk = [] # propriété (variable d'instance)
    Class.Counter += 1

  def pop(self, val): # méthode publique
    self.__stk.append(val)

  def __str__(self): # utilisée par print
    return str(self.__stk)
```

Pour créer une sous-classe de `MaClasse`:

```python
class MaSousClasse(MaClasse):
  def __init__(self):
    MaClasse.__init__(self) # appeler le constructeur sur-classe
    # variante super().__init__()

    self.__sum = 0 # nouvelle propriété
```

> Il est possible d'hériter de plusieurs classes à la fois (mais cela reste généralement déconseillé):
> 
> ```python
> class SubClass(Class1, Class2)
> ```
> 
> `Class1` est prioritaire sur `Class2` en cas de propriété identique

Pour savoir si une classe hérite d'une autre:

```python
issubclass(Class1, Class2) # Class1 hérite de Class2 ?
```

> Note: toute classe est considérée comme sous-classe d'elle-même.

Certaines variantes de classes prédéfinies contiennent les informations suivantes:

- `__name__`: chaîne de caractères contenant le nom de la classe.

```python
print(MaClass.__name__)
print(type(mon_objet).__name__)
```

- `__module__`: chaîne de caractères contenant le nom du module qui contient la définition de la classe:

```python
print(MaClasse.__module__)
print(type(mon_objet).__module__)
```

- `__doc__`: chaîne de caractères contenant la documentation de la classe

```python
print(MaClasse.__doc__)
print(type(mon_obj).__doc__)
```

- Les super-classes d'une classe:

```python
for x in MaClasse.__bases__: # tuple
  print(x.__name__)
```

Pour:

- savoir si une variable d'instance ou de classe existe:

```python
if hasattr(mon_obj, 'ma_propriete'):
  print(mon_obj.ma_propriete)
if hasattr(MaClasse, 'ma_propriete'):
  print(MaClasse.ma_propriete)
```

- consulter/modifier une variable d'instance ou de classe (i.e. attribut):

```python
val = getattr(obj, name)
setattr(obj, name, nouvelle_valeur)
```

## 2.15. Gestion de la console

### 2.15.1. Affichage avec print

>  `print` est devenue une fonction depuis la version 3.0 de Python
> 
> ```python
> print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)
> ```

Exemples d'utilisation:

```python
print("x=", 2*2) # items séparés par espace, terminé par \n
print("x=", 2*2, sep="", end=" ")
```

### 2.15.2. Acquisition

Pour récupérer les données saisies par l'utilisateur dans la console:

```python
reponse = input()
repons2 = input("Entrer la valeur: ")
```

## 2.16. Fichiers

Python les considère comme des flux. 3 flux sont déjà ouverts par défaut (module `sys`):

- `sys.stdin` : entrée standard,

- `sys.stdout`:  sortie standard,

- `sys.stderr`: sortie erreur standard.

Modes d'ouverture:

```python
stream = open('file.txt', mode='r', encoding=None) # en lecture
stream = open('file.txt', mode='w', encoding=None) # en écriture
stream = open('file.txt', mode='a', encoding=None) # en ajout
stream = open('file.txt', mode='r+', encoding=None) # en lecture et ajout
stream = open('file.txt', mode='w+', encoding=None) # en écriture et ajout
```

- tous ces modes d'ouverture peuvent être suffixés par `'b'` ou `'t'` pour indiquer respectivement une ouverture en mode binaire ou texte (par défaut).

- le paramètre de `encoding` peut aussi valoir `'utf-8'`...

- le paramètre `newline` peut valoir `''` (fin de ligne universel), `'\n'`, `'\r\n'`...

Fichier texte:

- lecture:

```python
ch = stream.read(1) # 1 caractère, '' si fin
content = stream.read() # tout le flux (attention à la taille)
ligne = stream.readline() # 1 seule ligne
lignes = stream.readlines() # liste avec toutes les lignes du fichier
lignes = stream.readlines(20) # liste de 20 lignes
```

- écriture:

```python
stream.write(c) # 1 caractère
stream.write(ligne+'\n')
```

> Pour écrire sur la sortie erreur:
> 
> ```python
> import sys
> 
> sys.stderr.write("Message d'erreur")
> ```

- fermeture

```python
stream.close()
```

> Comme l'objet créé à l'ouverture est une instance de la classe `iterable` (lecture d'une ligne par itération), il est possible d'écrire les instructions suivantes:
> 
> ```python
> from os import strerror
> 
> try:
>   for line in open('file.txt', 'rt'): # fermeture auto à la fin
>     print(line)
> except IOError as exc:
>   strerror(exc.errno)
> ```

Autre format avec fermeture automatique:

```python
with open('myfile.txt', 'r') as f:
  file_data = f.read()
```

Fichier binaire: l'écriture (`'wb'`) et la lecture (`'rb'`) utilisent des `bytearray`:

```python
data = bytearray(10) # 10 octets
... # modification des données
stream.write(data)
...
stream.readinfo(data) # lecture (retourne le nombre d'octets lus)
data2 = bytearray(stream.read()) # non modifiable, fichier entier
data2 = bytearray(stream.read(5)) # non modifiable, 5 octets
```

Gestion des exceptions:

```python
from os import exc.strerror

try:
  # ouverture, fermeture
  # et autres actions sur le fichier
except IOError as exc:
  # exc.errno = errno.ENOENT (fichier n'existe pas), 
  # errno.EMFILE (trop de fichiers ouverts)...
  strerror(exc.errno) # gestion adaptée de exc.errno
```