# Backend, API y commits para T6

Revisión documental actualizada el 2026-11-22. No se arrancó el servicio ni se ejecutaron pruebas para esta actualización.

## Un backend y el cuarto backend (criterios 3 y 15)

FOCCUS tiene una aplicación FastAPI en `FOCCUS/backend/api_usuarios/app/main.py`. Sus routers separan responsabilidades de usuarios, proyectos, guiones, escenas y otros módulos, pero no son cuatro servicios independientes.

Una ventaja es compartir API y controles entre módulos. Un riesgo es que los cambios, el despliegue o los fallos afecten al conjunto; por eso hay que coordinar los contratos web y móvil.

Se confirmó que el backend arranca y se aprobó explicar sus responsabilidades para el criterio 3. Para el criterio 15 se acordó comparar la evolución de un solo backend; está pendiente que el instructor acepte esa adaptación al texto original sobre cuatro. Ver [backend y recorrido](../sustentacion%20t6/backend-y-recorrido.md) y [comparación histórica](../sustentacion%20t6/requisito-15.md).

## API e instalación (criterio 12)

El `README.md` de FOCCUS describe la preparación del backend y frontend, `.env.example` y `/docs`. En un [arranque aislado documentado](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/docs/agentes/T6_EVIDENCIA.md), `/docs` y `/openapi.json` respondieron; esa ejecución no demuestra una instalación completa. No se repitió aquí. No publiques valores de configuración ni credenciales.

| Responsabilidad | Rutas presentes en el código | Fuente |
|---|---|---|
| Acceso | `POST /users/login`, `POST /users/2fa/send`, `POST /users/2fa/verify` | `app/routes/user_routes.py` |
| Proyectos | `GET /projects`, `POST /projects/create` | `app/routes/project_routes.py` |
| Guiones y escenas | `GET /guiones`, `POST /guiones/texto`, `GET /guiones/{id_guion}/escenas` | `app/routes/guion_routes.py`, `escena_routes.py` |
| Galería y desglose | `GET /projects/{id_project}/galeria`, `GET /guiones/{id_guion}/desglose` | `galeria_routes.py`, `desglose_routes.py` |
| Rodaje | `GET /projects/{id_project}/rodajes` | `rodaje_routes.py` |

Estas rutas describen el código, no una respuesta observada en esta revisión; tampoco sustituyen la documentación completa de entradas, respuestas y permisos. El [commit `60e43ad`](https://github.com/Cr4ckJu4nF3/FOCCUS/commit/60e43ad) incorpora el catálogo de bloques. El [registro web](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/docs/agentes/CAMBIOS_WEB.md) informa que su tabla se aplicó en Aiven; la [guía Docker](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/docs/DOCKER_LOCAL.md) registra pruebas con datos ficticios en MySQL local. Esto no confirma la versión instalada ni una demo integral.

Detalles del contrato observados en código:

- `POST /users/login`: cuerpo definido por `LoginSchema`: `mail`, `contrasena`, `device_id` obligatorio y `remember_me` opcional. Para 2FA, `/users/2fa/send` recibe `mail`, `device_id`, `pending_token`; `/users/2fa/verify` añade `codigo`. No publicar estos valores ni respuestas reales. Fuentes: `app/routes/user_routes.py`, `app/schemas/user_schema.py`.
- Las solicitudes protegidas del cliente web agregan `Authorization: Bearer …` y, si hay proyecto activo, `X-Project-Id`; `GET /projects` y `POST /projects/create` dependen de `require_admin`, mientras `GET /projects/{id}` requiere membresía y `PATCH /projects/{id}` administración del proyecto. Fuentes: `frontend/src/api.js`, `app/routes/project_routes.py`.
- Los códigos HTTP y respuestas concretas dependen de la ruta y el entorno; no se han observado aquí. El equipo debe verificar la documentación generada y los permisos del servicio efectivamente instalado antes de exponerlos como comprobados.

**Estado del criterio 12:** se aprobó el alcance presentado del README y la API. El README registra 36 pruebas backend aisladas, cobertura de 108/116 sentencias (93 %) de `auth.py`, 27 casos y 7/7 aserciones Postman contra una API parcial simulada. También registra 37 pruebas frontend y compilación en un árbol con cambios sin confirmar. Son resultados de otra ejecución, no cobertura general ni validación integral.

Siguen sin demostrarse la instalación limpia y la integración completa en el entorno de exposición. La aprobación no elimina esos límites. Los dos ciclos de corrección ya están documentados en [seguimiento de defectos](../sustentacion%20t6/seguimiento-defectos.md), en ramas separadas aún sin integrar a `main`.

## Historial de commits (criterio 13)

Ejemplos observados en el historial de FOCCUS, no creados para esta revisión:

| Tipo en mensaje | Commit | Descripción |
|---|---|---|
| Construcción | `7ff5143` | `feat(web): modulo Buscar codigo en el menu lateral del admin` |
| Corrección | `2397a2b` | `fix(web): completar correcciones y pruebas de requisitos funcionales` |
| Documentación | `9126d8f` | `Documentar consultas de pruebas de requisitos funcionales` |

Los prefijos ayudan a distinguir la intención, pero no prueban por sí solos un defecto, su issue o una reejecución. Hacia adelante, usar mensajes descriptivos y enlazar un issue real cuando exista; conservar la historia tal cual. Para acreditar ciclos de corrección se necesitan detección, commit específico y verificación documentada, no solo el nombre del commit.
