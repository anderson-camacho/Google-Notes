# 📝 Google Cloud Concepts and Notes

## ☁️ What is Cloud Computing?

**Definition:**\
Cloud computing is a method of using technological resources virtually and on-demand via the internet. It allows users to access and manage resources like servers, storage, and applications without worrying about the physical infrastructure.

### Key Characteristics:

- **On-demand Self-service**: Instant availability of resources as needed.
- **Broad Network Access**: Accessible from anywhere with internet.
- **Resource Pooling**: Shared resources among multiple users.
- **Rapid Elasticity**: Quickly scalable according to demand.
- **Measured Service**: Payment based only on resources used.

---

## 🛠️ Differences Between Traditional and Cloud Architecture

| Traditional Architecture    | Cloud Computing                  |
| --------------------------- | -------------------------------- |
| Dedicated physical servers  | Virtualized and shared resources |
| Limited scalability         | Rapid and flexible scalability   |
| Intensive manual management | Automated management             |
| High initial costs          | Variable costs based on usage    |

Google employs a **container-based architecture** to facilitate scalability and reduce complexity.

---

## 🌍 Google's Data Centers

- First to achieve **ISO 14001** certification (environmental management).
- Notable Example: **Finland**, recognized for efficiency and sustainability.

---

## 🔧 Cloud Service Models

### Infrastructure as a Service (IaaS)

- Basic computing resources (servers, storage, networks).
- Examples: Google Compute Engine.

### Platform as a Service (PaaS)

- Pre-configured infrastructure for developing and running applications.
- Examples: Google App Engine, Cloud Run.

### Software as a Service (SaaS)

- Complete applications available online.
- Examples: Gmail, Google Docs, Google Drive (Workspace).

---

## 📐 Google Cloud Infrastructure

### Primary Layers:

1. **Networking and Security:**

   - Foundation supporting all infrastructure and applications.

2. **Compute and Storage:**

   - Decoupling allows independent scaling.

   - Services:

     - **Compute Engine** (virtual machines)
     - **Google Kubernetes Engine** (container orchestration)
     - **App Engine** (managed platform)
     - **Cloud Run** and **Cloud Functions** (serverless computing)

   - Managed Storage:

     - **Cloud Storage**
     - **Cloud SQL and Spanner** (relational databases)
     - **Bigtable and Firestore** (NoSQL databases)

3. **Big Data and Machine Learning:**

   - Tools for data ingestion, storage, processing, and analysis.
   - Key Services:
     - **BigQuery** (real-time data analytics)
     - **Dataflow** (data processing and pipelines)
     - **Dataproc** (Hadoop and Spark processing)
     - **Pub/Sub** (real-time messaging)
     - **Looker** (visualization)
     - **AutoML and Vertex AI** (managed artificial intelligence and machine learning)

---

## 🗺️ Google Cloud Geography and Distribution

- **Regions and Zones:**

  - Region: Independent geographic area with several zones.
  - Zone: Specific area where resources are deployed.
  - Example: Region `europe-west2` (London) has 3 zones.

- **Multi-region Configurations:**

  - Improved availability and resilience.
  - Example: **Spanner** database with multi-region replication (Netherlands, Belgium).

- **Current Distribution:** 121 zones across 40 global regions.

- Constant updates available at [Google Cloud Locations](https://cloud.google.com/about/locations).

---

## ⚙️ Serverless Computing

- **Definition:**

  - Enables developing applications without managing infrastructure.

- **Google Services:**

  - **Cloud Run** (container-based microservices applications).
  - **Cloud Functions** (event-driven code execution).

- **Advantages:**

  - Focus on code development.
  - Pay-as-you-go pricing.

---

## 📌 Summary of Key Google Cloud Services

| Category    | Services                                                 |
| ----------- | -------------------------------------------------------- |
| 🖥️ Compute | Compute Engine, Kubernetes Engine, App Engine, Cloud Run |
| 💾 Storage  | Cloud Storage, Cloud SQL, Spanner, Bigtable, Firestore   |
| 📊 Big Data | BigQuery, Dataflow, Dataproc, Pub/Sub, Looker            |
| 🤖 ML & AI  | AutoML, Vertex AI                                        |

---

## 🔗 Useful Links

- a[Google Cloud Platform](https://cloud.google.com/)
- [Data Center Locations](https://cloud.google.com/about/locations)

These notes will help you efficiently and clearly review key Google Cloud concepts.

