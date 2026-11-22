# Matriz de trazabilidad RF ↔ HU ↔ Evidencia

Última revisión: 2026-11-20. La evidencia y los cambios de estado de esta pasada corresponden a web; móvil quedó fuera de alcance y no se validó, incluido el impacto del nuevo contrato 2FA.

Actualización documental del 2026-11-22: el [commit `60e43ad` de FOCCUS](https://github.com/Cr4ckJu4nF3/FOCCUS/commit/60e43ad) incorpora catálogo de bloques y gestión de escenas. El [registro web](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/docs/agentes/CAMBIOS_WEB.md) informa que el catálogo se aplicó en Aiven; el registro local de `foccus-bd` añade la verificación de su estructura. No se consultó la BD en esta revisión. La [guía Docker](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/docs/DOCKER_LOCAL.md) registra pruebas aisladas y aclara que un volumen nuevo no incluye la migración automáticamente. Esto no demuestra una demo integral ni cambia los estados históricos de la tabla. Móvil sigue sin validar.

La guía `FOCCUS/docs/agentes/GUIA_PRUEBAS_RF.md` registra 80 pruebas aisladas de backend y 16 de frontend, compilación web correcta y análisis sin errores en los archivos web modificados. También registra comprobaciones puntuales con aplicación, API, BD y correo reales. El estado ✅ indica implementación, **no aprobación integral**; los límites se detallan en el [informe](informe-revision.md). Flutter no se probó.

| RF | HU | Evidencia principal | Estado |
|---|---|---|---|
| RF-01 | HU-01 | `POST /register` | ✅ |
| RF-02 | HU-02 | `POST /users/login` | ✅ |
| RF-03 | HU-03 | `/users/2fa/*`, `test_2fa.py` (HTTP aislado: 7/7, comunicado) | ✅ |
| RF-04 | HU-04 | `/users/recover-password`, `/reset-password`; una recuperación por correo comprobada | ✅; cobertura parcial |
| RF-05 | HU-05 | `POST /users/invite`; invitación inicial creó miembro pero informó cero correos enviados; cierre SMTP corregido | ✅; invitación nueva pendiente, causa original no identificada |
| RF-06 | HU-06 | `require_project_admin` / `require_project_member`; pruebas aisladas y rechazo de acceso a proyecto y guion ajenos en casos reales | ✅ web; faltan recursos y operaciones |
| RF-07 | HU-07 | `DELETE /users/{id}/project/{id}` | ✅ |
| RF-08 | HU-08 | `DELETE /users/me/account` | ✅ |
| RF-09 | HU-09 | `/clients`, `Clients.jsx`, `test_clients.py` (3 pruebas aisladas aprobadas) | ✅ web |
| RF-10 | HU-10 | `PATCH /projects/{id}`; `test_project_resource_ownership.py` verifica que el administrador edita y persiste su proyecto, recibe 403 al editar otro y que el segundo permanece igual | ✅ web |
| RF-11 | HU-11 | `POST /projects/{id}/delete`; proyecto desechable y dependencias eliminados por API | ✅; confirmación gráfica pendiente |
| RF-12 | HU-12 | `app/utils/auth.py`, `Roles.jsx`, controles de membresía y `test_project_resource_ownership.py` | ✅ web |
| RF-13 | HU-13 | `/guiones`, `/guiones/archivo`, `/guiones/texto`; importaciones sintéticas mínimas PDF, DOCX y FDX por interfaz | ✅; faltan documentos complejos y OCR |
| RF-14 | HU-14 | `/guiones/{id}/versiones`; contenido y nota comprobados en versiones distintas | ✅; comprobación parcial |
| RF-15 | HU-15 | `GET`/`POST /guiones/versiones/{id}/notas`; nota persistida, leída por miembro y POST rechazado para este | ✅ web; comprobación parcial |
| RF-16 | HU-16 | `DELETE /guiones/{id}`; limpieza corregida y comprobada con pruebas aisladas y borrado desechable por API | ✅; confirmación gráfica pendiente |
| RF-17 | HU-17 | `/escenas` | ✅ |
| RF-18 | HU-18 | `/escenas/{id}/versiones`; imagen temporal subida, abierta de nuevo y cargada por miembro | ✅ web; faltan tipos y permisos |
| RF-19 | HU-19 | `/rodajes` | ✅ |
| RF-20 | HU-20 | `/rodajes/{id}/procesos`; PATCH aislado y edición conservada al volver a abrir proceso | ✅ web; comprobación parcial |
| RF-21 | HU-21 | `POST /contact` | ✅ |
| RF-22 | HU-22 | `/projects/{id}/galeria`; ficha y versión de uso consultadas | ✅; comprobación parcial |
| RF-23 | HU-23 | `/escenas/{id}/desglose/galeria`; vínculo de ficha a escena comprobado | ✅; comprobación parcial |
| RF-24 | HU-24 | `/guiones/{id}/desglose`, `/guiones/{id}/desglose/importar`; PDF sintético generó escena y tres requerimientos | ✅; faltan documentos complejos y OCR |
| RF-25 | HU-25 | `/projects/{id}/rodajes/importar`; PDF sintético creó jornada y asignó escena; persistió al recargar | ✅; faltan documentos complejos y OCR |
| RF-26, 27 | HU-26 | `Guion.jsx` (bloques `gb-*`, PDF); descarga de dos versiones y prueba aislada multipágina con jsPDF | ✅ web; faltan casos de formato y paginación |
| RF-28 | HU-27 | `utils/codigos.py`, `CodigoChip.jsx` | ✅ |
| RF-29 | HU-27 | `utils/codigos.py`, `CodigoChip.jsx`; respuestas de guiones y galería sin códigos para miembro | ✅ web; faltan otros módulos |
| RF-30 | HU-28 | `GET /projects/{id}/buscar-codigo`; administrador abrió una escena y miembro recibió 403 | ✅; comprobación parcial |
| varios | HU-29 | app Flutter | 🟡 |
