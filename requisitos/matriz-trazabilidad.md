# Matriz de trazabilidad RF ↔ HU ↔ Evidencia

Última revisión: 2026-11-20. La evidencia y los cambios de estado de esta pasada corresponden a web; móvil quedó fuera de alcance y no se validó, incluido el impacto del nuevo contrato 2FA.

Validación final: suite completa `python -m unittest discover -s tests -v` en `FOCCUS\backend\api_usuarios` (45/45); frontend `npm test` (10/10); `npm run build` correcto, con advertencia existente de chunk mayor a 500 kB. El lint focalizado de los archivos JS modificados pasó, incluido `npm exec eslint -- src/screen/Login.jsx`. La ejecución global de lint conserva 14 errores preexistentes en `Escena.jsx`, `Landing.jsx`, `Profile.jsx`, `ProjectRegistration.jsx` y `ProjectSelection.jsx`, archivos no modificados en esta pasada. Las pruebas son aisladas: no se probaron Flutter, BD real ni correo real.

| RF | HU | Evidencia principal | Estado |
|---|---|---|---|
| RF-01 | HU-01 | `POST /register` | ✅ |
| RF-02 | HU-02 | `POST /users/login` | ✅ |
| RF-03 | HU-03 | `/users/2fa/*`, `test_2fa.py` (HTTP aislado: 7/7, comunicado) | ✅ |
| RF-04 | HU-04 | `/users/recover-password`, `/reset-password` | ✅ |
| RF-05 | HU-05 | `POST /users/invite` | ✅ |
| RF-06 | HU-06 | `require_project_admin` / `require_project_member`; `test_project_resource_ownership.py` y pruebas de permisos | ✅ web |
| RF-07 | HU-07 | `DELETE /users/{id}/project/{id}` | ✅ |
| RF-08 | HU-08 | `DELETE /users/me/account` | ✅ |
| RF-09 | HU-09 | `/clients`, `Clients.jsx`, `test_clients.py` (3 pruebas aisladas aprobadas) | ✅ web |
| RF-10 | HU-10 | `PATCH /projects/{id}`; `test_project_resource_ownership.py` verifica que el administrador edita y persiste su proyecto, recibe 403 al editar otro y que el segundo permanece igual | ✅ web |
| RF-11 | HU-11 | `POST /projects/{id}/delete` | ✅ |
| RF-12 | HU-12 | `app/utils/auth.py`, `Roles.jsx`, controles de membresía y `test_project_resource_ownership.py` | ✅ web |
| RF-13 | HU-13 | `/guiones`, `/guiones/archivo`, `/guiones/texto` | ✅ |
| RF-14 | HU-14 | `/guiones/{id}/versiones` | ✅ |
| RF-15 | HU-15 | `GET`/`POST /guiones/versiones/{id}/notas`, `test_guion_notas.py` (5 pruebas aisladas aprobadas) | ✅ web |
| RF-16 | HU-16 | `DELETE /guiones/{id}` | ✅ |
| RF-17 | HU-17 | `/escenas` | ✅ |
| RF-18 | HU-18 | `/escenas/{id}/versiones`, subida de foto y lectura por miembro en `test_project_resource_ownership.py` (almacenamiento mockeado) | ✅ web |
| RF-19 | HU-19 | `/rodajes` | ✅ |
| RF-20 | HU-20 | `/rodajes/{id}/procesos`; PATCH exitoso y persistencia en `test_project_resource_ownership.py` | ✅ web |
| RF-21 | HU-21 | `POST /contact` | ✅ |
| RF-22 | HU-22 | `/projects/{id}/galeria` | ✅ |
| RF-23 | HU-23 | `/escenas/{id}/desglose/galeria` | ✅ |
| RF-24 | HU-24 | `/guiones/{id}/desglose` | ✅ |
| RF-25 | HU-25 | `/projects/{id}/rodajes/importar` | ✅ |
| RF-26, 27 | HU-26 | `Guion.jsx` (bloques `gb-*`, PDF) | ✅ web |
| RF-28 | HU-27 | `utils/codigos.py`, `CodigoChip.jsx` | ✅ |
| RF-29 | HU-27 | `utils/codigos.py`, `CodigoChip.jsx`, `test_codigos.py` (19 pruebas aisladas aprobadas, comunicado) | ✅ web |
| RF-30 | HU-28 | `GET /projects/{id}/buscar-codigo` | ✅ |
| varios | HU-29 | app Flutter | 🟡 |
