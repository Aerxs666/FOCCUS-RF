# Guion de demo integral T6

**Estado: no ejecutada en esta revisión.** Es una propuesta, no un registro de pruebas ni un resultado aprobado. Usar solo un entorno y datos ficticios autorizados; no publicar accesos ni identificadores reales.

## Preparación

- Confirmar qué revisiones del backend y frontend están instaladas y corresponden a lo que se mostrará. El código del repositorio no demuestra por sí solo qué está desplegado.
- Disponer de un proyecto ficticio desechable y una cuenta autorizada; no incluir contraseñas ni datos de acceso en esta guía. Confirmar que BD y correo estén disponibles sin mostrar datos sensibles.
- Si se incluye móvil, identificar la versión instalada y dispositivo, comprobar conexión y compatibilidad con el backend, en particular login y 2FA. La rama `mobile` observada no acredita la aplicación instalada. Si no se verifica, informar «móvil pendiente», no simular su éxito.
- No realizar migraciones, borrados ni operaciones destructivas durante la demo. La tabla del catálogo se reportó aplicada en Aiven, pero un volumen Docker nuevo no la incorpora automáticamente. Comprobar el entorno y el flujo antes de depender de él; ver [cierre](cierre-t6.md).

## Recorrido propuesto

Ejemplo totalmente ficticio: proyecto **«Corto Horizonte»**, guion **«Una mañana»**, escena **«INT. ESTUDIO - DÍA»**, objeto **«Cuaderno azul»**, jornada **«Día 1»**. Los nombres son ejemplos, no datos de la BD.

| Paso | Acción de exposición | Qué se espera mostrar, sin resultado aún |
|---|---|---|
| 1 | Iniciar sesión y completar 2FA. | Acceso al espacio de trabajo tras autenticación; correo disponible. |
| 2 | Seleccionar el proyecto ficticio. | Pantalla del proyecto y sus módulos. |
| 3 | Abrir el guion ficticio y su escena. | Texto del guion y escena relacionada. |
| 4 | Mostrar la galería y el desglose de esa escena. | Ficha del objeto ficticio y requerimientos o vínculos disponibles. |
| 5 | Mostrar una jornada de rodaje y la escena asignada. | Relación entre planificación y escena. |
| 6 | Si la app móvil fue previamente verificada, abrir el mismo proyecto y consultar el guion o la escena. | Mismos datos desde el móvil; si no está verificado, indicar el pendiente. |
| 7 | Explicar el [diagrama](../diagramas/README.md#arquitectura) y el [cierre honesto](cierre-t6.md). | Qué componentes participaron y qué queda pendiente. |

Para un recorrido integral, los vínculos entre escena, desglose, galería y rodaje deben existir y mostrarse efectivamente. Si falta uno, detenerse y explicarlo; no afirmar éxito completo. Las pantallas figuran en `FOCCUS/frontend/src/routes.jsx`; las rutas de guion, escena, galería, desglose y rodaje están en `backend/api_usuarios/app/routes/`.

## Registro posterior, solo si se ejecuta

| Fecha y entorno | Revisiones realmente usadas | Pasos realizados | Resultado observado y evidencia no sensible | Pendiente |
|---|---|---|---|---|
| Sin ejecutar | Sin verificar | Ninguno | Ninguno | Todo el recorrido |

No completar esta tabla con resultados esperados como si fueran observados.
