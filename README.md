# pagos-svc

Microservicio de pagos construido con Spring Boot 3.3, Java 21 y Docker.
Proyecto base de la asignatura Ingenieria DevOps (DOY0101) para el pipeline del semestre.

## Requisitos

- Docker (Desktop en Windows / Engine en Linux)
- Git

## Puesta en marcha

```bash
docker compose up --build -d
```

- Pagina de presentacion: http://localhost:8080
- Swagger UI: http://localhost:8080/swagger-ui/index.html
- Consola H2: http://localhost:8080/h2-console
- API REST: http://localhost:8080/api/pagos

## Pruebas locales

```bash
mvn test    # unit tests
mvn verify  # verifica cobertura JaCoCo (exige 100 %)
```