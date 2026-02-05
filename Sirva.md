openapi: 3.0.3

info:
  title: Sirva Relocation Management API
  description: |
    The Sirva Relocation Management API enables corporate clients
    and HR systems to initiate, manage, and track employee relocation
    requests across Sirva’s global network.

    The API supports end-to-end relocation workflows including
    move initiation, status tracking, and service coordination.
  version: 1.0.0
  contact:
    name: Sirva API Support
    email: api-support@sirva.com

servers:
  - url: https://api.sirva.com/v1
    description: Production server

security:
  - bearerAuth: []

tags:
  - name: Relocations
    description: Employee relocation management
  - name: Moves
    description: Household goods moving and storage

paths:
  /relocations:
    post:
      tags:
        - Relocations
      summary: Create a relocation request
      description: Initiates a new employee relocation request.
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: "#/components/schemas/CreateRelocationRequest"
            example:
              employeeId: EMP-2045
              originCountry: USA
              destinationCountry: Germany
              relocationType: Corporate
      responses:
        "201":
          description: Relocation request created successfully
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/Relocation"
        "400":
          description: Invalid request data
        "401":
          description: Unauthorized

  /relocations/{relocationId}:
    get:
      tags:
        - Relocations
      summary: Get relocation details
      description: Retrieves details of a specific relocation request.
      parameters:
        - name: relocationId
          in: path
          required: true
          schema:
            type: string
      responses:
        "200":
          description: Relocation details retrieved
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/Relocation"
        "404":
          description: Relocation not found

  /relocations/{relocationId}/status:
    patch:
      tags:
        - Relocations
      summary: Update relocation status
      description: Updates the current status of a relocation.
      parameters:
        - name: relocationId
          in: path
          required: true
          schema:
            type: string
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: "#/components/schemas/UpdateRelocationStatusRequest"
            example:
              status: IN_PROGRESS
      responses:
        "200":
          description: Relocation status updated successfully
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/RelocationStatusResponse"
        "400":
          description: Invalid status value
        "404":
          description: Relocation not found

  /moves/{relocationId}:
    get:
      tags:
        - Moves
      summary: Get move details
      description: Retrieves household goods moving details for a relocation.
      parameters:
        - name: relocationId
          in: path
          required: true
          schema:
            type: string
      responses:
        "200":
          description: Move details retrieved
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/Move"
        "404":
          description: Move details not found

components:
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT

  schemas:
    CreateRelocationRequest:
      type: object
      required:
        - employeeId
        - originCountry
        - destinationCountry
      properties:
        employeeId:
          type: string
          example: EMP-2045
        originCountry:
          type: string
          example: USA
        destinationCountry:
          type: string
          example: Germany
        relocationType:
          type: string
          enum:
            - Corporate
            - Consumer
          example: Corporate

    Relocation:
      type: object
      properties:
        relocationId:
          type: string
          example: REL-78901
        employeeId:
          type: string
        originCountry:
          type: string
        destinationCountry:
          type: string
        relocationType:
          type: string
        status:
          type: string
          example: INITIATED
        createdAt:
          type: string
          format: date-time
          example: 2026-02-05T07:20:00Z

    UpdateRelocationStatusRequest:
      type: object
      required:
        - status
      properties:
        status:
          type: string
          enum:
            - INITIATED
            - IN_PROGRESS
            - COMPLETED
            - CANCELLED

    RelocationStatusResponse:
      type: object
      properties:
        relocationId:
          type: string
          example: REL-78901
        status:
          type: string
          example: IN_PROGRESS
        updatedAt:
          type: string
          format: date-time
          example: 2026-02-06T11:45:00Z

    Move:
      type: object
      properties:
        relocationId:
          type: string
          example: REL-78901
        moveProvider:
          type: string
          example: Allied
        estimatedMoveDate:
          type: string
          format: date
          example: 2026-03-01
        storageRequired:
          type: boolean
          example: true
