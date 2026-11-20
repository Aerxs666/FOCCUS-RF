# Informe de revisión de RF y HU

Fecha: 2026-11-20.

## Alcance de esta pasada

Se actualizaron los requisitos y su trazabilidad con la decisión de alcance y la evidencia web final.

**Móvil quedó fuera de alcance por petición de la usuaria.** La columna móvil no se validó y sus estados anteriores se conservaron; tampoco se revisó el impacto del nuevo contrato 2FA en la aplicación móvil. No se probaron BD real ni correo real.

## Decisión sobre roles: RF-06 y RF-12

- Hay dos roles fijos por proyecto: **Administrador** (`id_rol` 1001), que gestiona los datos del proyecto, y **Usuario** (`id_rol` 1005), que solo los consulta. Los valores legados 1002–1004 deben ser de solo lectura.
- No se requiere un catálogo jerárquico configurable. Las acciones personales sobre perfil y cuenta quedan fuera de los permisos sobre datos del proyecto.
- `app/utils/auth.py` contiene controles de membresía y administración por proyecto. Según la auditoría de rutas comunicada, las escrituras del proyecto requieren `require_project_admin`; las rutas restantes con `require_project_member` son GET. La creación de notas exige administrador y su consulta permite miembros.
- El cierre web incluye validaciones de pertenencia recurso→proyecto. `test_project_resource_ownership.py` cubre aislamiento de IDs de recursos por proyecto (incluidos personajes y escenarios), rechazo al crear con un `id_project` ajeno, PATCH exitoso de un proceso con persistencia y subida de foto con `guardar_archivo` mockeado, seguida de lectura por un miembro.
- RF-06/HU-06, RF-12/HU-12, RF-18/HU-18 y RF-20/HU-20 quedan **cumplidos en web** conforme al código y evidencia aislada comunicada. No se extrapola ese resultado a móvil ni a servicios reales. La ausencia de filas en `roles` no prueba ni impide por sí sola el cumplimiento de los roles fijos.

## Validación final comunicada

- Backend: suite completa `python -m unittest discover -s tests -v` en `FOCCUS\backend\api_usuarios`: **45/45**.
- Frontend: `npm test`: **10/10**; `npm run build`: correcto, con advertencia existente de chunk mayor a 500 kB.
- El lint focalizado de los archivos JS modificados pasó, incluido `npm exec eslint -- src/screen/Login.jsx`. La ejecución global actual conserva 14 errores preexistentes en `Escena.jsx`, `Landing.jsx`, `Profile.jsx`, `ProjectRegistration.jsx` y `ProjectSelection.jsx`, archivos no modificados en esta pasada. No se corrigieron ni se atribuyen a esta pasada esos issues preexistentes.
- El aislamiento de las pruebas no representa una verificación de integración con BD o correo reales. Flutter no se probó.

## Comprobaciones y cambios

| Requisito | Evidencia y resultado | Límite o pendiente |
|---|---|---|
| RF-03 / HU-03 | No se entrega JWT de acceso antes de verificar el OTP; `backend/api_usuarios/tests/test_2fa.py`: 7/7 pruebas HTTP aisladas aprobadas, según el resultado comunicado. | Dependencias simuladas; no equivale a verificar correo y BD reales. |
| RF-09 / HU-09 | `Clients.jsx` implementa la pantalla CRUD y existen endpoints `/clients`. `test_clients.py`: 3 pruebas SQLite aisladas aprobadas sobre correo normalizado/duplicado, bloqueo de borrado con proyectos asociados y propagación de errores de integridad no relacionados con correo. | No se atribuye una prueba integral del CRUD en BD real. |
| RF-10 / HU-10 | `EditProjectModal.jsx` permite editar el proyecto activo con `PATCH /projects/{id}`. `test_project_resource_ownership.py` verifica por HTTP aislado que un administrador edita y persiste su propio proyecto, recibe 403 al editar otro y que el proyecto ajeno permanece sin cambios. | Prueba aislada; no equivale a integración con BD real. |
| RF-15 / HU-15 | `GET` y `POST /guiones/versiones/{id}/notas`; `test_guion_notas.py`: 5 pruebas aisladas aprobadas. El código exige administrador para crear y permite a miembros consultar, con aislamiento por proyecto y versión. | Las pruebas aisladas no equivalen a comprobar la BD real. |
| RF-29 / HU-27 | La prueba previa `test_galeria_solo_objetos` fallaba al aparecer `codigo: null` en un elemento sin ficha vinculada. `app/utils/codigos.py` ahora omite la propiedad cuando no hay código de personaje o lugar; se comunicaron 19 pruebas aprobadas de `test_codigos.py`. | Son pruebas aisladas; no prueban comportamiento en BD real. |
| RF-06, RF-12 / HU-06, HU-12 | `test_project_resource_ownership.py` cubre aislamiento de IDs de recursos entre proyectos, incluidos personajes y escenarios, y creación con `id_project` ajeno. | Suite aislada; no se probó BD real ni Flutter. |
| RF-18 / HU-18 | `test_project_resource_ownership.py` sube una foto (mock solo de `guardar_archivo`) y permite leerla como miembro. | No prueba almacenamiento externo ni correo/BD reales. |
| RF-20 / HU-20 | `test_project_resource_ownership.py` verifica PATCH de proceso exitoso y persistencia. | Prueba aislada; no equivale a integración con BD real. |

## Pendientes generales

1. Completar criterios de aceptación, prioridades y casos de prueba trazables para los RF.
2. Mantener como pendientes técnicos los archivos en la nube, la unificación de `apiFetch` y la deuda de estilos. Los estados móviles históricos y el impacto móvil del nuevo contrato 2FA no se validaron.

## Riesgos para la exposición

- Verificar previamente la disponibilidad del backend, la BD y el envío de correo.
- No presentar los resultados de pruebas aisladas como una verificación integral contra BD o correo reales.
- El build conserva una advertencia de chunk mayor a 500 kB. El lint focalizado de los archivos JS modificados, incluido `Login`, pasó; el lint global conserva 14 errores preexistentes en los archivos citados.
