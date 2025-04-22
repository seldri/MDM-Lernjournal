# Lernjournal 2 Container

### Verwendete Docker Images

|                          |                                                                 |
|--------------------------|-----------------------------------------------------------------|
| Image 1                  | vaultwarden/server:latest                                       |
| Image 1 – URL Docker Hub | https://hub.docker.com/r/vaultwarden/server                    |
| Image 2                  | postgres:15                                                    |
| Image 2 – URL Docker Hub | https://hub.docker.com/_/postgres                              |
| Docker Compose           | https://github.com/yanickfischer/mdm-lernjournal2-compose |

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

Das sehen wir sowohl in Docker...
<img src="images/Vault_Docker.png" alt="Docker Container" style="max-width: 100%; height: auto;">

als auch im localhost...
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
| onnx-sentiment-analysis | Nein |
| onnx-image-classification | Ja |
| Repo URL Fork | https://github.com/yanickfischer/onnx-image-classification|
| Docker Hub URL | https://hub.docker.com/repository/docker/yanickpfischer/onnx-image-classification |

### Dokumentation lokales Deployment
Nun geht es an den zweiten Teil des Lernjournals.
Hier soll ich Entweder die onnx-sentiment-analysis oder onnx-image-classification lokal in Docker und auf Azure zum Laufen bringen.
Dabei bin ich wie folgt vorgegangen:

1. Fork von https://github.com/mosazhaw/onnx-image-classification erstellt, verfügbar unter https://github.com/yanickfischer/onnx-image-classification
2. Forked Repository genutzt um einen lokalen Clone im VsCode zu erstellen
3. Via VsCode CLI den Docker build durchführen
```bash
docker build -t onnx-image-classification .
docker run --name onnx-image-classification -p 9000:5000 -d onnx-image-classification
```
<img src="images/onnx_dockerbuild.png" alt="Build Container" style="max-width: 100%; height: auto;">

4. Docker Image wurde erstellt
   
<img src="images/onnx_docker.png" alt="Docker1" style="max-width: 100%; height: auto;">
<img src="images/onnx_docker2.png" alt="Docker2" style="max-width: 100%; height: auto;">

6. Test der Docker Applikation im localhost mit einem eigenen Bild eines Roboters
```bash
 python onxx-sentiment-app/export_to_onnx.py
```
<img src="images/onnx_localhost.png" alt="Onnx Localhost" style="max-width: 100%; height: auto;">

6. Docker Image taggen
```bash
docker tag onnx-image-classification yanickpfischer/onnx-image-classification:latest
```
<img src="images/docker_tag.png" alt="Docker tag" style="max-width: 100%; height: auto;">

7. Image auf Docker Hub publishen
```bash
docker push yanickpfischer/onnx-image-classification:latest.
```
<img src="images/docker_Push.png" alt="Docker Hub Push" style="max-width: 100%; height: auto;">

8. Das Image wurde erfolgreich auf Docker Hub published
<img src="images/docker_hub.png" alt="Publich Hub image" style="max-width: 100%; height: auto;">

### Dokumentation Deployment Azure Web App

Diese Form von Deployment funktioniert bei mir ohne Probleme.

1. Ressourcengruppe erstellen
```bash
az group create --name mdm-lj2-rg --location westeurope
```

2. App Service Plan erstellen
```bash
az appservice plan create \
  --name mdm-lj2-plan \
  --resource-group mdm-lj2-rg \
  --sku F1 \
  --is-linux
```
3. Web App mit Docker Image erstellen
```bash
az webapp create \
  --resource-group mdm-lj2-rg \
  --plan mdm-lj2-plan \
  --name mdm-lj2-app \
  --deployment-container-image-name yanickpfischer/onnx-image-classification:latest
```
Das Deployment hat funktioniert.
Es wurden alle Ressourcen erstellt...

Die App Overview sieht gut aus...

Und die App läuft auch wirklich...

### Dokumentation Deployment ACA

**Diese Form von Deployment funktioniert nicht aufgrund von Problemen mit den Subscriptions in Azure**

1. Ressourcengruppe erstellen
```bash
az group create --location westeurope --name mdm-lj2-aca
```
2. Container App Environment erstellen - Schritt funktioniert nicht wegen Subscription issue
```bash
az containerapp env create \
  --name mdm-lj2-onnx-image-classification-env \
  --resource-group mdm-lj2-aca \
  --location westeurope
```
3. Container App erstellen - funktioniert nicht weil vorheriger Schritt schon fehlschlägt
```bash
az containerapp create \
  --name mdm-lj2-onnx-image-classification-app \
  --resource-group mdm-lj2-aca \
  --environment mdm-lj2-onnx-image-classification-env \
  --image yanickpfischer/onnx-image-classification:latest \
  --target-port 80 \
  --ingress external \
  --query properties.configuration.ingress.fqdn
```

### Dokumentation Deployment ACI

**Diese Form von Deployment funktioniert nicht aufgrund von Problemen mit den Subscriptions in Azure**

1. Ressourcengruppe erstellen
```bash
az group create --location westeurope --name mdm-lj2-aci
```

2. Container Instanz erstellen - Schritt funktioniert nicht wegen Subscription issue
```bash
az container create \
  --resource-group mdm-lj2-aci \
  --name mdm-lj2-onnx-image-classification-instance \
  --image yanickpfischer/onnx-image-classification:latest \
  --dns-name-label mdm-lj2-onnx-image-classification-instance \
  --ports 80
```
