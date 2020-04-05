# Chapitre 3. API

## 3.1 Modules de l'API standard

### 3.1.1. argparse

Ce module, basé sur le module déprécié *optparse*, permet de créer et générer l'interface de la ligne de commande.

```python
import argparse
```

 Dès sa création, le parser ajoute automatiquement l'option *-h/--help* (affichage de l'aide) au programme:

```python
parser = argparse.ArgumentParser()
args = parser.parse_args()
```

Pour définir un nouvel argument positionnel (et l'aide associée):

```python
parser.add_argument('arg1', help="description de l'argument") # type chaîne
parser.add_argument('arg2', type=int, help="description de l'argument entier")
```

On y accède ensuite avec les instructions:

```python
print(args.arg1)
print(args.arg2**2)
```

Pour définit un argument optionnel:

```python
parser.add_argument("--verbosity", help="description associée") # nécessite une valeur
# Option booléenne (pas de valeur)
parser.add_argument("-verbose", help="description", action="store_true")
# OPtion booléenne et option raccourcie
parser.add_argument("-v", "--verbose", help="description", action="store_true")
```
