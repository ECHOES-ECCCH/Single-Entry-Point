
# ECHOES API – Preliminary Concepts (v0.1)

> **Note:** This is a draft specification and subject to change.

---

## 📚 Table of Contents

### 🟢 GET Endpoints
- [List RDF Endpoints](#🟢-endpoint-list-rdf-endpoints)
- [List Metadata Sources](#🟢-endpoint-list-metadata-sources)
- [Digital Twin Contributors](#🟢-endpoint-digital-twin-contributors)
- [Digital Twin History](#🟢-endpoint-digital-twin-history)
- [Digital Twin Usage](#🟢-endpoint-digital-twin-usage)
- [User Files](#🟢-endpoint-user-files)
- [Search Digital Twins](#🟢-endpoint-search-digital-twins)

### 🟡 POST Endpoints
- [Register External Endpoint](#🟡-endpoint-register-external-endpoint)
- [Create a Digital Twin](#🟡-endpoint-create-a-digital-twin)
- [Preview a Digital Twin](#🟡-endpoint-preview-a-digital-twin)
- [Enrich a Digital Twin](#🟡-endpoint-enrich-a-digital-twin)
- [Share a Resource](#🟡-endpoint-share-a-resource)

### 🔵 PUT Endpoints
- [Update a Digital Twin](#🔵-endpoint-update-a-digital-twin)
- [Update Digital Twin Permissions](#🔵-endpoint-update-digital-twin-permissions)

---


## HTTP Method Icons

- 🟢 **GET** – Retrieve data  
- 🟡 **POST** – Submit new data  
- 🔵 **PUT** – Update existing data  

---

## 🟢 Endpoint: List RDF Endpoints

**Method:** `GET`  
**Path:** `/digital-twins/endpoints`

Retrieve a list of registered external RDF endpoints for federated querying.

---

## 🟢 Endpoint: List Metadata Sources

**Method:** `GET`  
**Path:** `/metadata/endpoints`

List available metadata repositories (internal and external).

---

## 🟢 Endpoint: Digital Twin Contributors

**Method:** `GET`  
**Path:** `/digital-twins/{id}/contributors`

Retrieve contributors (users or institutions) for a specific Digital Twin.

---

## 🟢 Endpoint: Digital Twin History

**Method:** `GET`  
**Path:** `/digital-twins/{id}/history`

Get version history of a Digital Twin including metadata, structure, or media changes.

---

## 🟢 Endpoint: Digital Twin Usage

**Method:** `GET`  
**Path:** `/digital-twins/{id}/usage`

Retrieve usage metrics for a Digital Twin: access, citations, or tool usage.

---

## 🟢 Endpoint: User Files

**Method:** `GET`  
**Path:** `/user-spaces/{id}/files`

List files uploaded by a user.

### Query Parameters

| Parameter      | Description                                      |
|----------------|--------------------------------------------------|
| `userId`       | ID of the requesting user                        |
| `fileType`     | Filter by file type (`rdf`, `video`, `csv`)      |
| `visibility`   | Visibility filter (`private`, `public`)          |
| `tags`         | Filter by tags (e.g., `Cyprus`, `2025`)          |
| `createdAfter` | Return files created after a specific date       |
| `sortBy`       | Sort by attribute (e.g., `uploadDate`)           |
| `order`        | Sorting order (`asc`, `desc`)                    |

---

## 🟢 Endpoint: Search Digital Twins

**Method:** `GET`  
**Path:** `/digital-twins`

Federated discovery of Digital Twins across local and external RDF sources.

### Query Parameters

| Parameter            | Description                                                        |
|----------------------|---------------------------------------------------------------------|
| `userId`             | ID of the requesting user                                           |
| `query`              | SPARQL query for federated retrieval                               |
| `sources`            | List of RDF sources (e.g., `echoes`, `external1`)                  |
| `includeMetadata`    | Include metadata in results (`true`/`false`)                        |
| `includeLinkedMedia` | Include linked media (`true`/`false`)                              |
| `hasMedia`           | Filter for Digital Twins with media (`true`/`false`)               |

---

## 🟡 Endpoint: Register External Endpoint

**Method:** `POST`  
**Path:** `/digital-twins/endpoints/register`

Register a new SPARQL endpoint for federated queries.

### Body Parameters

| Parameter            | Description                                   |
|----------------------|-----------------------------------------------|
| `userId`             | ID of the user registering the endpoint       |
| `endpointUrl`        | URL of the external SPARQL endpoint           |
| `accessPolicy`       | Access level (`read-only`, `read-write`)      |
| `contactEmail`       | Contact email address                         |
| `supportedOntologies`| List of supported ontologies                  |

---

## 🟡 Endpoint: Create a Digital Twin

**Method:** `POST`  
**Path:** `/digital-twins/create`

Create a Digital Twin using metadata and a Virtual Application.

### Body Parameters

| Parameter        | Description                                             |
|------------------|---------------------------------------------------------|
| `userId`         | ID of the user creating the Digital Twin               |
| `metadataSource` | Metadata source (e.g., local, federated, SPARQL)       |
| `vaToolId`       | Virtual Application tool ID for metadata processing    |
| `storageTarget`  | Where to store the Digital Twin (`local`, `federated`) |
| `visibility`     | Visibility of the Digital Twin (`private`, `public`)   |

---

## 🟡 Endpoint: Preview a Digital Twin

**Method:** `POST`  
**Path:** `/digital-twins/preview`

Preview a Digital Twin’s structure before saving.

### Body Parameters

| Parameter        | Description                                        |
|------------------|----------------------------------------------------|
| `userId`         | ID of the user requesting the preview             |
| `metadataSource` | Source of the metadata                            |
| `vaToolId`       | Virtual Application tool ID                       |
| `outputFormat`   | Format for preview (`JSON`, `RDF`, `TTL`)         |

---

## 🟡 Endpoint: Enrich a Digital Twin

**Method:** `POST`  
**Path:** `/digital-twins/{id}/enrich`

Add RDF data, media, or metadata to an existing Digital Twin.

### Body Parameters

| Parameter    | Description                                              |
|--------------|----------------------------------------------------------|
| `userId`     | ID of the enriching user                                 |
| `twinId`     | ID of the Digital Twin to be enriched                    |
| `data`       | RDF triples to be added                                  |
| `media`      | Media files to attach                                    |
| `metadata`   | Metadata describing the new content                      |
| `visibility` | Visibility of new content (`private`, `public`)          |

---

## 🟡 Endpoint: Share a Resource

**Method:** `POST`  
**Path:** `/user-spaces/{id}/share`

Share a file or Digital Twin with other users or groups.

### Body Parameters

| Parameter       | Description                                         |
|------------------|-----------------------------------------------------|
| `userId`         | ID of the sharing user                              |
| `resourceId`     | ID of the file or Digital Twin                      |
| `targetUserId`   | ID of recipient user or group                       |
| `permissions`    | Access level (`read-only`, `read-write`)            |
| `expirationDate` | Optional expiration date for access                 |
| `notify`         | Notify recipient (`true`/`false`)                   |
| `message`        | Optional custom message                             |

---

## 🔵 Endpoint: Update a Digital Twin

**Method:** `PUT`  
**Path:** `/digital-twins/{id}/update`

Modify content, metadata, or media of a Digital Twin.

### Body Parameters

| Parameter         | Description                                      |
|-------------------|--------------------------------------------------|
| `userId`          | ID of the user performing the update             |
| `twinId`          | ID of the Digital Twin                           |
| `updatedData`     | RDF triples to replace or modify existing data   |
| `updatedMetadata` | Updated metadata fields                          |
| `updatedMedia`    | Updated or replaced media files                  |
| `visibility`      | Updated visibility (`private`, `public`)         |
| `changeNote`      | Description of the change for version tracking   |

---

## 🔵 Endpoint: Update Digital Twin Permissions

**Method:** `PUT`  
**Path:** `/digital-twins/{id}/permissions`

Change access permissions for a Digital Twin.

### Body Parameters

| Parameter    | Description                             |
|--------------|-----------------------------------------|
| `userId`     | ID of the user updating permissions     |
| `twinId`     | ID of the Digital Twin                  |
| `permissions`| Updated permissions (e.g., read/write)  |

---
