# Chapitre 2. Langage

Cf. [documentation en ligne](https://docs.python.org/3.7/contents.html)

> Les commentaires dans les programmes débutent avec le caractère # et s'étendent jusqu'à la fin de la ligne.

Python est un langage à *typage dynamique*: les variables ne sont pas déclarées explicitement mais implicitement lors d'une affectation (le type est alors celui qui *correspond* au mieux à la valeur fournie).

> **Attention:** une nouvelle affectation de la variable avec un type différent change le type de celle-ci.

Tous les types de données correspondent à des classes. Le type d'un objet s'obtient avec la commande:

```python
type(3.2)
type("a") # ou type('a')
```

## 2.1 Littéral

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

Pour connaître la longueur d'une liste:

```python
l = len(ma_liste)
```

Pour modifier la liste:

- ajouter un élément à la fin:

```python
ma_liste.append(4)
```

- ajouter une liste à la fin d'une autre:

```python
ma_liste.extend(liste2)
```

- extraire le dernier élément:

```python
element = ma_liste.pop()
```

- insérer un élément à une certaine position (en décalant les suivants):

```python
ma_liste.insert("bonjour", 4)
```

- pour supprimer un élément (et décaler les suivants vers le début):

```python
del ma_liste[1] # supprimer un seul élément
del ma_liste[1:3] # supprimer les éléments 1 et 2
```

Opérations sur tous les éléments:

- pour parcourir les éléments:

```python
for e in ma_liste:
  print(e)
```

- pour énumérer les éléments:

```python
for i, item in enumerate(ma_liste):
  print(i, item)
```

- pour faire la somme de tous les éléments:

```python
sum([1, 3, 5, 6]) # donne 15
```

- pour vérifier la présent/absence d'un élément:

```python
5 in ma_liste
5 not in ma_liste
```

- pour permuter 2 éléments:

```python
ma_liste[0], ma_liste[4] = ma_liste[4], ma_liste[0]
```

- pour copier une liste:

```python
liste2 = liste1[:] # liste entière
liste2 = liste1[2:7] # éléments 2 à 6
liste2 = liste1[:7] # éléments 0 à 6
liste2 = liste1[7:] # éléments à partir de 7
```

- pour trier:

```python
['omega', 'alpha', 'gamme'].sort() # tri dans la même liste
sorted(['omega', 'alpha', 'gamme']) # donne une nouvelle liste
sorted(['omega', 'alpha', 'gamme'], reverse=True) # tri inversé
```

- pour combiner 2 listes (en une liste de tuples):

```python
liste1 = ['a', 'b', 'c']
liste2 = [1, 2, 3]
z = zip(liste1, liste2) # création d'un générateur
liste3 = liste(z) # donne [('a', 1), ('b', 2), ('c', 3)]
```

    et pour les décombiner:

```python
l1, l2 = zip(*liste3)
```

Compréhension de liste:

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

> Attention: contrairement à une fonction, un générateur ne peut pas être appelé directement.fig
