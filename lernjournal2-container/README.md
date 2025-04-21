# Lernjournal 2 Container

### Verwendete Docker Images

|                          |                                                                 |
|--------------------------|-----------------------------------------------------------------|
| Image 1                  | vaultwarden/server:latest                                       |
| Image 1 – URL Docker Hub | https://hub.docker.com/r/vaultwarden/server                    |
| Image 2                  | postgres:15                                                    |
| Image 2 – URL Docker Hub | https://hub.docker.com/_/postgres                              |
| Docker Compose           | https://github.com/yanickfischer/Lernjournal2-Vaultwarden.git  |

---
## Docker Applikation manuell und mit Compose: Vaultwarden-PosgreSQL

### Dokumentation manuelles Deployment

**Ziel:** Bereitstellung einer webbasierten Passwortmanager-Applikation (Vaultwarden) bestehend aus zwei Docker-Containern:

- **Vaultwarden** (Anwendung)
- **PostgreSQL** (Datenbank)

####  Setup

Netzwerk erstellen
```bash
docker network create vaultwarden-net
```

Vaultwarden-Postgress Applikation erstellen und Logindaten für Admiinzugang setzen
```bash
docker run -d \
  --name vaultwarden-db \
  --network vaultwarden-net \
  -e POSTGRES_DB=vaultwarden \
  -e POSTGRES_USER=vwuser \
  -e POSTGRES_PASSWORD=vwpass \
  -v vw-postgres-data:/var/lib/postgresql/data \
  postgres:15
```
<img src="images/Vault_ManualSetup.png" alt="Setup CLI" style="max-width: 100%; height: auto;">

Applikation ausführen
```bash
docker run -d \
  --name vaultwarden \
  --network vaultwarden-net \
  -e DATABASE_URL=postgresql://vwuser:vwpass@vaultwarden-db/vaultwarden \
  -e ADMIN_TOKEN=supersecretadmin123 \
  -v vw-data:/data \
  -p 8080:80 \
  vaultwarden/server:latest
```
<img src="images/Vault1.png" alt="Adminkonsole lokal" style="max-width: 100%; height: auto;">

Login mit Secret

<img src="images/Vault2.png" alt="Adminkonsole nach Login" style="max-width: 100%; height: auto;">

### Dokumentation docker-compose.yml orchestrierte Methode

Die Vaultwarden-Applikation wurde nach dem manuellen Deployment nun mit Docker Compose als Mehrcontainer-Anwendung bereitgestellt. Dabei werden zwei Container (Vaultwarden + PostgreSQL) über eine zentrale `docker-compose.yml` orchestriert.

<img src="images/Vault_VsCodeCLI.png" alt="Compose erstellen" style="max-width: 100%; height: auto;">

Im Projektverzeichnis befindet sich die Datei im Odner "Vaultwarden-Compose"

```bash
docker-compose.yml
```
<img src="images/Vault_Compose_File.png" alt="Compose File" style="max-width: 100%; height: auto;">

Und auch hier kann die Applikation erfolgreich gestartet werden
<img src="images/Vault_Admin.png" alt="Adminkonsole lokal" style="max-width: 100%; height: auto;">

Hier noch die Ansicht der Diagnostics
<img src="images/Vault_Diagnostics.png" alt="Admin Diagnostics" style="max-width: 100%; height: auto;">

Zum Schluss fahren wir den Container wieder runter und beenden die Applikation
```bash
docker-compose down
```
<img src="images/Vault_down.png" alt="Applikation beenden" style="max-width: 100%; height: auto;">

## Deployment ML-App

### Variante und Repository

| Gewähltes Beispiel | Bitte ausfüllen |
| -------- | ------- |
| onnx-sentiment-analysis | Ja/Nein |
| onnx-image-classification | Ja/Nein |
| Repo URL Fork | URL |
| Docker Hub URL | URL |

### Dokumentation lokales Deployment

* [ ] TODO

### Dokumentation Deployment Azure Web App

* [ ] TODO

### Dokumentation Deployment ACA

* [ ] TODO

### Dokumentation Deployment ACI

* [ ] TODO
