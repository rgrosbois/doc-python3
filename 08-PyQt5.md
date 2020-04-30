# Chapitre 8. PyQt5

(prononcer *paille-cute five*)

Cette bibliothèque a été initialement développée pour le langage *C++*.

- Installation (version 5.14.2):

```bash
>>> pip install PyQt5
```

- Documentation en ligne: [wiki.qt.io](https://wiki.qt.io/Main)

## 8.1. Application

L'application elle-même est un objet de la classe `QApplication`:

```python
import sys
from PyQt5.QtWidgets import QApplication

if __name__ == "__main__":
    app = QApplication(sys.argv)
    window = MaFenetre()
    sys.exit(app.exec_())
```

### 8.1.1. Fenêtre

Il s'agit d'un objet d'une classe héritant de `QWidget`:

```python
import sys
from PyQt5.QtWidgets import QApplication, QWidget

class MaFenetre(QWidget):
    def __init__(self):
        QWidget.__init__(self)
        self.setWindowTitle("Ma Fenetre")
        # self.setLayout(...) # définir l'agencement
        self.show()
```

### 8.1.2. Agencements

- horizontal: `QHBoxLayout`

  ```python
  from PyQt5.QtWidgets import QHBoxLayout
  
  horiz = QHBoxLayout()
  horiz.addWidget(mon_label) # élément à ajouter
  ```
  
- vertical: `QVBoxLayout`

  ```python
  from PyQt5.QtWidgets import QVBoxLayout
  
  vertical = QHBoxLayout()
  vertical.addWidget(mon_label) # élément à ajouter
  ```
  
- quadrillage: `QGridLayout`:

  ```python
  from PyQt5.QtWidgets import QGridLayout
  
  grid = QGridLayout()
  grid.addWidget(mon_label, 0, 0, 1, 0) # ligne, colonne, nb lignes, nb colonnes
  ```

Pour imbriquer les agencements:

```python
vertical.addLayout(horizontal)
```

### 8.1.3. Composants

- Label: `QLabel`

  ```python
  from PyQt5.QtWidgets import QLabel
  
  label = QLabel("Hello")
  ```

- Saisie de texte: `QLineEdit`

  ```python
  from PyQt5.QtWidget import QLineEdit
  
  name_input = QLineEdit()
  ```

  Pour récupérer le contenu du champ:

  ```python
  texte = name_input.text()
  ```

- Bouton: `QPushButton`

  ```python
  from PyQt5.QtWidgets import QPushButton
  
  ok_button = QPushButton("OK")
  ```

  Pour changer le texte du bouton après coup:
  
  ```python
  ok_button.setText("Nouveau texte")
  ```

### 8.1.4. Événement

Il faut spécifier une méthode de rappel pour chaque signal à traiter:

```python
ok_button.clicked.connect(clicked_button) 
ok_button.released.connect(released_button)
ok_button.pressed.connect(pressed_button)
```

Exemple de fonction de rappel:

```python
def clicked_button(self):
    print("Cliqué !")
```

## 8.3. QML

Permet de construire l'interface en déclarant son contenu sous forme d'objets dans un fichier QML:

- Fichier principal de l'application python:

```python
#!/usr/bin/python3

import os
import sys
from PyQt5.QtCore import *
from PyQt5.QtGui import *
from PyQt5.QtQuick import *
from PyQt5.Qt import *

if __name__ == "__main__":
    app = QApplication(sys.argv)

    engine = QQmlApplicationEngine()
    engine.load(QUrl.fromLocalFile("main.qml"))

    sys.exit(app.exec_())
```

- Fichier QML:

```qml
import QtQuick 2.7
import QtQuick.Window 2.2
import QtQuick.Controls 1.4
import QtGraphicalEffects 1.0

ApplicationWindow {
    id: mainWindow
    height: 160
    width: 300
    visible: true
    title: "My Window"

    Item {
        id: page
        visible: true
        width: parent.width

        Rectangle {
            height: {
                console.log("I\'m a comment")
                return 160
            }
            width: parent.width

            color: "#ff0000"

            Text {
                text: "I am some regular text"
                height: 50
                width: parent.width
                font.pixelSize: 12
            }
        }
    }
}
```

