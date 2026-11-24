# Deuda técnica priorizada para T6

Prioridad propuesta por riesgo para la exposición y el producto; no fija responsables ni fechas. Actualización documental del 2026-11-22, sin pruebas ni conexión a BD.

| Prioridad | Deuda y riesgo | Evidencia verificable | Siguiente decisión o evidencia requerida |
|---|---|---|---|
| Alta | Compatibilidad móvil con login/2FA y otros contratos: puede impedir el recorrido integrado. | `FOCCUS/docs/agentes/CAMBIOS_WEB.md` registra adaptación pendiente; `mobile` está en otra rama. | Revisar versión instalada, adaptar cuando se solicite y comprobar flujo con backend correspondiente. No se validó móvil aquí. |
| Alta | El catálogo depende de la tabla y la versión disponibles en cada entorno. Un volumen Docker nuevo no la incorpora automáticamente. | [Commit `60e43ad`](https://github.com/Cr4ckJu4nF3/FOCCUS/commit/60e43ad), [registro web](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/docs/agentes/CAMBIOS_WEB.md) y [guía Docker](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/docs/DOCKER_LOCAL.md). | Confirmar la versión y probar el flujo en el entorno autorizado. Coordinar con BD cualquier migración, respaldo y restauración necesarios. |
| Alta | Las pruebas parciales no acreditan el sistema entero. | [Evidencia T6](../sustentacion%20t6/README.md) y [plan de pruebas](../sustentacion%20t6/plan-pruebas.md). | Ejecutar y registrar los recorridos pendientes, incluida la demo integral. Los dos ciclos documentados siguen en ramas separadas. |
| Media | Archivos subidos en disco local: pérdida o despliegue en otra instancia puede afectar disponibilidad. | `FOCCUS/backend/api_usuarios/app/main.py` monta `/assets`; `app/utils/file_storage.py`. | Definir estrategia de almacenamiento y recuperación; no afirmar que ya existe almacenamiento en nube. |
| Media | Integración HTTP y manejo de errores distribuidos en frontend. | `FOCCUS/frontend/src/api.js`; el [informe](../requisitos/informe-revision.md) deja pendiente unificar `apiFetch`. | Inventariar usos y priorizar una unificación compatible sin afirmar que está terminada. |
| Media | Deuda de estilos y lint: puede dificultar mantenimiento. | El [informe](../requisitos/informe-revision.md) conserva una ejecución anterior; el usuario comunica que la última publicación reportó 14 errores preexistentes. No se ejecutó lint en esta revisión. | Confirmar y abordar los errores cuando corresponda. El criterio 14 no se realizará, sin afirmar una exención oficial. |

El [cierre](cierre-t6.md) separa las decisiones tomadas de los puntos pendientes.
