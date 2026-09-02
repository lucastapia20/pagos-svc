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

## Modelo de ramificacion

### Opciones evaluadas

| Modelo | Como funciona | Ideal para |
| --- | --- | --- |
| **GitFlow** | Ramas `main` + `develop` + `feature/` + `hotfix/` | Proyectos con releases planificadas y rama de integracion |
| **GitHub Flow** | Solo `main` + `feature/` + pull request | Despliegue continuo simple y equipos pequenos |
| **Trunk-based** | Rama unica (`main`/`trunk`) + ramas de vida corta | Entrega continua, tronco inestable no permitido |

### Modelo elegido: GitFlow

Elegimos **GitFlow** porque el curso se desarrolla durante todo el semestre y cada entrega (EP01, EP02, EP03) es un hito estable. La rama `develop` nos permite integrar features de ambos integrantes sin ensuciar `main`, y la rama `hotfix/` nos deja corregir un bug en produccion sin interrumpir el trabajo en desarrollo. Ademas, GitFlow separa explicitamente el codigo estable (`main`) del codigo en integracion (`develop`), lo que da trazabilidad clara del codigo frente a lo que se pide en las rubricas del curso.

### Estructura de ramas del proyecto

| Rama | Origen | Proposito | ¿Se borra? |
| --- | --- | --- | --- |
| `main` | inicial | Codigo estable, siempre listo para produccion | No |
| `develop` | main | Integracion de features terminadas | No |
| `feature/<nombre>` | develop | Un cambio de funcionalidad | Si, al fusionarse |
| `hotfix/<nombre>` | main | Correccion urgente de un bug en produccion | Si, al fusionarse |

Regla de naming: `feature/descripcion-corta` y `hotfix/descripcion-corta`, todo en minusculas y separado por guiones (por ejemplo `feature/pagina-presentacion`).