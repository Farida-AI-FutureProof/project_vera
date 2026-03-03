# Metadata Schema

This document defines the metadata fields used in Project VERA's ingestion pipeline. Metadata is attached to every document stored in the vector database and enables secure retrieval, cross-domain analysis and role‑based access control (RBAC).

| Field | Type | Description |
| --- | --- | --- |
| `document_id` | string | Unique identifier for the document (e.g., NTSB `EventId`, FDA `Recall_Number`, shipment or order ID, or `email_id`). |
| `source` | string | High‑level source category, such as `aviation`, `fda`, `logistics`, or `email`. |
| `access_level` | enum | Security classification used for RBAC. Valid values are `public`, `internal_only`, and `confidential`. |
| `department` | string | Functional area or business unit associated with the document (e.g., `operations`, `quality`, `logistics`, `engineering`). |
| `date` | date | Timestamp relevant to the document’s context (e.g., event date, recall initiation date, shipment date, email timestamp). |
| `domain` | string | Optional domain classification for broad grouping (e.g., `aviation`, `regulatory`, `supply_chain`). |
| `user_role` | string | Role of the querying user (e.g., Junior, Senior, Compliance Officer). This is provided at query time and not stored with the document. |
| `additional_metadata` | object | Any dataset‑specific fields required for advanced analysis (e.g., `Classification` for recalls, `Weather_Condition` for aviation incidents, or `SLA_Hours` for logistics records). |

These fields are stored as key‑value pairs in the ChromaDB metadata associated with each document. By tagging documents consistently, the retrieval system can apply fine‑grained filters based on source, access level, department, or any custom metadata and enforce role‑based access control at query time.
