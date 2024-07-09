<p align="center"><img src="https://www.openapis.org/wp-content/uploads/sites/3/2016/10/OpenAPI_Pantone.png" width="500"></p>

# OpenAPI, Swagger UI, Docker
- OpenAPI v3.x
- Swagger UI v5.x

# Requirements
- Stable version of [Docker](https://docs.docker.com/engine/install/)
- Compatible version of [Docker Compose](https://docs.docker.com/compose/install/#install-compose)

# How To Deploy
- `docker compose up -d`

# Notes

### Swagger UI
- URL: http://localhost:8080

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
