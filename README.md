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

Eligo **GitFlow** porque el curso se desarrolla durante todo el semestre y cada entrega (EP01, EP02, EP03) es un hito estable. La rama `develop` permite integrar las features terminadas sin ensuciar `main`, y la rama `hotfix/` deja corregir un bug en produccion sin interrumpir el trabajo en desarrollo. Ademas, GitFlow separa explicitamente el codigo estable (`main`) del codigo en integracion (`develop`), lo que da trazabilidad clara del codigo frente a lo que se pide en las rubricas del curso. Este repositorio se desarrolla de forma individual, por lo que el flujo se ejecuta por una sola persona, manteniendo igual la disciplina de ramas y pull requests.

### Estructura de ramas del proyecto

| Rama | Origen | Proposito | ¿Se borra? |
| --- | --- | --- | --- |
| `main` | inicial | Codigo estable, siempre listo para produccion | No |
| `develop` | main | Integracion de features terminadas | No |
| `feature/<nombre>` | develop | Un cambio de funcionalidad | Si, al fusionarse |
| `hotfix/<nombre>` | main | Correccion urgente de un bug en produccion | Si, al fusionarse |

Regla de naming: `feature/descripcion-corta` y `hotfix/descripcion-corta`, todo en minusculas y separado por guiones (por ejemplo `feature/pagina-presentacion`).

## Convenciones y buenas practicas

### Convencion de commits

Formato: `tipo(alcance): descripcion-corta`. Escrito en **minusculas y sin tildes**.

| Tipo | Para que | Ejemplo |
| --- | --- | --- |
| `feat` | Nueva funcionalidad | `feat(ui): agregar pie de pagina` |
| `fix` | Correccion de bug | `fix(home): corregir titulo` |
| `docs` | Documentacion | `docs: agregar changelog` |
| `chore` | Tareas / CI | `chore(ci): agregar workflow hola mundo` |

### Naming de ramas

`feature/<feature-name>` y `hotfix/<feature-name>`, en minusculas y con guiones. Ejemplos: `feature/pagina-presentacion`, `hotfix/titulo-pagina`.

### Flujo de merge

- Features y hotfix siempre entran por **pull request**, nunca push directo a `main` o `develop`.
- Se requiere al menos **1 aprobacion** antes de fusionar; en este repositorio en solitario la aprueba el propio autor tras revisar la diff.
- Usar merge commit o squash, y **borrar la rama** despues de fusionar.

### Estrategia de revision

- El autor abre el PR y revisa el diff antes de fusionar.
- En equipos, se asigna un revisor que comenta, aprueba o pide cambios; nunca se fusiona un PR sin revisar.
- Antes de cada PR: confirmar que `mvn test` pasa y revisar la diff.

> **Nota: repositorio en solitario (EP01).** Este encargo se desarrollo con una sola cuenta de GitHub, por lo que el rol de autor y revisor fue asumido por el mismo integrante. El flujo completo (crear rama desde su base, abrir PR, revisar el diff, aprobar y fusionar) se cumplio en cada cambio para validar las 2 features y el hotfix del indicador IE2.