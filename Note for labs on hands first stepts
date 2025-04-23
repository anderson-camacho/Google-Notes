# Notas del Laboratorio: Get Started with Cloud Shell, GCP Essentials (GSP002)

## ⏱ Duración
- 45 minutos

## 🌐 Nivel
- Introductorio

## 💼 Requisitos previos
- Conocimiento básico de editores de texto en Linux: `vim`, `emacs`, `nano`

## 🌐 Recursos necesarios
- Navegador web (preferiblemente Google Chrome en modo Incógnito)
- Acceso a internet

---

## 📅 Estructura del Laboratorio

### Tareas:
1. Configuración del entorno
2. Filtrado de salidas en línea de comandos
3. Conexión a instancia de VM
4. Actualización del firewall
5. Visualización de logs
6. Evaluación de comprensión

---

## ✨ Descripción General
Google Cloud Shell es una máquina virtual basada en Debian que ofrece acceso a la línea de comandos para administrar recursos de Google Cloud. Incluye herramientas como `gcloud` preinstaladas y 5 GB de almacenamiento persistente.

Este laboratorio enseña a usar `gcloud` para gestionar recursos en GCP y conectarse a instancias de cómputo.

---

## ⚖️ Configuración Inicial

### Activar Cloud Shell:
1. Hacer clic en el icono de Cloud Shell.
2. Autorizar el uso de credenciales.
3. Verificar el `PROJECT_ID` con:
```bash
gcloud config list project
```
4. Verificar la cuenta activa:
```bash
gcloud auth list
```

### Establecer Zona y Región:
```bash
gcloud config set compute/region REGION

gcloud config set compute/zone ZONE
```

### Variables de entorno:
```bash
export PROJECT_ID=$(gcloud config get-value project)
export ZONE=$(gcloud config get-value compute/zone)
echo -e "PROJECT ID: $PROJECT_ID\nZONE: $ZONE"
```

---

## 🚀 Crear VM con gcloud
```bash
gcloud compute instances create gcelab2 --machine-type e2-medium --zone $ZONE
```
Verificar con:
```bash
gcloud compute instances list
```

---

## 🔍 Filtrar salidas con gcloud
```bash
gcloud compute instances list --filter="name=('gcelab2')"
gcloud compute firewall-rules list --filter="network='default'"
gcloud compute firewall-rules list --filter="NETWORK:'default' AND ALLOW:'icmp'"
```

---

## ✉️ Conectarse a la VM
```bash
gcloud compute ssh gcelab2 --zone $ZONE
```
Instalar nginx:
```bash
sudo apt install -y nginx
```
Salir de la VM:
```bash
exit
```

---

## ⚡ Actualización del Firewall
1. Agregar tags a la instancia:
```bash
gcloud compute instances add-tags gcelab2 --tags http-server,https-server
```
2. Crear regla de firewall:
```bash
gcloud compute firewall-rules create default-allow-http \
--direction=INGRESS --priority=1000 --network=default \
--action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 \
--target-tags=http-server
```
3. Verificar acceso:
```bash
curl http://$(gcloud compute instances list --filter=name:gcelab2 --format='value(EXTERNAL_IP)')
```

---

## 📃 Ver logs del sistema
Listar logs disponibles:
```bash
gcloud logging logs list
gcloud logging logs list --filter="compute"
```
Ver logs para una VM:
```bash
gcloud logging read "resource.type=gce_instance" --limit 5
gcloud logging read "resource.type=gce_instance AND labels.instance_name='gcelab2'" --limit 5
```

---

## 🎓 Evaluación Final
Tres formas básicas de interactuar con GCP:
- Interfaz de línea de comandos (`gcloud`)
- Consola de Google Cloud
- Librerías cliente

---

## 🔗 Referencias
- [Documentación de Cloud Shell](https://cloud.google.com/shell/docs)
- [Documentación de gcloud CLI](https://cloud.google.com/sdk/gcloud)

---

## © Derechos
- Manual actualizado: 12 de marzo de 2025  
- Probado por última vez: 12 de marzo de 2025  
- Copyright 2025 Google LLC

