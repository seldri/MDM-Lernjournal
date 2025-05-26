# Lernjournal 4 ONNX (Lite0)

## Übersicht

| | Beschreibung |
| -------- | ------- |
| Modellklassifikation mit App | [Projekt auf GitHub](https://github.com/seldri/models) |
| Applikations-Repo | https://github.com/seldri/onnx-image-classification.git |

---

## 1. Ziel und Setup

Ziel war es, ein kleineres ONNX-Modell (**EfficientNet-Lite0**) für Bildklassifikation lokal zu betreiben.  
Im ersten Schritt wurde **kein Dockerfile** verwendet – die App wurde direkt über Python gestartet.

```bash
pip install -r requirements.txt
python app.py
```

---

## 2. Projektstruktur

Das Projekt besteht aus folgenden Dateien und Ordnern:

- `app.py` – Hauptskript mit der Flask-Anwendung, die das ONNX-Modell lädt und Bilder klassifiziert
- `efficientnet_lite0.onnx` – Das kleinere ONNX-Modell für Bildklassifikation (EfficientNet-Lite0)
- `labels_map.txt` – JSON-Datei mit den Klassennamen für die Modellvorhersagen
- `requirements.txt` – Liste aller benötigten Python-Bibliotheken (z. B. Flask, onnxruntime, numpy, opencv)
- `templates/index.html` – Das HTML-Frontend der Webanwendung (Upload-Button, Anzeige der Vorhersage)
- `uploads/test_images/` – Ordner mit Beispielbildern für Testzwecke

![Projektstruktur](images/Bild1.png)

---

## 3. Lokales Deployment (ohne Docker)

Die Anwendung kann direkt lokal gestartet werden, nachdem alle Abhängigkeiten installiert wurden.  
Dies ist ideal für die schnelle Entwicklung und das Testen der App.

```bash
python app.py
```

Die Anwendung läuft daraufhin lokal unter:  
**http://127.0.0.1:5000**

![Lokaler Start über Python](images/Container1.png)

---

## 4. Container Build mit Dockerfile

Im nächsten Schritt wurde ein `Dockerfile` erstellt, um die Applikation in einem Container zu betreiben.  
Dies ermöglicht eine einfache und konsistente Ausführung auf jedem System mit Docker.

### Dockerfile-Inhalt

```dockerfile
# Basis-Image mit Python
FROM python:3.13.0

# Arbeitsverzeichnis im Container
WORKDIR /usr/src/app

# Kopiere Projektdateien in den Container
COPY app.py *.onnx labels_map.txt requirements.txt ./
COPY templates templates
COPY uploads uploads

# Installiere Abhängigkeiten
RUN apt-get update && apt-get install -y libgl1
RUN pip install --no-cache-dir -r requirements.txt

# Flask-App starten
EXPOSE 5000
CMD ["python", "-m", "flask", "run", "--host=0.0.0.0"]
```

### Build-Befehl

```bash
docker build -t onnx-image-classifier:local .
```

![Docker Build](images/Container2.png)

---

## 5. Docker-Container lokal starten

Der erstellte Container wurde danach gestartet:

```bash
docker run -p 5001:5000 --name onnx-classifier onnx-image-classifier:local
```

Die Anwendung war danach unter  
**http://127.0.0.1:5001**  
im Browser erreichbar.

![Docker-Run erfolgreich](images/Container5.png)

---

## 6. Container-Status und Logs in Docker Desktop

Die Container-Übersicht sowie Logs wurden über Docker Desktop überprüft.  
Dies zeigt, dass das Image erfolgreich ausgeführt wird:

Container Status:
![Docker Desktop Übersicht](images/Container3.png)  

Container Logs:
![Docker Desktop Logs](images/Container4.png)

---
