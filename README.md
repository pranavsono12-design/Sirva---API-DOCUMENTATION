# Sirva Relocation Management API Documentation

## Overview
This repository contains API documentation for a hypothetical
Sirva Relocation Management platform designed to support corporate
employee relocations and global moving services.

The documentation demonstrates how Sirva’s enterprise systems or
external HR platforms could initiate relocation requests, track
relocation status, and retrieve household goods moving details.

## Contents
- **sirva-relocation-api.yaml**  
  OpenAPI 3.0 specification serving as the single source of truth
  for the API.

- **api-documentation.md**  
  Human-readable API documentation including endpoint explanations,
  request/response examples, and error handling.

## How to View the API Reference
The OpenAPI file can be rendered using tools such as:
- Swagger UI
- Redoc
- Stoplight

Example:
1. Open https://editor.swagger.io
2. Upload `sirva-relocation-api.yaml`
3. View the auto-generated API reference

## Assumptions
- Authentication is handled via Bearer tokens (JWT).
- The API is intended for enterprise HR integrations.
- The API is designed to be scalable across multiple countries.

## Purpose
This documentation was created as part of an API documentation
assessment to demonstrate technical writing, OpenAPI knowledge,
and understanding of enterprise API design.
