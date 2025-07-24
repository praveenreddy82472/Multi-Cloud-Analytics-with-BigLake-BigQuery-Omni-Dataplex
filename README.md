# Multi-Cloud Analytics with BigLake, BigQuery Omni & Dataplex

## Objective

Build a scalable multi-cloud analytics solution that enables seamless querying of data stored across Google Cloud Storage (GCS) and Azure Blob Storage, leveraging Google Cloud’s BigLake and BigQuery Omni. Integrate Dataplex for centralized data governance and metadata management across hybrid and multi-cloud environments.

---

---

## Project Story & Workflow

First, we started by creating buckets in Google Cloud Storage (GCS) to hold our raw data files like CSV and ORC formats. Next, we set up a BigQuery dataset to logically organize our tables.

Instead of loading data directly into BigQuery tables, we created BigLake external tables. These external tables don’t physically store data inside BigQuery — they just hold metadata and pointers to the files stored in GCS. This allows us to query data directly in Cloud Storage without copying or duplicating it. Since BigQuery only accesses the metadata, you won’t see data previews inside BigQuery, but queries run on the actual files stored externally.

For the multi-cloud part, we also worked with Azure Blob Storage. We first created an external connection from BigQuery Omni to our Azure Blob Storage account. Then, in BigQuery, we created a dataset located in the Azure region (e.g., azure-eastus2) and created external tables referencing the data files stored in Azure Blob Storage via this connection. Similar to GCS external tables, the data stays physically in Azure; BigQuery just queries it remotely.

To manage data governance and metadata, we used Dataplex. We created a Raw Zone in Dataplex and linked it to our GCS bucket assets. Dataplex then scanned the data, automatically discovered schemas, and allowed us to enforce policies such as data lineage, sensitive data classification, and access controls. Because we did not transform or curate the data in this project, we didn’t create a Curated Zone.

This architecture enables seamless querying and governance of data spread across multiple cloud platforms without data duplication or movement. It showcases how BigLake and BigQuery Omni allow unified multi-cloud analytics, while Dataplex provides centralized governance and metadata management.

---



## Architecture Overview

    [Google Cloud Storage (GCS)]        [Azure Blob Storage]
                |                                |
                +---------------+----------------+
                                |
                    [BigLake External Tables]
                                |
                +---------------+----------------+
                |                                |
        [BigQuery Omni]                     [Dataplex]
                |                                |
         [BigQuery SQL]                  [Governance & Metadata]
                |
      [Analytics & BI Tools (Looker, Data Studio, etc.)]



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


