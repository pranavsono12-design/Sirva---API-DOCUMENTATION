# Sirva Relocation Management API – Documentation

## Overview

The **Sirva Relocation Management API** enables corporate clients and HR platforms to initiate, manage, and track employee relocations across Sirva’s global service network.

This API supports relocation workflows including:
- Request creation
- Relocation tracking
- Household goods moving coordination

---

## Base URL

```
https://api.sirva.com/v1
```

---

## Authentication

All API requests require authentication using a **Bearer Token**.

### Header

```
Authorization: Bearer <ACCESS_TOKEN>
```

If authentication fails, the API returns **401 Unauthorized**.

---

## Create a Relocation Request

Initiates a new employee relocation.

### Endpoint

```
POST /relocations
```

### Request Body

```json
{
  "employeeId": "EMP-2045",
  "originCountry": "USA",
  "destinationCountry": "Germany",
  "relocationType": "Corporate"
}
```

### Field Descriptions

| Field | Type | Required | Description |
|------|------|----------|------------|
| employeeId | string | Yes | Employee identifier |
| originCountry | string | Yes | Current country |
| destinationCountry | string | Yes | Destination country |
| relocationType | string | No | Corporate or Consumer |

### Response – 201 Created

```json
{
  "relocationId": "REL-78901",
  "employeeId": "EMP-2045",
  "originCountry": "USA",
  "destinationCountry": "Germany",
  "status": "INITIATED",
  "createdAt": "2026-02-05T07:20:00Z"
}
```

---

## Get Relocation Details

### Endpoint

```
GET /relocations/{relocationId}
```

### Response – 200 OK

```json
{
  "relocationId": "REL-78901",
  "employeeId": "EMP-2045",
  "originCountry": "USA",
  "destinationCountry": "Germany",
  "status": "IN_PROGRESS"
}
```

---

## Update Relocation Status

### Endpoint

```
PATCH /relocations/{relocationId}/status
```

### Request Body

```json
{
  "status": "COMPLETED"
}
```

### Allowed Status Values

- INITIATED  
- IN_PROGRESS  
- COMPLETED  
- CANCELLED  

---

## Get Household Goods Move Details

### Endpoint

```
GET /moves/{relocationId}
```

### Response – 200 OK

```json
{
  "relocationId": "REL-78901",
  "moveProvider": "Allied",
  "estimatedMoveDate": "2026-03-01",
  "storageRequired": true
}
```

---

## Common Error Format

```json
{
  "errorCode": "RELOCATION_NOT_FOUND",
  "message": "The requested relocation does not exist"
}
```

---

## HTTP Status Codes

| Code | Meaning |
|-----:|--------|
| 200 | Success |
| 201 | Resource created |
| 400 | Invalid request |
| 401 | Unauthorized |
| 404 | Not found |
| 500 | Server error |
