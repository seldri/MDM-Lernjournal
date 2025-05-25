# Review 2 Java
## Beurteiltes Projekt
|       | Bitte ausfüllen |
|-------|-----------------|
| Review von (ZHAW-Kürzel) | etemizab |
| Review durch (ZHAW-Kürzel) | selimdri |
| Datum Review, von/bis | 15.05.2025, 16:15 - 16:30 |
## Review
| Thema                                                                      | Skala | Mängel* | Verbesserungsmöglichkeiten* |
|----------------------------------------------------------------------------|-------|--------|----------------------------|
| Datenquelle klar definiert (Projekt 2: zusätzlich Abgrenzung zu Projekt 1) | 3     | keine   | Datenquelle ist klar definiert und sinnvoll abgegrenzt |
| (Datensatz vorhanden)                                                      | 3     | keine   | Der Bilddatensatz ist sehr umfangreich und passend für Bildklassifikation |
| (Datensatz-Grösse ausreichend, Aufteilung Train/Test, Kennzahlen vorhanden) | 1     | Aufteilung noch nicht umgesetzt | Trainings-/Test-Split noch vornehmen, evtl. Kennzahlen für spätere Evaluation definieren |
| Modell vorhanden                                                           | 1     | DJL-Modellkonzept steht, Modell aber noch nicht integriert | Klassifikationsmodell über DJL ist geplant, Anbindung an Java Spring Boot noch ausstehend |
| App: auf lokalem Rechner gestartet und funktional                          | 1     | Backend steht, Frontend in Arbeit | Upload-Formular und Verbindung zum Backend noch implementieren |
| App: mehrere unterschiedliche Testcases durch Reviewer ausführbar          | 0     | noch keine Testmöglichkeiten | Sobald Upload funktioniert, sollten erste Testfälle definiert und geprüft werden |
| Deployment: Falls bereits vorhanden, funktional und automatisiert          | 0     | Deployment noch nicht vorhanden | Geplant ist ein Deployment via Docker und Azure – frühzeitig Image und Build-Prozess testen |
| Code: Git-Repository vorhanden, Arbeiten mit Branches / Commits            | 2     | keine | GitHub-Repository ist vorhanden und wird regelmässig gepflegt – Branch-Konzept kann später noch optimiert werden |
| Code: Dependency Management, Dockerfile, Build funktional                  | 1     | Maven-Projektstruktur steht | Dockerfile in Planung – Build-Prozess lokal funktionsfähig, Containerisierung noch offen |
\* wenn fehlend: mögliche Schwierigkeiten und Lösungen besprechen
## Skala
| Skala |                 |
|-------|-----------------|
| 0     | fehlt           |
| 1     | mit Lücken      |
| 2     | alles vorhanden |
| 3     | übertroffen     |
## Hinweise
Das Projekt ist vielversprechend gestartet. Die Datenquelle ist klar definiert und der Datensatz umfangreich und sehr gut geeignet für Bildklassifikation mit DJL. Die Architektur mit Java Spring Boot Backend und Web-Frontend ist sinnvoll und gut durchdacht.
 
Aktuell liegt der Fokus auf der Integration des Klassifikationsmodells und der Verknüpfung von Frontend und Backend für den Bild-Upload. Das Frontend-Grundgerüst wurde erstellt und erste API-Endpunkte sind vorbereitet. Für die nächsten Schritte empfehle ich: Upload-Funktionalität fertigstellen, DJL-Modell einbinden, erste Testfälle definieren und im Anschluss die Dockerisierung vorbereiten. Ein Azure Deployment ist geplant und sollte möglichst früh getestet werden, um Kompatibilitätsprobleme zu vermeiden.
 
Der aktuelle Stand ist für diese Projektphase absolut im Soll und sehr gut dokumentiert.
