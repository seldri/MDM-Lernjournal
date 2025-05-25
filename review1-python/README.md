# Review 1 Python

## Beurteiltes Projekt

|       | Bitte ausfüllen |
|-------|-----------------|
| Review von (ZHAW-Kürzel) |  maniyman          |
| Review durch (ZHAW-Kürzel) |  selimdri         |
| Datum Review, von/bis |  25.03.2025, 16:15-16:30    |

## Review

### Vorwort
Das Projekt befindet sich bereits in der Umsetzung und umfasst eine App zur Analyse und Vorhersage von Wechselkursen des Schweizer Frankens mithilfe von Zeitreihenanalysen mit dem Framework **Prophet** von Facebook.

## Zusammenfassung Review
Das Projekt verfolgt ein klar umrissenes Ziel: Wechselkurse des CHF sollen analysiert und prognostiziert werden. Die Daten werden einmalig als **CSV von OpenData.swiss** heruntergeladen, in **MongoDB Cloud** geladen und dann für die Prophet-Zeitreihenanalyse wieder in CSV umgewandelt. 

Hier haben wir kritisch hinterfragt, ob der doppelte Umweg über MongoDB und CSV tatsächlich notwendig ist. Die Analyse könnte effizienter gestaltet werden, wenn die Daten direkt in einem geeigneten Format für Prophet verarbeitet würden – z. B. direkt aus MongoDB mit passender Transformation.

Trotzdem ist das Projektziel nachvollziehbar und das Setup mit Prophet sehr interessant gewählt. Die Idee hat Potenzial und der Kollege ist technisch versiert. Die nächsten Schritte wären nun:
1. Vorverarbeitung der Daten optimieren
2. Prophet-Modell trainieren
3. Validierung mit Metriken und Testdaten
4. Ergebnisse im Frontend darstellen
5. Optional: Deployment der App

| Thema                                                                      | Skala | Mängel* | Verbesserungsmöglichkeiten* |
|----------------------------------------------------------------------------|-------|--------|----------------------------|
| Datenquelle klar definiert (Projekt 2: zusätzlich Abgrenzung zu Projekt 1) | 2     | —      | — |
| Scraping vorhanden                                                         | 0     | Daten nur einmalig heruntergeladen | Kein echtes Scraping nötig, daher nicht relevant |
| Scraping automatisiert                                                     | 0     | — | Nicht relevant, da keine laufende Erhebung geplant ist |
| Datensatz vorhanden                                                        | 2     | — | — |
| Erstellung Datensatz automatisiert, Verwendung Datenbank                   | 1     | Unklar, ob automatisiert | Direkte Integration in Prophet prüfen |
| Datensatz-Grösse ausreichend, Aufteilung Train/Test, Kennzahlen vorhanden  | 1     | Noch keine Metriken zur Vorhersagequalität sichtbar | Evaluation und Aufteilung einbauen |
| Modell vorhanden                                                           | 1     | Prophet initial eingebunden | Weitere Optimierung und Validierung nötig |
| Modell-Versionierung vorhanden (ModelOps)                                  | 0     | Nicht erwähnt | Könnte über Joblib oder ähnliches eingeführt werden |
| App: auf lokalem Rechner gestartet und funktional                          | 1     | Teilweise | Weitere Testcases hilfreich |
| App: mehrere unterschiedliche Testcases durch Reviewer ausführbar          | 0     | Noch keine Tests durchgeführt | Testdaten vorbereiten |
| Deployment: Falls bereits vorhanden, funktional und automatisiert          | 0     | Noch nicht durchgeführt | In späterem Schritt realisieren |
| Code: Git-Repository vorhanden, Arbeiten mit Branches / Commits            | 1     | Grundsätzlich vorhanden | Mehr strukturierte Branch-Strategie wünschenswert |
| Code: Dependency Management, Dockerfile, Build funktional                  | 0     | Noch nicht umgesetzt | Containerisierung mit Docker als nächster Schritt |

\* wenn fehlend: mögliche Schwierigkeiten und Lösungen besprechen

## Skala

| Skala |                 |
|-------|-----------------|
| 0     | fehlt           |
| 1     | mit Lücken      |
| 2     | alles vorhanden |
| 3     | übertroffen     |

## Hinweise

Der Projekt-Review fliesst nicht in die Beurteilung der Leistungsnachweise ein, soll aber dem Studierenden dazu dienen, bis zur Abgabe noch Verbesserungsmöglichkeiten zu erkennen. Der Review *des fremden Projektes* muss als Teil des *eigenen* Lernjournals abgegeben werden.
