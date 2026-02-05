Sirva Relocation Management API – Documentation
Overview

The Sirva Relocation Management API enables corporate clients and HR platforms to initiate, manage, and track employee relocations across Sirva’s global service network.

This API supports relocation workflows including request creation, relocation tracking, and household goods moving coordination.

Base URL
https://api.sirva.com/v1

Authentication

All API requests require authentication using a Bearer Token.

Header

Authorization: Bearer <ACCESS_TOKEN>


If authentication fails, the API returns 401 Unauthorized.

Create a Relocation Request

Initiates a new employee relocation.

Endpoint
POST /relocations

Request Body
{
  "employeeId": "EMP-2045",
  "originCountry": "USA",
  "destinationCountry": "Germany",
  "relocationType": "Corporate"
}

Field Description
Field	Type	Required	Description
employeeId	string	yes	Employee identifier
originCountry	string	yes	Current country
destinationCountry	string	yes	Destination country
relocationType	string	no	Corporate or Consumer
Response – 201 Created
{
  "relocationId": "REL-78901",
  "employeeId": "EMP-2045",
  "originCountry": "USA",
  "destinationCountry": "Germany",
  "status": "INITIATED",
  "createdAt": "2026-02-05T07:20:00Z"
}

Get Relocation Details

Retrieves details of an existing relocation request.

Endpoint
GET /relocations/{relocationId}

Response – 200 OK
{
  "relocationId": "REL-78901",
  "employeeId": "EMP-2045",
  "originCountry": "USA",
  "destinationCountry": "Germany",
  "status": "IN_PROGRESS"
}

Update Relocation Status

Updates the current status of a relocation.

Endpoint
PATCH /relocations/{relocationId}/status

Request Body
{
  "status": "COMPLETED"
}

Allowed Status Values

INITIATED

IN_PROGRESS

COMPLETED

CANCELLED

Get Household Goods Move Details

Retrieves moving and storage details associated with a relocation.

Endpoint
GET /moves/{relocationId}

Response – 200 OK
{
  "relocationId": "REL-78901",
  "moveProvider": "Allied",
  "estimatedMoveDate": "2026-03-01",
  "storageRequired": true
}

Common Error Format
{
  "errorCode": "RELOCATION_NOT_FOUND",
  "message": "The requested relocation does not exist"
}

HTTP Status Codes
Code	Meaning
200	Success
201	Resource created
400	Invalid request
401	Unauthorized
404	Not found
500	Server error