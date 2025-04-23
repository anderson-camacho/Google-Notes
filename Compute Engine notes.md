# 🧠 Resumen General

Google Cloud Compute Engine (GCE) permite la creación y gestión de máquinas virtuales (VMs) en la infraestructura de Google. Ofrece flexibilidad en la configuración de recursos, opciones de escalado automático para adaptarse a la demanda y alternativas de bajo costo como las instancias preemptibles. Estas características facilitan el despliegue de aplicaciones robustas y eficientes en la nube.

---

# ☁️ Google Cloud Compute Engine (GCE)

## ¿Qué es GCE?

GCE es un servicio de infraestructura como servicio (IaaS) que permite crear y administrar VMs en la infraestructura de Google. Estas VMs pueden ejecutar diversos sistemas operativos, como Debian, Ubuntu, Red Hat, SUSE y Windows Server.

## Características Principales

- **Flexibilidad**: Configura VMs con diferentes cantidades de CPU, memoria y almacenamiento según tus necesidades.
- **Variedad de sistemas operativos**: Linux (Debian, Ubuntu, SUSE, Red Hat, CoreOS) y Windows Server.
- **Discos de arranque**: Persistentes, balanceados, estándar o SSD.
- **Redes y firewall**: Configuración de reglas de red, balanceadores de carga, IP estática, etc.

---

# 💻 Creación de una VM

## A través de la Consola de Google Cloud

1. Ve a **Compute Engine > Instancias de VM**.
2. Haz clic en **Crear instancia**.
3. Configura:
   - Nombre: `gcelab`
   - Región y zona: según preferencia
   - Tipo de máquina: `e2-medium` (2 vCPU, 4 GB RAM)
   - Disco de arranque: Debian GNU/Linux 11 (10 GB)
   - Permitir tráfico HTTP
4. Haz clic en **Crear**.

## A través de la línea de comandos (gcloud)

###
gcloud compute instances create gcelab2 \
  --machine-type=e2-medium \
  --zone=us-central1-a
###

---

# 💰 Instancias Preemptibles

## ¿Qué son?

Las instancias preemptibles son máquinas virtuales temporales con costo reducido. Pueden ser detenidas por Google en cualquier momento.

## Características

- Costo hasta 91% más bajo.
- Duración máxima: 24 horas.
- Se detienen sin previo aviso (con un warning de 30s).
- Ideales para cargas de trabajo tolerantes a fallos.

## Casos de uso ideales

- Procesamiento por lotes
- Simulaciones
- Renderizado

---

# ⚙️ Autoescalado (Autoscaling)

## ¿Qué es?

Es la capacidad de incrementar o reducir automáticamente el número de instancias en un grupo según métricas definidas, como uso de CPU o tráfico.

## Componentes necesarios

- **Instance Template**: Plantilla base de configuración para todas las VMs.
- **Managed Instance Group (MIG)**: Grupo de instancias basado en la plantilla.
- **Política de autoscaling**: Define cuándo escalar hacia arriba o abajo.

## Comandos

### Crear plantilla de instancia

###
gcloud compute instance-templates create web-server-template \
  --machine-type=e2-medium \
  --image-family=debian-11 \
  --image-project=debian-cloud
###

### Crear grupo de instancias

###
gcloud compute instance-groups managed create web-server-group \
  --base-instance-name=web-server \
  --template=web-server-template \
  --size=2 \
  --zone=us-central1-a
###

### Configurar autoescalado

###
gcloud compute instance-groups managed set-autoscaling web-server-group \
  --max-num-replicas=5 \
  --min-num-replicas=2 \
  --target-cpu-utilization=0.6 \
  --cool-down-period=90 \
  --zone=us-central1-a
###

---

# 🌐 Balanceo de Carga

El tráfico puede ser distribuido automáticamente entre varias instancias mediante un balanceador de carga.

## Tipos de Balanceo en GCP

- **HTTP(S) Load Balancer**: Balanceo de capa 7.
- **TCP/SSL Proxy Load Balancer**: Balanceo de capa 4.
- **Network Load Balancer**: Balanceo básico de IP y puerto.
- **Internal Load Balancer**: Usado dentro de redes privadas.

---

# 📚 Recursos Recomendados

- [Documentación oficial de Compute Engine](https://cloud.google.com/compute/docs)
- [Guía de Autoescalado](https://cloud.google.com/compute/docs/autoscaler)
- [Instancias Preemptibles](https://cloud.google.com/compute/docs/instances/preemptible)
- [Tipos de máquina](https://cloud.google.com/compute/docs/machine-types)

---

