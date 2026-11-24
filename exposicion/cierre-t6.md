# Cierre T6: visión para exposición

Actualización documental: 2026-11-22. Esta guía prepara la exposición; no es una calificación ni demuestra una demo integral.

Actualización del 2026-11-24: [mejoras de interfaz `9141a3f`](https://github.com/Cr4ckJu4nF3/FOCCUS/commit/9141a3f) y [editor de guion `48a844c`](https://github.com/Cr4ckJu4nF3/FOCCUS/commit/48a844c) publicadas en FOCCUS. La [demo propuesta](demo-t6.md) incorpora el nuevo flujo; no se ejecutó aquí. Según lo comunicado por el usuario, la última publicación reportó 55 pruebas frontend y compilación correctas, con 14 errores de lint preexistentes; no son resultados ejecutados en esta revisión. La versión instalada para exposición sigue sin comprobar.

## Alcance y versión

- FOCCUS web reúne autenticación, proyectos, guion, escenas, galería, desglose y rodaje. Hay implementación y comprobaciones puntuales anteriores, no una aceptación integral: ver [matriz](../requisitos/matriz-trazabilidad.md) e [informe](../requisitos/informe-revision.md).
- La revisión inicial partió de `main` en `9126d8f`. Después se publicaron, entre otros, el [catálogo y gestión de escenas](https://github.com/Cr4ckJu4nF3/FOCCUS/commit/60e43ad) y el [entorno Docker local](https://github.com/Cr4ckJu4nF3/FOCCUS/commit/93d57e6). No se identificó la revisión instalada para la exposición.
- Flutter figura en la rama `mobile`, revisión `98c6a42` observada; no se comprobó la versión instalada, el dispositivo, el inicio de sesión ni la integración. El reporte de cambios web identifica adaptaciones móviles pendientes, incluido el contrato de 2FA.
- El [registro web](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/docs/agentes/CAMBIOS_WEB.md) informa que la tabla del catálogo se aplicó en Aiven. La [guía Docker](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/docs/DOCKER_LOCAL.md) registra pruebas locales con datos ficticios; un volumen nuevo no incluye la migración automáticamente. Hay que comprobar el entorno de exposición antes de presentar el catálogo.

## Qué falta decidir o completar

| Tema | Estado para el cierre |
|---|---|
| Integración completa y demo | Guion preparado, **sin ejecutar** en esta revisión; web, correo, datos y móvil deben comprobarse en el entorno real de exposición. |
| Pruebas | El README de FOCCUS registra 36 pruebas backend aisladas, cobertura del 93 % solo de `auth.py`, 27 casos y 7/7 aserciones Postman contra una API parcial. También registra 37 pruebas frontend y compilación en un árbol con cambios sin confirmar. Son resultados de otra ejecución, no cobertura general. Los [dos ciclos de corrección](../sustentacion%20t6/seguimiento-defectos.md) están en ramas separadas, aún sin integrar. Faltan instalación limpia y demo integral. |
| API e instalación | Se aprobó el alcance presentado del README y la API. Un arranque aislado documentó `/docs` y `/openapi.json`, pero no demuestra una instalación limpia completa. Ver [API y commits](api-y-commits-t6.md). |
| Cuarto backend | Se acordó comparar la evolución de un backend; está pendiente que el instructor acepte esa adaptación al requisito original de cuatro. Ver [comparación](../sustentacion%20t6/requisito-15.md). |
| Calidad y deuda | La [deuda técnica](deuda-tecnica-t6.md) es una propuesta. Para el criterio 14 se decidió no realizar el trabajo; no se afirma una exención oficial. |

Se indicó que la adaptación y verificación móvil se orientan a T7. El alcance, las fechas y los demás temas pendientes deben concretarse; no se presenta esa orientación como aceptación de T6.

## Lectura de la lista

| Criterio | Avance documental | Pendiente |
|---|---|---|
| 1 | Esta visión de cierre separa lo observado de lo pendiente. | Equipo: definir alcance, responsables y decisión real de cierre. |
| 2 | En ClickUp se reconstruyeron períodos y tareas a partir de commits. Los sprints nativos siguen sin iniciar y sus fechas no son las históricas. | Comprobar dos retrospectivas con reflexión sobre pruebas; la reconstrucción no demuestra ceremonias reales. |
| 3 | Se confirmó el arranque y se aprobó explicar las responsabilidades del backend. Ver [recorrido](../sustentacion%20t6/backend-y-recorrido.md). | La interpretación de la comparación con backends anteriores corresponde al instructor. |
| 5 | Se aprobó la [arquitectura](../diagramas/README.md#arquitectura) y el recorrido explicado. | Ejecutar y registrar la [demo integral](demo-t6.md), incluida la parte móvil si se presenta. |
| 12 | Se aprobó el alcance presentado del [README y la API](api-y-commits-t6.md#api-e-instalación-criterio-12). | La instalación limpia y la integración completa no se han demostrado. |
| 13 | [Ejemplos reales de commits](api-y-commits-t6.md#historial-de-commits-criterio-13). | Vincular correcciones a defectos y verificaciones reales cuando existan; no alterar la historia. |
| 15 | [Deuda priorizada](deuda-tecnica-t6.md) y reflexión del backend. | Validar con instructor la comparación de cuatro y sus antecedentes. |

La [matriz completa de criterios](../sustentacion%20t6/README.md) conserva los estados y sus límites.

Fuente del instrumento: [lista de chequeo T6](https://github.com/ergrato-dev/checklist-proyectos-adso/blob/main/listas-de-chequeo/listas-oferta-abierta/t6/6t-lista-de-chequeo-oa.md).
