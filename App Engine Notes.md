Este documento recopila notas clave sobre Google Compute Engine y Google Cloud Shell para la creación y gestión de máquinas virtuales (VMs). Se describen los conceptos fundamentales de Compute Engine como servicio IaaS, la interfaz interactiva de Cloud Shell y la CLI gcloud, la organización de recursos en regiones y zonas, y los comandos esenciales usados en Cloud Shell para:

Crear instancias.

Conectarse vía SSH.

Actualizar e instalar software (NGINX).

Ver procesos y acceder a servicios HTTP.

Además, se complementa con información sobre plantillas de instancia y VMs preemptibles para optimizar configuración y costos, todo referenciado según la documentación oficial de Google Cloud.

☁️ Fundamentos de Google Compute Engine

IaaS de alto rendimiento: Compute Engine ofrece VMs autogestionadas con hipervisor KVM para Linux y Windows, almacenamiento local y duradero, y control mediante Google Cloud Console, gcloud o API REST (cloud.google.com).

Flexibilidad de configuración: Escoge tipo de máquina, disco de arranque y red según requisitos de CPU, memoria y almacenamiento (cloud.google.com).

Plantillas de instancia: Guarda la configuración de una VM (tipo, imagen, etiquetas, scripts) para recrear instancias uniformes o grupos administrados (MIGs) (cloud.google.com).

Instancias preemptibles: VMs a menor costo (60–91% descuento) que pueden detenerse si Google necesita capacidad; ideales para cargas de trabajo tolerantes a fallos (cloud.google.com).

🖥️ Google Cloud Shell y CLI gcloud

Cloud Shell: VM Debian con 5 GB de $HOME persistente, preconfigurada con gcloud, git, kubectl y editores (vim, nano) (cloud.google.com).

Autenticación automática: Al iniciar Cloud Shell, se autentica el usuario y se establece la variable PROJECT_ID para la sesión actual (cloud.google.com).

CLI gcloud: Herramienta para gestionar recursos de Compute Engine, IAM y servicios GCP con autocompletado y ayuda integrada (--help) (cloud.google.com).

📍 Organización geográfica: Regiones y Zonas

Región: Área geográfica que agrupa zonas (p.ej., us-central1) (cloud.google.com).

Zona: Ubicación aislada dentro de una región (p.ej., us-central1-a) con baja latencia y alta conectividad interna (cloud.google.com).

Recursos zonales: Instancias de VM y discos persistentes, que deben ubicarse en la misma zona para enlazarse correctamente (cloud.google.com).

Recursos regionales y globales: Direcciones IP estáticas y balanceadores de carga, que abarcan varias zonas o regiones (cloud.google.com).

🚀 Comandos esenciales en Cloud Shell

A continuación, los comandos más usados para gestionar VMs en Compute Engine, explicando su función y flujo de trabajo:

Comando: gcloud compute instances create <NOMBRE> --machine-type=<TIPO> --zone=<ZONA>

Crea una nueva instancia de VM con el tipo de máquina y zona especificados. Automáticamente aprovisiona disco raíz y red (cloud.google.com).

Comando: gcloud compute ssh <NOMBRE> --zone=<ZONA>

Establece una conexión SSH segura a la VM sin necesidad de gestionar manualmente claves, generándolas localmente si no existen (cloud.google.com).

Comando: sudo apt-get update

Actualiza la lista de paquetes disponibles en la VM, garantizando que las instalaciones posteriores usen las versiones más recientes de los repositorios de Debian/Ubuntu.

Comando: sudo apt-get install -y nginx

Instala el servidor web NGINX automáticamente, incluyendo dependencias, para desplegar aplicaciones HTTP.

Comando: ps auwx | grep nginx

Verifica los procesos activos de NGINX, mostrando el proceso maestro y los workers.

Comando: curl http://$(gcloud compute instances list --filter=name=<NOMBRE> --format='value(EXTERNAL_IP)')

Recupera la IP externa de la VM y realiza una solicitud HTTP, útil para validar que NGINX está atendiendo peticiones desde el exterior.

🔄 Elasticidad y Autoescalado Avanzado

Google Compute Engine permite aplicaciones elásticas ajustando dinámicamente el número de VMs según la demanda mediante Managed Instance Groups (MIGs) y políticas de autoscaling (cloud.google.com).

Autoscaling de Instancias (MIGs)

El autoscaler monitoriza métricas como la utilización de CPU y la capacidad de balanceo para añadir o eliminar VMs automáticamente. Por ejemplo, con target-cpu-utilization se define el porcentaje de uso de CPU deseado, y el autoscaler ajusta el tamaño del grupo en consecuencia (cloud.google.com).
También es posible programar escalados en horarios específicos usando scaling schedules para anticipar picos de tráfico (cloud.google.com). Cuando se combina con políticas basadas en la capacidad de balanceo de carga HTTP(S), las instancias se ajustan para mantener la calidad del servicio (cloud.google.com).

Balanceo de Carga en VPC

El tráfico entrante se distribuye con Load Balancers integrados en VPC, que incluyen HTTP(S), TCP/UDP y Network Load Balancing. Estos balanceadores colaboran con el autoscaler para redirigir peticiones a instancias saludables y equilibrar cargas (cloud.google.com).

Escalar hacia fuera vs Escalar hacia arriba

Se recomienda escalar horizontalmente (añadir más VMs) antes que escalar verticalmente (máquinas más potentes) para aprovechar la resiliencia distribuida y controlar costos (cloud.google.com).

Tipos de Máquina y Cuotas

Las VMs se agrupan en familias (E2, N2, C2…) con tipos predefinidos y personalizados, adaptados a diferentes cargas de trabajo. Cada familia ofrece distintos balances de CPU/RAM y está sujeta a cuotas de CPU por zona, que limitan la cantidad de núcleos disponibles para tu proyecto (cloud.google.com). Para ver las cuotas actuales, revisa la página de Quotas en la Cloud Console (cloud.google.com).

🔧 Complementos y mejores prácticas

Cambiar región/​zona por defecto: Usa gcloud config set compute/region <REGION> y gcloud config set compute/zone <ZONA> para no repetir flags en cada comando (cloud.google.com).

Utilizar plantillas de instancia para replicar configuraciones en múltiples VMs o grupos administrados, mejorando consistencia y eficiencia (cloud.google.com).

Implementar Managed Instance Groups (MIGs) con políticas de autoscaling basadas en CPU o métricas de Monitoring para adaptar recursos a la demanda (cloud.google.com).

Monitoreo y alertas: Configura Cloud Monitoring y Cloud Logging para supervisar salud de instancias y recibir notificaciones ante anomalías.

📚 Referencias

Compute Engine Overview (cloud.google.com)

Google Cloud CLI Overview (cloud.google.com)

Regions & Zones Documentation (cloud.google.com)

Preemptible VM Instances (cloud.google.com)

Instance Templates Guide (cloud.google.com)

Autoscaler Documentation (cloud.google.com)

SSH Connection Guide (cloud.google.com)

Global, Regional, Zonal Resources (cloud.google.com)

Create & Start Instance (cloud.google.com)

Changing Default Zone/Region (cloud.google.com)

