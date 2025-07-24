# Multi-Cloud Analytics with BigLake, BigQuery Omni & Dataplex

## Objective

Build a scalable multi-cloud analytics solution that enables seamless querying of data stored across different cloud providers—Google Cloud Storage (GCS) and Azure Blob Storage—using Google Cloud's BigLake and BigQuery Omni. Implement centralized data governance and metadata management with Dataplex, allowing unified analytics and governance across hybrid and multi-cloud environments.

---

## Architecture Overview

```mermaid
graph LR
    subgraph Google Cloud
        GCS[Google Cloud Storage (GCS)]
        BQ[BigQuery]
        BL[BigLake External Tables]
        DP[Dataplex]
    end

    subgraph Azure Cloud
        AZBlob[Azure Blob Storage]
        AzureAD[Azure Active Directory]
    end

    GCS --> BL
    AZBlob --> BL
    BL --> BQ
    BQ --> DP
    AzureAD -- Federated Identity --> BQ
