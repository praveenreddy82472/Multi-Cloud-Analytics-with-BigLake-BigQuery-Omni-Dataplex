# Multi-Cloud Analytics with BigLake, BigQuery Omni & Dataplex

## Objective

Build a scalable multi-cloud analytics solution that enables seamless querying of data stored across Google Cloud Storage (GCS) and Azure Blob Storage, leveraging Google Cloud’s BigLake and BigQuery Omni. Integrate Dataplex for centralized data governance and metadata management across hybrid and multi-cloud environments.

---

## Architecture Overview

[GCS]              [Azure Blob Storage]
   |                       |
   +-------+       +-------+
           |       |
       [BigLake External Tables]
           |
   +-------+-------+
   |               |
[BigQuery Omni]   [Dataplex]
       |               |
   [BigQuery]      [Governance & Metadata]
       |
[Analytics & BI Tools]


---

Data is stored raw in GCS and Azure Blob Storage.

BigLake exposes external tables on top of these cloud storage files.

BigQuery Omni enables cross-cloud querying with a federated identity connection to Azure.

Dataplex manages metadata, data zones, and governance policies across clouds.

---

## Key Steps

Uploaded sample data files to GCS and Azure Blob Storage.

Created BigLake external tables referencing these files via BigQuery Omni.

Configured federated identity for secure cross-cloud authentication.

Used Dataplex to set up lakes, zones, and assets for unified metadata and governance.

Queried external tables in BigQuery to analyze data across clouds.

---

---
## Challenges & Solutions

Authentication: Set up Azure App Registration and federated identity to enable secure access.

Region Alignment: Ensured BigQuery datasets are in the same region as the BigQuery Omni connection.

Permissions: Assigned correct Azure Blob Storage roles to the Google service account.

Governance: Leveraged Dataplex for consistent metadata and policy management.

---

---
## Impact & Benefits
Unified analytics platform querying multi-cloud data without data duplication.

Reduced storage and compute costs by querying external tables.

Centralized data governance and metadata management.

Scalable architecture supporting hybrid and multi-cloud strategies.

---
---
## How to Run
Upload data to GCS and Azure Blob Storage.

Create a BigQuery dataset in region azure-eastus2.

Configure federated identity between GCP and Azure AD.

Create BigLake external tables using existing connections.

Set up Dataplex lakes and zones.

Query data using BigQuery SQL.


