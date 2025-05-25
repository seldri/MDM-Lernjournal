# Lernjournal 4 ONNX

## Übersicht

| | Beschreibung |
| -------- | ------- |
| ONNX Modell für Analyse (Netron) | [mobilenetv3-small.onnx Analyse](https://netron.app/) |
| Modellklassifikation mit Skript | [Projekt auf GitHub](https://github.com/seldri/models) |

## Dokumentation ONNX Analyse

Zu Beginn des Lernjournals stand das Ziel, die ONNX Runtime kennenzulernen und ein vortrainiertes Modell zu analysieren sowie anzuwenden. Ich habe mich für das Modell **mobilenetv3-small.onnx** entschieden, das im ONNX Model Zoo verfügbar ist und ein leichtgewichtiges Modell für Bildklassifikation darstellt.

### Einsatz des Netron Viewers

Mit dem **Netron Viewer** konnte ich das Modell im Detail untersuchen:

- **Input-Shape:** `[1, 3, 224, 224]`
- **Struktur:** Convolutional Layers, Batch Normalization, Activation, Global Average Pooling
- **Ausgabe:** Klassifikation über 1000 Klassen via Softmax

Die Visualisierung der Architektur half mir zu verstehen, wie das Modell die Eingaben verarbeitet und welche Formate für das Preprocessing nötig sind.

---

## Ziele

- Konzept von ONNX verstehen
- Modellstruktur mit Netron analysieren
- ONNX Runtime praktisch anwenden
- Eingabeformat korrekt vorbereiten
- Modellklassifikation lokal durchführen
- Ergebnisse und Code dokumentieren

---

## 1. Vorbereitung und Modellauswahl

Verwendetes Modell:
- `mobilenetv3-small.onnx` aus dem GitHub-Repo [seldri/models](https://github.com/seldri/models)

---

## 2. Klassifikationsskript

Ein einfaches Python-Skript (`classify.py`) wurde geschrieben, um ein Beispielbild zu laden, zu verarbeiten und mit dem Modell zu klassifizieren.

```bash
python classify.py
```

---

## 3. Vergleich der Klassifikation

Hier wurden drei Beispielbilder verwendet, um die Vorhersagen zu vergleichen. Diese stammen aus der Testreihe mit dem mobilenetv3-Modell:

### Beispielbilder
- Bild 1: `Bild1.jpg` – Top-Klasse: ...
- Bild 2: `Bild2.jpg` – Top-Klasse: ...
- Bild 3: `Bild3.jpg` – Top-Klasse: ...

*Screenshots der Konsole und Netron-Visualisierung liegen vor.*

---

## 4. Codeanpassung

Der Input des Modells ist im Format `[1, 3, 224, 224]` (NCHW), daher wurde das Bild wie folgt vorbereitet:

- Resize auf 224x224
- Normierung der Pixelwerte
- Umwandlung von HWC → CHW → NCHW mit `transpose` und `expand_dims`

---

## 5. Fazit

- Die Anwendung der ONNX Runtime war einfach umzusetzen.
- Die Analyse mit Netron war entscheidend für die korrekte Eingabeform.
- MobilenetV3 bietet eine gute Performance bei geringem Ressourcenverbrauch.
- Der Vergleich mehrerer Bilder zeigte stabile Vorhersagen.
- Das Klassifikationsskript kann für weitere Modelle leicht angepasst werden.

---

## 6. Quellcode

Der vollständige Code ist im GitHub-Repository verfügbar:  
[https://github.com/seldri/models](https://github.com/seldri/models)

---

## 7. Quellen

- ONNX Model Zoo: https://github.com/onnx/models  
- Netron Viewer: https://netron.app  
- ONNX Runtime: https://onnxruntime.ai
