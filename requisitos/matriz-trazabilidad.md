# Matriz de trazabilidad RF ↔ HU ↔ Evidencia

| RF | HU | Evidencia principal | Estado |
|---|---|---|---|
| RF-01 | HU-01 | `POST /register` | ✅ |
| RF-02 | HU-02 | `POST /users/login` | ✅ |
| RF-03 | HU-03 | `/users/2fa/*` | ✅ |
| RF-04 | HU-04 | `/users/recover-password`, `/reset-password` | ✅ |
| RF-05 | HU-05 | `POST /users/invite` | ✅ |
| RF-06 | HU-06 | `require_project_admin`, `require_project_member` | ✅ |
| RF-07 | HU-07 | `DELETE /users/{id}/project/{id}` | ✅ |
| RF-08 | HU-08 | `DELETE /users/me/account` | ✅ |
| RF-09 | HU-09 | `/clients` | ✅ |
| RF-10 | HU-10 | `/projects` | ✅ |
| RF-11 | HU-11 | `POST /projects/{id}/delete` | ✅ |
| RF-12 | HU-12 | `/roles` | 🟡 |
| RF-13 | HU-13 | `/guiones`, `/guiones/archivo`, `/guiones/texto` | ✅ |
| RF-14 | HU-14 | `/guiones/{id}/versiones` | ✅ |
| RF-15 | HU-15 | `/guiones/versiones/{id}/notas` | 🟡 |
| RF-16 | HU-16 | `DELETE /guiones/{id}` | ✅ |
| RF-17 | HU-17 | `/escenas` | ✅ |
| RF-18 | HU-18 | `/escenas/{id}/versiones` | 🟡 |
| RF-19 | HU-19 | `/rodajes` | ✅ |
| RF-20 | HU-20 | `/rodajes/{id}/procesos` | 🟡 |
| RF-21 | HU-21 | `POST /contact` | ✅ |
| RF-22 | HU-22 | `/projects/{id}/galeria` | ✅ |
| RF-23 | HU-23 | `/escenas/{id}/desglose/galeria` | ✅ |
| RF-24 | HU-24 | `/guiones/{id}/desglose` | ✅ |
| RF-25 | HU-25 | `/projects/{id}/rodajes/importar` | ✅ |
| RF-26, 27 | HU-26 | `Guion.jsx` (bloques `gb-*`, PDF) | ✅ web |
| RF-28, 29 | HU-27 | `utils/codigos.py`, `CodigoChip.jsx` | ✅ |
| RF-30 | HU-28 | `GET /projects/{id}/buscar-codigo` | ✅ |
| varios | HU-29 | app Flutter | 🟡 |
