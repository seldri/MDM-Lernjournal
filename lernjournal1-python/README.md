# Lernjournal 1 Python

## Repository und Library

| | Bitte ausfüllen |
| -------- | ------- |
| Repository (URL)  | https://github.com/yanickfischer/SW1_TextManipulation.git
| Kurze Beschreibung der App-Funktion | To-Do-Liste mit Text-Manipulation |
| Verwendete Library aus PyPi (Name) | textblob, nltk, flask, gunicorn |
| Verwendete Library aus PyPi (URL) | [https://pypi.org/project/textblob/](https://pypi.org/project/textblob/, https://pypi.org/project/nltk/, https://pypi.org/project/Flask/, https://pypi.org/project/gunicorn/)|
| ... | |
| ... | |

## App, Funktionalität
Die Applikation bietet dem User die Möglichkeit Aufgaben in einer To-Do-Liste zu erfassen und zeigt Informationen zur gemachten Texteingabe an.

#### Ansicht im Web-UI:
!!!!!
ERGàNZEN!!!!

### Funktionen Aufgaben bearbeiten
Der User kann eine neue Aufgabe hinzufügen oder diese auch wieder löschen.

#### Ansicht im Web-UI:

<img width="1360" alt="Screenshot 2025-03-17 at 12 16 38" src="https://github.com/user-attachments/assets/9a8971b8-146b-4948-902d-eb6cad1d2080" />

#### Code der Applikation:

<img width="703" alt="Screenshot 2025-03-18 at 10 16 50" src="https://github.com/user-attachments/assets/07fd8653-a57b-40c2-9a1a-740d83fa6027" />

### Trigger Text Informationen
Bei der Eingabe durch den User und mit dem Trigger des Buttons "Add Task" wird zudem eine Operation durchgeführt, welche den Text untersucht und folgende Informationen zur eingabe anzeigt:
-Originaleingabe
-Umkehrung des Textes
-Anzahl der Wörter
-Anzahl der Buchstaben (Char)
-Palindrome*

*https://de.wikipedia.org/wiki/Palindrom 

#### Ansicht Web-UI:

<img width="311" alt="Screenshot 2025-03-17 at 12 15 30" src="https://github.com/user-attachments/assets/d2b731eb-e0ba-4b27-953f-cc209644e955" />

#### Code der Application:

<img width="644" alt="Screenshot 2025-03-18 at 10 17 03" src="https://github.com/user-attachments/assets/6070e012-2f89-45a1-a10e-24736576f592" />


## Dependency Management

Nach der Entwicklung der Applikation wurden die Dependencies mit folgendem Prozess generiert:

1. pip freeze > reqruirements.in
2. pip-compile requirements.in

Entsprechend stehen im Projekt die Dependencies zur Verfügung.

### requirements.in Inhalt:

<img width="437" alt="Screenshot 2025-03-17 at 12 02 54" src="https://github.com/user-attachments/assets/6489849e-5ae1-4e17-95e3-34aca4c71661" />

### requirements.txt Inhalt (Teil-Auszug):

<img width="511" alt="Screenshot 2025-03-17 at 12 03 07" src="https://github.com/user-attachments/assets/76c5e18c-9776-4956-b922-2a76b5a091c3" />


## Deployment

Für das Deployment der Webapplikation wurde Microsoft Azure verwendet.
Das lokal entwickelte Flask-Projekt wird ZIP-Datei auf einen Azure App Service deploye und steht somit der Öffentlichkeit zur Verfügung.
Nachfolgend die vorgenommenen Schritte zum Deployment mit Azure.

**1. Projekt vorbereiten (ZIP-Archiv erstellen)** 
Zuerst wurde das Projekt als ZIP-Datei verpackt, wobei temporäre Dateien (z.B. .venv) ausgeschlossen wurden: zip -r deployment.zip . -x "*.venv*" "*.git*" "__pycache__/*"

**2. Azure Ressource anlegen**
Es wurde eine neue Ressourcengruppe, ein App Service Plan und eine Web-App mit Python Runtime erstellt. Dabei wurde die Version Python 3.13 gewählt und ein frei wählbarer App-Name vergeben:


