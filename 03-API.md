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

### 3.1.2. csv

Ce module permet d'analyser et écrire des fichiers CSV. 

Pour récupérer la liste des objets de la collection:

* **Méthode 1 :** valeurs des objets dans une liste
  
  ```python
  import csv
  
  with open('fichier.csv', newline='') as csvfile: # csvfile=itérateur
    r = csv.reader(csvfile)
  
    # Liste des descripteurs
    descripteurs = next(r)
  
    # Liste des objets
    c = []
    for o in collection:
      c.append(o)
  ```
  
  Autres paramètres pour `reader()`: 
  
  - `delimiter` :  `','` par défaut
- **Méthode 2 :**  descripteurs et valeurs des objets dans un dictionnaire (`OrderedDict`)

```python
import csv

with open('fichier.csv', newline='') as csvfile: 
  r = csv.DictReader(f)

  # Ensemble des objets
  c = []
  for o in collection:
    c.append(o) # conversion en dictionnaire classique
```

### 3.1.3. math

Pour les fonctions et constantes usuelles en mathématiques.

```python
import math

racine2 = math.sqrt(2)
```

### 3.1.4. os

Pour la gestion des chemins de fichiers et répertoires.

```python
import os

# Répertoire
curdir = os.getcwd() # répertoire courant
os.chdir('/home/grosbois/test')
ls = os.listdir('/home/grosbois/') # liste du contenu du répertoire

# Fichiers
os.rename("ancien.txt", "nouveau.txt")

# gestion arborescence multiplateforme (/ ou \):
mondir = os.join(curdir, "test")
```

## 3.2. modules d'API tiers

### 3.2.1. matplotlib

Pour la [visualisation de données](https://matplotlib.org/) dans une figure (nécessite la plupart du temps une sortie graphique: *Jupyter*, ...).

- Installation:

```bash
python -m pip install -U pip
python -m pip install -U matplotlib
```

- Importation:

```python
import matplotlib.pyplot as plt
```

#### 3.2.1.2. Approche OO

> Elle est préférable dans un environnement non-intéractif, pour un *backend* PGN, SVG, PDF, PS:
> 
> ```python
> import matplotlib
> 
> matplotlib.use('png') # ou ps, eps, pdf, svg
> ...
> pt.savefig('monfichier.png')
> ```

Une figure (vide):

```python
fig = plt.figure()
fig = plt.figure(figsize = (10,1)) # largeur, hauteur (en pouces)
```

Une figure peut contenir un ou plusieurs `Axes`(zone de tracé où des points peuvent être spécifiés en terme de coordonnées):

```python
fig, ax = plt.subplots() # figure avec un seul Axes
fig, axs = plt.subplots(2,2) # figure avec grille de 2x2 Axes
```

Un `Axes` possède:

- un ou plusieurs tracé:
  
  ```python
  # 1er tracé
  ax.plot([1, 2, 3, 4], [1, 4, 2, 3], label='points') # 1er tracé
  
  # 2ème tracé
  x = [i*0.25 for i in range(10)]
  y = [v**3 for v in x]
  ax.plot(x, y, label='cubique')
  ```

- un titre:
  
  ```python
  ax.set_title("Relevé de tension")
  ```

- des ticks:
  
  ```python
  ax.set_yticks([])
  ```

- des labels:
  
  ```python
  ax.set_xlabel('temps [s]')
  ax.set_ylabel('Tension [V]')
  ```

- une légende (qui affiche les labels):
  
  ```python
  ax.legend() # afficher la légende
  ```

- 2 ou 3 `Axis` avec chacun des valeurs limites et des ticks (utilisation de `Locator`) et ticklabels (utilisation de `Formatter`)

#### 3.2.1.2. Approche pyplot

Elle est préférable dans un environnement interactif, type *Jupyter*.

- pour activer l'environnement interactif dans *Jupyter Notebook*:

```
%matplotlib notebook
```

- pour activer l'environnement interactif dans *Jupyter Lab*:

```
%matplotlib widget
```

> Pour désactiver l'affichage automatique du tracé :
> 
> ```python
> plt.ioff() # (activé par défaut)
> ```
> 
> Pour afficher le tracé lorsque l'affichage automatique :
> 
> ```python
> plt.show()
> ```
> 
> Pour réactiver l'affichage automatique :
> 
> ```python
> plt.ion()
> ```

```python
# 1er tracé
plt.plot([1, 2, 3, 4, [1, 4, 2, 3]], label='points')

# 2nd tracé
x = [i*0.25 for i in range(10)]
y = [v**3 for v in x]
plt.plot(x,y, label='cubique')

# Ticks
plt.xticks = [i in range(0,11)]
plt.yticks = [i in range(0,21)]

# Labels, titre et légende
plt.xlabel('temps [s]')
plt.ylabel('Tension [V]')
plt.title('Relevé de tension')
plt.legend()
```

#### 3.2.1.3. Options de tracé

- Valeurs indexées (par de valeurs de `x`):

```python
plt.plot(y)
```

- types de graphiques:

```python
plt.bar(names, values) # bargraphe
plt.scatter(names, values) # points X,Y
```

- Couleur et type de ligne (=3ème paramètres de `plot`):

```python
plt.plot([1,2,3,4], [1,4,9,16], 'ro') # défaut: 'b-'
```

- Épaisseur des lignes:

```python
plt.plot(x, y, linewidth=2.0)
```

- Utilisation des *setter*s de chaque ligne:
  
  ```python
  line1, line2 = plt.plot(x1,y1,x2,y2)
  
  line1.set_antialiased(False)
  ```

- Modification des propriétés des lignes:
  
  ```python
  lines = plt.plot(x1,y1,x2,y2)
  
  plt.setp(lines, 'color', 'r', 'linewidth', 2.0)
  ```

### 3.2.2. numpy

Pour faciliter la manipulation de liste de valeurs numériques

```python
import numpy as np

x = np.linspace(0,10,100) # 100 valeurs entre 0 et 10
y = x**3 # Cube de chacune des valeurs dans x
```

### 3.2.3. pandas

Pour l'analyss de données:

```python
import pandas as pd
```

- Lire les données depuis un fichier CSV:

```python
df = pd.read_csv('mon_fichier.csv')
```

- Afficher les premières lignes:

```python
df.head()
```

- Sauver dans un fichier CSV:

```python
df.to_csv("mon_fichier.csv")
```

### 3.2.4. PyBluez

*(version 0.22)*

Ce [module](http://people.csail.mit.edu/albert/bluez-intro/c212.html) permet une utilisation plus complète du Bluetooth que les sockets natives (uniquement Linux) et est aussi disponible sous Windows (quelques difficultés d'installation sous WIndows 10 ?)

```python
import bluetooth
```

Pour scanner les périphériques aux alentours (pendant environ 10s):

```python
nearby_devices = bluetooth.discover_devices()
for addr in nearby_devices:
  print(addr, bluetooth.lookup_name(addr))_
```

Communication L2CAP (un peu l'équivalent de UDP). Les ports sont appelés PSM (*Protocol Service Multiplexers*), leurs numéros sont impaires (1-4095: psm réservés, 4097-32765: psm dynamiques):

- Serveur:

```python
# Socket d'écoute
s = bluetooth.BluetoothSocket(bluetooth.L2CAP)
s.bind(("", 0x1001)) # MAC, PSM (entre 0x1001 et 0x8FFF)
s.listen(1)

socket, client_address = s.accept()
print("Connexion avec %s" % bluetooth.lookup_name(client_address))
...

socket.close()
s.close()
```

- Client:

```python
socket = bluetooth.BluetoothSocket(bluetooth.L2CAP)
socket.connect(('00:21:13:01:62:8D', 0x1001)) # MAC et PSM
...
socket.close()
```

> Pour ajuster certains paramètres de communication:
> 
> ```python
> bluetooth.set_l2cap_mtu(socket, 65535) # valeur max, 672 par défaut
> ```

Communication RFCOMM (basée sur L2CAP, un peu l'équivalent de TCP). Les ports sont appelés des *channel*s:

- Serveur:

```python
s = bluetooth.BluetoothSocket(bluetooth.RFCOMM)
s.bind(("", 1)) # MAC, port fixe (entre 1 et 30)
s.listen(1)

socket, client_address = s.accept()
print("Connexion avec %s" % bluetooth.lookup_name(client_address))
...
socket.close()
s.close()
```

- Client:

```python
socket = bluetooth.BluetoothSocket(bluetooth.RFCOMM)
socket.connect(('00:21:13:01:62:8D', 1))
...
socket.close()
```

Discussions entre client et serveur:

```python
data = socket.recv(1024) # taille du tampon
print(data)
socket.send(bytes("Mon message\n", 'ascii'))
```

Le serveur utilise généralement un numéro de port dynamique. SDP (*Service Discovery Protocol*) peut alors être utilisé pour effectuer les opérations suivantes:

- identifier le numéro du premier port libre pour un protocole particulier:

```python
bluetooth.get_available_port(bluetooth.RFCOMM) # ou L2CAP
```

- associer un *Universal Unique Identifier* (uuid: "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" ou "xxxxxxxx" ou "xxxx") pour annoncer/retrouver un service bluetooth particulier.
  
  - Côté serveur:
  
  ```python
  s = bluetooth.BluetoothSocket(bluetooth.RFCOMM)
  port = bluetooth.get_available_port(bluetooth.RFCOMM)
  s.bind("", port)      
  s.listen(1)
  
  uuid = "1e0ca4ea-299d-4335-93eb-27fcfe7fa848"
  bluetooth.advertise_service(s, "Mon service", uuid)
  
  socket, client_address = s.accept()
  ...
  bluetooth.stop_advertising(socket)
  socket.close()
  s.close()
  ```
  
  - Côté client:
  
  ```python
  uuid = "1e0ca4ea-299d-4335-93eb-27fcfe7fa848"
  services_matches = bluetooth.find_service(name=None, uuid=uuid, address=None) # ou MAC spécifique
  
  service = services_matches[0]:
  port = service["port"]
  protocol = service["protocol"]
  name = service["name"]
  host = service["host"]
  
  socket = bluetooth.BluetoothSocket(bluetooth.RFCOMM)
  socket.connect((host, port))
  ...
  socket.close()
  ```

### 3.2.5. pyserial

C'est [module](http://pyserial.sourceforge.net/) spécialisé pour la gestion du port série.

- Pour l'installer sous Fedora 19:

```bash
$ yum install python3-serial
```

- Pour le charger:

```python
import serial
```

- Pour configurer et ouvrir un port:

```python
ser = serial.Serial(port="/dev/ttyUSB0", baudrate=9600)
```

- Pour écrire sur le port:

```python
ser.write(bytes.fromhex('BA0201B9'))
ser.write(b'Bonjour')
```

- Pour lire depuis le port:

```python
ser.read() # 1 seul octet
ser.read(15) # 15 octets
```

- Pour fermer le port

```python
ser.close()  
```

### 3.2.6. pyusb

C'est un [module](http://sourceforge.net/apps/trac/pyusb/) écrit entièrement en Python et compatible avec les versions 2.4 et supérieures. 

Pour l'installer sur Fedora 19:

```bash
$ yum install pyusb
```

> Attention: la distribution Fedora 19 ne propose le paquet *pyusb* que pour Python 2.x. Pour l'utiliser sous Python 3.x, il faut rajouter un lien symbolique:
> 
> ```bash
> $ cd /usr/lib/python3.3/site-packages
> $ ln -s /usr/lib/python2.7/site-packages/usb/ 
> ```

Pour utiliser ce module:

```python
import usb.core
import usb.util
```

> Attention: sans configuration spécifique, il est fort probable que seul l'administrateur puisse prendre le contrôle du périphérique.

#### 3.2.6.1. Connexion/déconnexion

Pour retrouver le périphérique depuis ses identifiants logiciels:

```python
dev = usb.core.find(idVendor=0x1234, idProduct=0x0001)
```

> Dans le cas où plusieurs périphériques utilisent les même identifiants VID/PID (on les distingue alors à l'aide de leur numéro de bus et adresse), on utilise plutôt:
> 
> ```python
> dev = usb.core.find(find_all=True, idVendor=0x1234, idProduct=0x0001)
> ```
> 
> Le paramètre `find_all` est faux par défaut

Pour activer la configuration par défaut:

```python
dev.set_configuration()
```

Pour libérer les ressources en fin de programme:

```python
dev.reset() # Bizarre ?
```

#### 3.2.6.2. Écriture et lecture BULK

- écriture:

```python
msg = 'test'
assert len(dev.write(1, msg, 0, 100)) == len(msg)
```

- lecture:

```python
ret = dev.read(0x81, 64, 0, 100)
```

### 3.2.7. requests

Pour effectuer des requête HTTP:

```python
import requests
```

- méthode `GET`:
  
  ```python
  reponse = requests.get('https://snlpdo.fr/')
  ```
  
  - Pour récupérer un flux binaire:
  
  ```python
  reponse = request.get('https://snlpdo.fr/ICN/img/ciel.png', stream=True).raw
  Image.open(reponse)
  ```
  
  ```python
  reponse = requests.get(url, headers={'referer': 'localhost'})
  ```

- méthode `POST`:

```python
content = ( "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n"
                "<XLS\n"
                "  xmlns:gml=\"http://www.opengis.net/gml\"\n"
                "  xmlns=\"http://www.opengis.net/xls\"\n"
                "  xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" version=\"1.2\"\n"
                "  xsi:schemaLocation=\"http://www.opengis.net/xls http://schemas.opengis.net/ols/1.2/olsAll.xsd\">\n"
                "  <RequestHeader srsName=\"epsg:4326\"/>\n"
                "  <Request maximumResponses=\"1\" methodName=\"GeocodeRequest\" requestID=\"uid42\" version=\"1.2\">\n"
                "  <GeocodeRequest returnFreeForm=\"false\">\n"
                "    <Address countryCode=\"StreetAddress\">\n"
                f"      <freeFormAddress>{adresse}</freeFormAddress>\n"
                "    </Address>\n"
                "  </GeocodeRequest>\n"
                "  </Request>\n"
                "</XLS>\n")
url = f"http://gpp3-wxs.ign.fr/{CLE_IGN}/geoportail/ols"

reponse = requests.post(url, headers={'referer': 'localhost', 'Content-Type': 'text/xml'}, data=content)
```

### 3.2.8. twilio

Pour l'envoi de SMS:

```python
from twilio.rest import Client

# Your Account SID from twilio.com/console
account_sid = "AC7a30b21638561825347996a884c54788"
# Your Auth Token from twilio.com/console
auth_token  = "4dbddd7130b701e91656e54b298f6750"

client = Client(account_sid, auth_token)

message = client.messages.create(
    to="+33684623595", 
    from_="+33755537346",
    body="Le contenu de mon message")

print(message.sid)
```
