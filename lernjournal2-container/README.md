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

**Azure Application URL = https://mdm-lj2-app.azurewebsites.net/**

Diese Form von Deployment funktioniert bei mir ohne Probleme.

1. Ressourcengruppe erstellen
```bash
az group create --name mdm-lj2-rg --location westeurope
```
<img src="images/az_appservice1.png" alt="App Service – Ressourcengruppe erstellt" style="max-width: 100%; height: auto;">

2. App Service Plan erstellen
```bash
az appservice plan create \
  --name mdm-lj2-plan \
  --resource-group mdm-lj2-rg \
  --sku F1 \
  --is-linux
```
<img src="images/az_appservice2.png" alt="App Service Plan erstellt" style="max-width: 100%; height: auto;">

3. Web App mit Docker Image erstellen
```bash
az webapp create \
  --resource-group mdm-lj2-rg \
  --plan mdm-lj2-plan \
  --name mdm-lj2-app \
  --deployment-container-image-name yanickpfischer/onnx-image-classification:latest
```
<img src="images/az_appservice3.png" alt="App Deployment läuft" style="max-width: 100%; height: auto;">

Das Deployment hat funktioniert.

Es wurden alle Ressourcen erstellt...
<img src="images/az_appservice4.png" alt="App im Browser aufrufbar" style="max-width: 100%; height: auto;">

Die App Overview sieht gut aus...

Und die App läuft auch wirklich...
<img src="images/az_appservice5.png" alt="App Übersicht in Azure Portal" style="max-width: 100%; height: auto;">

### Dokumentation Deployment ACA

**Azure Application URL = https://mdm2-imgclass.proudriver-dbeeb7ad.westeurope.azurecontainerapps.io/**

Nach einigem Krampf und Rumspielen mit Subscriptions und Commands, konnte ich auch mit ACA deployen...

1. Ressourcengruppe erstellen
```bash
az group create --location westeurope --name mdm-lj2-aca
```
<img src="images/az_aca0.png" alt="RG created" style="max-width: 100%; height: auto;">

2. Container App Environment erstellen
```bash
az containerapp env create \
  --name mdm2-imgclass-env \
  --resource-group mdm-lj2-aca \
  --location westeurope
```
<img src="images/az_aca1.png" alt="Fehler beim ACA-Environment wegen fehlendem Log Analytics" style="max-width: 100%; height: auto;">

3. Durch zusätzliche Eingabe dieses Command konnte die Fehlermeldung behoben werden und das Environment wurde erstellt  
```bash
az provider register -n Microsoft.OperationalInsights --wait
```
<img src="images/az_aca3.png" alt="Env ready" style="max-width: 100%; height: auto;">

4. Container App erstellen
```bash
az containerapp create \
  --name mdm2-imgclass \
  --resource-group mdm-lj2-aca \
  --environment mdm2-imgclass-env \
  --image yanickpfischer/onnx-image-classification:latest \
  --target-port 80 \
  --ingress external \
  --query properties.configuration.ingress.fqdn
```
<img src="images/az_aca4.png" alt="Container OK" style="max-width: 100%; height: auto;">

Und das alles funktioniert hat, sehen wir auch hier in der App direkt...
<img src="images/az_aca5.png" alt="App live" style="max-width: 100%; height: auto;">

### Dokumentation Deployment ACI

**Azure Application URL = http://mdm2imgclass.westeurope.azurecontainer.io/** 

Nach einigem Krampf und Rumspielen mit Subscriptions, Commands und Betreuung durch Chat GPT, konnte ich auch mit ACI **aber mit zusätzlicher Verwendung von ACR** deployen...

1. Ressourcengruppe erstellen - funktioniert problemlos wie gewohnt
```bash
az group create --location westeurope --name mdm-lj2-aci
```
<img src="images/az_aci.png" alt="Fehler beim ACI-Deployment wegen nicht registrierter Subscription" style="max-width: 100%; height: auto;">

2. Container Instanz erstellen - funktioniert leider mit mehreren Versuchen nicht mit diesem Command oder Troubleshooting-Vorschlägen von Chat-GPT 4o
**aber ich geb nach Rücksprache mit Adrian Moser doch nicht auf**
```bash
az container create \
  --resource-group mdm-lj2-aci \
  --name mdm-lj2-onnx-image-classification-instance \
  --image yanickpfischer/onnx-image-classification:latest \
  --dns-name-label mdm-lj2-onnx-image-classification-instance \
  --ports 80
```
<img src="images/az_aci1.png" alt="ACI errors" style="max-width: 100%; height: auto;">

Weil das Problem auch nach warten und diversen Versuchen noch bestehen blieb, habe ich ChatGPT konsultiert.
GPT empfiehlt 3 Optionen, von denen die ersten beiden fehlschlagen...

*Option 1: Später erneut probieren -> **funktioniert leider nicht (wie schon oben im Bild gesehen)**
*Option 2: Workaround über neuen Tag (deutsch = Kennzeichnung) -> **funktioniert leider nicht**
<img src="images/az_aci_retag.png" alt="Image re-tag" style="max-width: 100%; height: auto;">

*Option 3: Azure Container Registry (ACR) verwenden (empfohlen, wenn’s zuverlässig sein soll) -> somit ist das *hoffentlich* die Lösung...

1. ACR Registry erstellen, um darin dann das Docker-Image abzulegen
```bash
az acr create \
  --resource-group mdm-lj2-aci \
  --name lj2registry \
  --sku Basic \
  --location westeurope
```
<img src="images/az_aci_acr1.png" alt="ACR created" style="max-width: 100%; height: auto;">

2. ACR login und Tagen der images
```bash
az acr login --name lj2registry
docker tag yanickpfischer/onnx-image-classification:v2 lj2registry.azurecr.io/onnx-image-classification:v2
```
<img src="images/az_aci_acr2.png" alt="ACR login & push" style="max-width: 100%; height: auto;">

3. Push des Docker Images (siehe Bild oben)
```bash
docker push lj2registry.azurecr.io/onnx-image-classification:v2
```

3. Versuch Container zu erstellen - schlägt fehl "Please specify --registry-username in order to use custom image registry."

Dieses Bild zeigt Schritt 3, 4 + 5...
<img src="images/az_aci_acr3.png" alt="ACR enabled admin" style="max-width: 100%; height: auto;">

```bash
az container create \
  --resource-group mdm-lj2-aci \
  --name mdm2imgclass \
  --image lj2registry.azurecr.io/onnx-image-classification:v2 \
  --dns-name-label mdm2imgclass \
  --ports 80 \
  --os-type Linux \
  --cpu 1 \
  --memory 1.5 \
  --registry-login-server lj2registry.azurecr.io
```
4. Versuch Credentials anzuzeigen - schlägt fehl
```bash
az acr credential show --name lj2registry
```
5. Admin Enablen auf dem Verzeichnis
```bash
az acr update -n lj2registry --admin-enabled true
```
6. Credentials erneut anzeigen
```bash
az acr credential show --name lj2registry
```
Hier sind die Passwörter bewusst geschwärzt, ich nutze den value von password für den nächsten Schritt
<img src="images/az_aci_acr4.png" alt="ACI registry error" style="max-width: 100%; height: auto;">

7. Container erneut erstellen mit geholtem passwort
```bash
az container create \
  --resource-group mdm-lj2-aci \
  --name mdm2imgclass \
  --image lj2registry.azurecr.io/onnx-image-classification:v2 \
  --dns-name-label mdm2imgclass \
  --ports 80 \
  --os-type Linux \
  --cpu 1 \
  --memory 1.5 \
  --registry-login-server lj2registry.azurecr.io \
  --registry-username lj2registry \
  --registry-password HIER_STEHT_DAS_PASSWORTx
```
<img src="images/az_aci_acr5.png" alt="ACI auth added" style="max-width: 100%; height: auto;">

8. Entlich Efolg! Der Container läuft! :D 
<img src="images/az_aci_acr6.png" alt="ACI running" style="max-width: 100%; height: auto;">

und die Applikation funktioniert auch wirklich...
<img src="images/az_aci_acr7.png" alt="ACI web UI" style="max-width: 100%; height: auto;">

Hier sehen wir noch die "ACR" Ressourcen die gebraucht werden...
<img src="images/az_aci_acr8.png" alt="ACI overview portal" style="max-width: 100%; height: auto;">

