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

### Dokumentation manuelles Deployment

####  Ziel

Bereitstellung einer webbasierten Passwortmanager-Applikation (Vaultwarden) bestehend aus zwei Docker-Containern:

- **Vaultwarden** (Anwendung)
- **PostgreSQL** (Datenbank)

####  Vorbereitung

Alte Container, Volumes und Netzwerk wurden bereinigt:

```bash
docker stop vaultwarden vaultwarden-db
docker rm vaultwarden vaultwarden-db
docker network rm vaultwarden-net
docker volume rm vw-data vw-postgres-data
```

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
