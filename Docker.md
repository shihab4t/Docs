# Docker

## Commands

- `docker ps`
- `docker build -t shihab4t/demoapp:1.0 .`
- `docker run -p 5000:8080 shihab4t/demoapp:1.0`
- `docker volume create shared-stuff`
- `docker run --mount source=shared-stuff, target=/stuff`
- `docker-compose up`
