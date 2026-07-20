openapi: 3.0.3

info:
  title: Demo Task API
  version: 1.0.0
  description: Simple API example for Redocly.

servers:
  - url: https://api.example.com/v1
    description: Production

tags:
  - name: Tasks
    description: Task management

paths:
  /tasks:
    get:
      tags:
        - Tasks
      summary: Get task list
      parameters:
        - name: status
          in: query
          description: Filter by status
          required: false
          schema:
            $ref: "#/components/schemas/TaskStatus"
      responses:
        "200":
          description: List of tasks
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: "#/components/schemas/Task"

    post:
      tags:
        - Tasks
      summary: Create task
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: "#/components/schemas/CreateTaskRequest"
      responses:
        "201":
          description: Task created
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/Task"

  /tasks/{taskId}:
    get:
      tags:
        - Tasks
      summary: Get task by ID
      parameters:
        - name: taskId
          in: path
          required: true
          schema:
            type: integer
            example: 42
      responses:
        "200":
          description: Task details
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/Task"

        "404":
          description: Task not found
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/Error"

    patch:
      tags:
        - Tasks
      summary: Update task status
      parameters:
        - name: taskId
          in: path
          required: true
          schema:
            type: integer

      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              required:
                - status
              properties:
                status:
                  $ref: "#/components/schemas/TaskStatus"

      responses:
        "200":
          description: Updated task
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/Task"

components:

  schemas:

    TaskStatus:
      type: string
      enum:
        - pending
        - in_progress
        - completed

    Task:
      type: object
      required:
        - id
        - title
        - status
      properties:
        id:
          type: integer
          example: 42

        title:
          type: string
          example: Buy groceries

        description:
          type: string
          nullable: true
          example: Milk, bread and eggs

        status:
          $ref: "#/components/schemas/TaskStatus"

        createdAt:
          type: string
          format: date-time
          example: "2026-07-20T10:15:00Z"

    CreateTaskRequest:
      type: object
      required:
        - title
      properties:
        title:
          type: string
          example: Buy groceries

        description:
          type: string
          example: Milk, bread and eggs

    Error:
      type: object
      properties:
        code:
          type: string
          example: TASK_NOT_FOUND

        message:
          type: string
          example: Task with given ID was not found