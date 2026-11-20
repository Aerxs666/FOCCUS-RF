# Informe de revisión de RF y HU

Fecha: 2026-11-20.

## Alcance y fuentes

Esta revisión incorpora la evidencia web de `docs/agentes/GUIA_PRUEBAS_RF.md` del repositorio FOCCUS y las correcciones del commit `2397a2b`. Los símbolos de implementación de RF y HU no significan aprobación integral. **Móvil quedó fuera de alcance**: sus estados anteriores y el impacto del contrato 2FA no se validaron.

La guía registra comprobaciones puntuales con aplicación, API, BD y correo reales, además de pruebas aisladas. Son evidencia parcial de los casos descritos, no una validación de todos los recorridos ni de todos los servicios. La última ejecución local indicada en la guía pasó 80 pruebas aisladas de backend y 16 de frontend; el frontend compiló y el análisis de los archivos web modificados no reportó errores.

En una ejecución anterior se comunicaron 45 pruebas de backend y 10 de frontend, compilación correcta con advertencia de tamaño de chunk y lint focalizado aprobado. El lint global conservaba 14 errores preexistentes en `Escena.jsx`, `Landing.jsx`, `Profile.jsx`, `ProjectRegistration.jsx` y `ProjectSelection.jsx`; esta revisión no confirma su estado actual.

## Decisión sobre roles: RF-06 y RF-12

- Los roles son fijos por proyecto: Administrador (`1001`) gestiona sus datos y Usuario (`1005`) los consulta; los valores legados `1002–1004` deben ser de solo lectura. No se requiere un catálogo jerárquico configurable. Las acciones personales sobre perfil y cuenta quedan fuera de esta restricción.
- `app/utils/auth.py` contiene controles de membresía y administración. La auditoría comunicada indicó que las escrituras de proyecto requieren `require_project_admin` y que las rutas restantes con `require_project_member` son GET. Las pruebas aisladas cubren pertenencia de recursos, creación con proyecto ajeno, edición de proceso y lectura de una foto con almacenamiento simulado.
- Con dos cuentas y proyectos de prueba se rechazó el acceso a un proyecto ajeno y a un guion y sus versiones mediante el proyecto propio. Un miembro pudo leer una nota y una imagen, pero recibió 403 al crear una nota y buscar un código. **Faltan otros recursos y operaciones por rol**; no se extrapola a Flutter.

## Comprobaciones y correcciones recientes

| RF / HU | Evidencia y resultado | Límite o pendiente |
|---|---|---|
| RF-03 / HU-03 | `test_2fa.py`: 7 pruebas HTTP aisladas comunicadas; el acceso se entrega tras verificar el código. | Prueba aislada, no validación integral de todos los casos de correo. |
| RF-04 y RF-05 / HU-04 y HU-05 | La invitación inicial creó el miembro pero notificó cero correos enviados. Después se recuperó su acceso por correo. Se corrigió el cierre SMTP tras una desconexión observada. | No se identificó con certeza la causa original ni se probó una invitación nueva. La llegada de un correo sin identificar no demuestra su recepción. |
| RF-09 / HU-09 | `Clients.jsx`, endpoints `/clients` y tres pruebas SQLite aisladas comunicadas. | No se atribuye una prueba integral del CRUD en BD real. |
| RF-10 y RF-11 / HU-10 y HU-11 | Proyecto de demostración creado; proyecto desechable eliminado por API y ausencia de recursos y archivos comprobada. La prueba aislada de PATCH cubre edición propia y rechazo de proyecto ajeno. | Falta confirmación gráfica de la eliminación; no se hizo respaldo antes del borrado registrado. |
| RF-13 a RF-15 / HU-13 a HU-15 | PDF con texto, DOCX y FDX sintéticos se importaron por interfaz y se leyeron; el DOCX se reabrió tras recargar. Se comprobaron contenido y nota en versiones distintas; un miembro leyó la nota y recibió 403 al crearla. | Son ejemplos mínimos; faltan documentos complejos y PDF escaneados. No se comprobó OCR. |
| RF-16 / HU-16 | Se corrigió la limpieza de dependencias, códigos y archivos. Las pruebas aisladas incluyen desgloses compartidos y fallos de limpieza de códigos. Se eliminó por API un guion desechable y se comprobó la ausencia de sus dependencias y carpeta. | Falta confirmación gráfica; no se hizo respaldo antes del borrado registrado. |
| RF-18, RF-20, RF-22 y RF-23 / HU-18, HU-20, HU-22 y HU-23 | Una imagen temporal de continuidad se volvió a abrir y un miembro la cargó; una edición de proceso persistió; se comprobó una ficha de galería, su escena y una versión de uso. | Faltan tipos de foto, variantes y más pruebas de permisos. |
| RF-24 y RF-25 / HU-24 y HU-25 | Se corrigieron casos de encabezados y fechas de PDF. Dos importaciones sintéticas por aplicación crearon una escena con tres requerimientos y una jornada con esa escena; la jornada persistió tras recargar. | Faltan documentos reales complejos y OCR. La reimportación puede modificar escenas o requerimientos: usar recursos desechables. |
| RF-27 / HU-26 | Se corrigió el manejador de exportación. Se descargaron dos versiones y se comprobó contenido diferencial; en una se revisaron portada, encabezados, Carta y Courier. jsPDF real se probó aisladamente con texto multipágina, Courier 12 y numeración. | La prueba aislada no cubrió márgenes ni descarga; faltan otros casos de formato y paginación. |
| RF-29 y RF-30 / HU-27 y HU-28 | Se ajustó la omisión de `codigo` cuando no existe código de personaje o lugar. Un administrador buscó un código de escena; un miembro recibió 403 y no recibió códigos en respuestas de guiones y galería. | Faltan comprobar los demás módulos y más operaciones. |

## Pendientes y precauciones

1. Ejecutar y registrar los casos pendientes de la guía con fecha, resultado y evidencia sin datos sensibles; no presentar las comprobaciones parciales como aprobación completa.
2. Para pruebas destructivas futuras, acordar previamente un respaldo verificable de BD y archivos, y usar recursos desechables; no eliminar el proyecto de exposición.
3. Verificar servicios y buzones antes de la exposición. Completar criterios de aceptación, prioridades y casos de prueba trazables.
4. Mantener como pendientes técnicos los archivos en la nube, la unificación de `apiFetch` y la deuda de estilos. Revisar móvil y el impacto de 2FA cuando entre en alcance.
