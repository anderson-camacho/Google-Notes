## Notas para consulta rápida: Cloud Run Functions

### Conceptos clave

- Cloud Run Functions ejecuta código en respuesta a **eventos** (HTTP, Pub/Sub, Cloud Storage) sin necesidad de gestionar infraestructura.
- Es **serverless**: Google gestiona el escalado automático y facturación solo por ejecución.
- Ideal para tareas esporádicas o de corta duración: generación de miniaturas, notificaciones, procesamiento de datos.

### Flujo de trabajo

1. **Preparar** el código y dependencias localmente.  
2. **Implementar** la función con `gcloud functions deploy`.  
3. **Probar** disparadores (p.ej., publicar en un tema de Pub/Sub).  
4. **Revisar registros** con `gcloud functions logs read` para validar la ejecución.

### Ejemplo de código

El archivo `index.js` contiene la lógica de la función:

```javascript
const functions = require('@google-cloud/functions-framework');

functions.cloudEvent('helloPubSub', cloudEvent => {
  const data = cloudEvent.data.message.data;
  const name = data ? Buffer.from(data, 'base64').toString() : 'World';
  console.log(`Hello, ${name}!`);
});
```

El archivo `package.json` define dependencias y scripts:

```json
{
  "name": "gcf_hello_world",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "@google-cloud/functions-framework": "^3.0.0"
  }
}
```

### Comandos esenciales

```bash
# Establecer región predeterminada
gcloud config set run/region REGION

# Crear directorio de la función y entrar
dkdir gcf_hello_world && cd gcf_hello_world

# Editar index.js (pegar código de ejemplo)
nano index.js

# Editar package.json (pegar JSON de ejemplo)
nano package.json

# Instalar dependencias
npm install

# Desplegar la función en Gen2 con Pub/Sub como disparador
gcloud functions deploy helloPubSub \
  --gen2 \
  --runtime=nodejs20 \
  --region=REGION \
  --source=. \
  --entry-point=helloPubSub \
  --trigger-topic=cf-demo \
  --stage-bucket=PROJECT_ID-bucket \
  --service-account=cloudfunctionsa@PROJECT_ID.iam.gserviceaccount.com \
  --allow-unauthenticated

# Ver detalles de la función
gcloud functions describe helloPubSub --region=REGION

# Publicar un mensaje en Pub/Sub para disparar la función
gcloud pubsub topics publish cf-demo --message="Cloud Function Gen2"

# Leer registros de la función
gcloud functions logs read helloPubSub --region=REGION
``` 

### Detalles importantes

- **Tipos de disparador**: Pub/Sub, HTTP, Storage, entre otros.
- **Entorno Gen2**: Funciones corren sobre Cloud Run, aprovechando contenedores serverless y Eventarc.
- **Permisos**: La cuenta de servicio debe tener roles `roles/pubsub.publisher` para publicar y `roles/run.invoker` para invocación.

### Referencias

- Documentación general de Cloud Run Functions: https://cloud.google.com/functions  
- Guía rápida (CLI): https://cloud.google.com/functions/docs/quickstart-cli  
- Triggers y eventos: https://cloud.google.com/functions/docs/calling  
- Monitoreo y registros: https://cloud.google.com/functions/docs/monitoring/logging

