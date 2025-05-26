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

Die Projektstruktur ist auf folgendem Screenshot zu sehen:

![Projektstruktur](images/Bild1.png)

---

## 3. Lokales Deployment (ohne Docker)

Die Anwendung kann direkt lokal gestartet werden, nachdem alle Abhängigkeiten installiert wurden.  
Dies ist ideal für die schnelle Entwicklung und das Testen der App.

```bash
python app.py
```

Die Anwendung läuft daraufhin lokal unter: http://127.0.0.1:5000

![Projektstruktur](images/Container1.png)
---

