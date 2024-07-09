<p align="center"><img src="https://www.openapis.org/wp-content/uploads/sites/3/2016/10/OpenAPI_Pantone.png" width="500"></p>

# OpenAPI, Swagger, Docker
- OpenAPI v3.x
- Swagger UI v5.x
- Swagger Editor v4.x
- Redoc v2.x

# Requirements
- Stable version of [Docker](https://docs.docker.com/engine/install/)
- Compatible version of [Docker Compose](https://docs.docker.com/compose/install/#install-compose)

# How To Deploy
- `docker compose up -d`

# Notes

### Swagger UI (Docker)
- URL: http://localhost:8080

### GitHub Pages
- Swagger UI: https://refactorian.github.io/openapi-swagger-docker
- Swagger Editor: https://refactorian.github.io/openapi-swagger-docker/editor
- Redoc: https://refactorian.github.io/openapi-swagger-docker/redoc

### Docker compose commands
- Build or rebuild services
    - `docker compose build`
- Create and start containers
    - `docker compose up -d`
- Stop and remove containers, networks
    - `docker compose down`
- Stop all services
    - `docker compose stop`
- Restart service containers
    - `docker compose restart`
- Run a command inside a container
    - `docker compose exec [container] [command]`


# OpenAPI Specification Guide

The OpenAPI Specification (OAS) is a standard, language-neutral way to define your API. It helps humans and computers discover and understand what your service can do, all without needing to look at the source code or documentation or inspect network traffic. An OpenAPI document is a YAML or JSON file that outlines the API’s endpoints, operations, input and output parameters, request and response formats, authentication methods, and more.

### Basic Structure

1. **OpenAPI Version**
   ```yaml
   openapi: 3.0.0
   ```

2. **Info Object**
   ```yaml
   info:
     title: Sample API
     description: API description in Markdown.
     version: 1.0.0
   ```

3. **Servers Object**
   ```yaml
   servers:
     - url: https://api.example.com/v1
       description: Production server
   ```

4. **Paths Object**
   ```yaml
   paths:
     /users:
       get:
         summary: Returns a list of users.
         responses:
           '200':
             description: A JSON array of user names
             content:
               application/json:
                 schema: 
                   type: array
                   items:
                     type: string
   ```

### Components

1. **Schemas**
   ```yaml
   components:
     schemas:
       User:
         type: object
         properties:
           id:
             type: integer
           name:
             type: string
   ```

2. **Parameters**
   ```yaml
   components:
     parameters:
       UserId:
         name: userId
         in: path
         required: true
         schema:
           type: integer
   ```

3. **Responses**
   ```yaml
   components:
     responses:
       NotFound:
         description: Entity not found.
   ```

4. **Security Schemes**
   ```yaml
   components:
     securitySchemes:
       ApiKeyAuth:
         type: apiKey
         in: header
         name: X-API-Key
   ```

### Key Elements

### Paths
Defines the available paths and operations for the API.
```yaml
paths:
  /pets:
    get:
      summary: List all pets
      operationId: listPets
      responses:
        '200':
          description: A paged array of pets
          content:
            application/json:    
              schema: 
                type: array
                items: 
                  $ref: '#/components/schemas/Pet'
```

### Parameters
Defines the inputs to an API method, which could be path, query, header, or cookie parameters.
```yaml
parameters:
  - in: query
    name: limit
    schema:
      type: integer
    description: How many items to return at one time (max 100)
```

### Responses
Defines the possible responses from an API method.
```yaml
responses:
  '200':
    description: A paged array of pets
    headers:
      x-next:
        description: A link to the next page of responses
        schema:
          type: string
    content:
      application/json:
        schema: 
          type: array
          items: 
            $ref: '#/components/schemas/Pet'
```

### Components
Holds reusable objects, such as schemas, responses, parameters, and security definitions.
```yaml
components:
  schemas:
    Pet:
      type: object
      required:
        - id
        - name
      properties:
        id:
          type: integer
          format: int64
        name:
          type: string
        tag:
          type: string
```

### Best Practices

1. **Use Meaningful Descriptions:** Provide detailed descriptions for each field, endpoint, and response to make the documentation user-friendly.
2. **Keep It DRY (Don't Repeat Yourself):** Utilize the components section to avoid redundancy.
3. **Validate the Specification:** Use tools like Swagger or Redocly to validate and visualize your OpenAPI specification.
4. **Document Security:** Clearly define authentication and authorization mechanisms.
5. **Version Your API:** Include versioning in the API paths or headers to handle breaking changes gracefully.
