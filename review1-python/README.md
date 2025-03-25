# Review 1 Python

## Beurteiltes Projekt

|       | Bitte ausfüllen |
|-------|-----------------|
| Review von (ZHAW-Kürzel) |  selimalb          |
| Review durch (ZHAW-Kürzel) |  fischya3         |
| Datum Review, von/bis |  25.03.2025, 16:15-16:30    |

## Review

### Vorwort
Das vorgestellte Projekt ist nur im konezptionellen Zustand. Entsprechend können die meisten Punkte in der Tabelle nicht spezifisch reviewed werden, weshalb hier die Zusammenfassung in Fliesstext gemacht wurde:

## Zusammenfassung Review
Aufgrund der verbleibenden Zeit, Empfehlung der Reviewer mal zuerst eine API Anbindung zu machen und Daten auf diesem Weg zu holen. Da der Stand des Projektes wirklich aktuell eigentlich noch nicht umgesetzt ist und nur konzeptionell eine Idee besteht, haben wir als Reviewer die konzeptionelle Idee mit dem Reviewten besprochen und ihm Tipps zur Umsetzung gegeben. Wir haben vorgeschlagen das folgende Schritte unternommen werden: 
1. API statt Scraping
2. Datensource erschliessen und ersten Datensatz auslesen
3. Mongo DB anbinden und Datensatz in Collection speichern
4. Zentrale Fragestellung "Wie wahrscheinlich ist das Basketball Team A gegen Team B gewinnt" mit einem Modell predicten
5. Frontend entwickeln
6. Falls genügend Zeit, API durch Scraping ersetzen
7. Deployen + Automatisieren

-> Beim Einhalten dieser Vorschläge, sollte eine Fertigstellung mit den begrenzten zeitlichen Ressourcen noch möglich sein. 

| Thema                                                                      | Skala | Mängel* | Verbesserungsmöglichkeiten* |
|----------------------------------------------------------------------------|-------|--------|----------------------------|
| Datenquelle klar definiert (Projekt 2: zusätzlich Abgrenzung zu Projekt 1) | 1  | Datenquelle noch nicht mit Scraping / API ausprobiert  | Bei Entscheidung für API die Quelle nutzen, die eine API bietet. Falls Scraping ist es die bisherige Datenquelle, da einfach noch unklar ob es funktioniert.                       |
| Scraping vorhanden                                                         | 0 | bisher nicht umgesetzt | Falls die Zeit knapp wird lieber mit API starten und wenn Zeit noch da, später auf Scraping entwickeln                  |
| Scraping automatisiert                                                     | 0 | bisher nicht umgesetzt | durch Reviewten noch zu erstellen|
| Datensatz vorhanden                                                        | 0 | bisher nicht umgesetzt | durch Reviewten noch zu erstellen|
| Erstellung Datensatz automatisiert, Verwendung Datenbank                   | 0 | bisher nicht umgesetzt | durch Reviewten noch zu erstellen|
| Datensatz-Grösse ausreichend, Aufteilung Train/Test, Kennzahlen vorhanden  | 0 | bisher nicht umgesetzt | durch Reviewten noch zu erstellen|
| Modell vorhanden                                                           | 0 | bisher nicht umgesetzt | durch Reviewten noch zu erstellen|
| Modell-Versionierung vorhanden (ModelOps)                                  | 0 | bisher nicht umgesetzt | durch Reviewten noch zu erstellen|
| App: auf lokalem Rechner gestartet und funktional                          | 0 | bisher nicht umgesetzt | durch Reviewten noch zu erstellen|
| App: mehrere unterschiedliche Testcases durch Reviewer ausführbar          | 0 | bisher nicht umgesetzt | durch Reviewten noch zu erstellen|
| Deployment: Falls bereits vorhanden, funktional und automatisiert          | 0 | bisher nicht umgesetzt | durch Reviewten noch zu erstellen|
| Code: Git-Repository vorhanden, Arbeiten mit Branches / Commits            | 0 | bisher nicht umgesetzt | durch Reviewten noch zu erstellen|
| Code: Dependency Management, Dockerfile, Build funktional                  | 0 | bisher nicht umgesetzt | durch Reviewten noch zu erstellen|

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
