# pagos-svc

Microservicio de pagos construido con Spring Boot 3.3, Java 21 y Docker.
Es el proyecto base de la asignatura Ingeniería DevOps (DOY0101) y la semilla del pipeline que trabajaremos en el semestre.

## Requisitos

- Docker (Desktop en Windows / Engine en Linux)
- Git

## Puesta en marcha

```bash
docker compose up --build -d
```

- Página de presentación: http://localhost:8080
- Swagger UI: http://localhost:8080/swagger-ui/index.html
- Consola H2: http://localhost:8080/h2-console
- API REST: http://localhost:8080/api/pagos

## Pruebas locales

```bash
mvn test    # unit tests
mvn verify  # verifica cobertura JaCoCo (exige 100 %)
```

## Modelo de ramificación

### Opciones que evalué

| Modelo | Cómo funciona | Ideal para |
| --- | --- | --- |
| **GitFlow** | Ramas `main` + `develop` + `feature/` + `hotfix/` | Proyectos con releases planificadas y una rama de integración |
| **GitHub Flow** | Solo `main` + `feature/` + pull request | Despliegue continuo simple y equipos pequeños |
| **Trunk-based** | Una sola rama (`main`/`trunk`) + ramas de vida corta | Entrega continua, tronco inestable no permitido |

### Modelo elegido: GitFlow

Elegí **GitFlow** porque el curso se desarrolla durante todo el semestre y cada entrega (EP01, EP02, EP03) es un hito estable. La rama `develop` me permite integrar las features terminadas sin ensuciar `main`, y la rama `hotfix/` me deja corregir un bug en producción sin interrumpir el trabajo en desarrollo. Además, GitFlow separa claramente el código estable (`main`) del código en integración (`develop`), lo que da trazabilidad frente a lo que piden las rúbricas del curso.

Este repositorio lo desarrollo de forma individual, así que mantengo la disciplina de ramas y pull requests aunque el flujo lo ejecute una sola persona.

### Estructura de ramas del proyecto

| Rama | Origen | Propósito | ¿Se borra? |
| --- | --- | --- | --- |
| `main` | inicial | Código estable, siempre listo para producción | No |
| `develop` | main | Integración de features terminadas | No |
| `feature/<nombre>` | develop | Un cambio de funcionalidad | Sí, al fusionarse |
| `hotfix/<nombre>` | main | Corrección urgente de un bug en producción | Sí, al fusionarse |

Regla de naming: `feature/descripcion-corta` y `hotfix/descripcion-corta`, todo en minúsculas y separado por guiones (por ejemplo `feature/pagina-presentacion`).

## Convenciones y buenas prácticas

### Convención de commits

Formato: `tipo(alcance): descripcion-corta`. Escrito en **minúsculas y sin tildes**.

| Tipo | Para qué | Ejemplo |
| --- | --- | --- |
| `feat` | Nueva funcionalidad | `feat(ui): agregar pie de pagina` |
| `fix` | Corrección de bug | `fix(home): corregir titulo` |
| `docs` | Documentación | `docs: agregar changelog` |
| `chore` | Tareas / CI | `chore(ci): agregar workflow hola mundo` |

### Naming de ramas

`feature/<feature-name>` y `hotfix/<feature-name>`, en minúsculas y con guiones. Ejemplos: `feature/pagina-presentacion`, `hotfix/titulo-pagina`.

### Flujo de merge

- Las features y hotfix siempre entran por **pull request**, nunca con push directo a `main` o `develop`.
- Se requiere al menos **1 aprobación** antes de fusionar; como este repo es en solitario, la aprueba el propio autor después de revisar la diff.
- Uso merge commit o squash y **borro la rama** luego de fusionar.

### Estrategia de revisión

- El autor abre el PR y revisa la diff antes de fusionar.
- En un equipo se asigna un revisor que comenta, aprueba o pide cambios; nunca se fusiona un PR sin revisar.
- Antes de cada PR: confirmar que `mvn test` pasa y revisar la diff.

> **Nota: repositorio en solitario (EP01).** Este encargo se desarrolló con una sola cuenta de GitHub, así que el rol de autor y revisor lo cumple la misma persona. El flujo completo (crear la rama desde su base, abrir el PR, revisar la diff, aprobar y fusionar) se hizo en cada cambio para validar las 2 features y el hotfix del indicador IE2.
