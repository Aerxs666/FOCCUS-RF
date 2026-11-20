# FOCCUS — Requisitos Funcionales (RF)

Última revisión: 2026-11-20. Estados: ✅ implementado · 🟡 parcial · 🔲 pendiente.
"Web" = frontend React + backend FastAPI. "Móvil" = app Flutter (rama `mobile` del repo de código).
Móvil quedó fuera de alcance por petición de la usuaria: no se validó la columna y se conservan sus estados anteriores. El impacto del nuevo contrato 2FA en móvil tampoco se revisó.
Los símbolos indican estado de implementación, **no aprobación integral de las pruebas**. La evidencia y sus límites se detallan abajo y en el [informe](informe-revision.md).

## Actores

| Actor | Descripción |
|---|---|
| Visitante | Persona sin cuenta (landing, registro, contacto). |
| Administrador | Rol `id_rol` 1001 dentro de un proyecto. Crea, edita, borra, invita y ve los códigos. |
| Usuario | Rol `id_rol` 1005 dentro de un proyecto: consulta los datos del proyecto sin modificarlos. Los valores legados 1002–1004 deben ser de solo lectura. |

El alcance de roles afecta a los datos del proyecto, no a las acciones personales de perfil o cuenta.

## RF originales (RF-01 a RF-21)

| ID | Requisito | Web | Móvil |
|---|---|---|---|
| RF-01 | Registrar una empresa junto con su primer usuario, que queda como Administrador | ✅ | — |
| RF-02 | Iniciar sesión con correo y contraseña | ✅ | ✅ |
| RF-03 | El sistema debe verificar la identidad mediante un código de un solo uso por correo y entregar el JWT de acceso solo tras verificarlo | ✅ | por verificar |
| RF-04 | Recuperar el acceso con un código enviado al correo | ✅ | por verificar |
| RF-05 | El Administrador invita usuarios a un proyecto asignándoles un rol | ✅ | por verificar |
| RF-06 | El sistema debe reservar al Administrador la creación, edición y eliminación de datos del proyecto y permitir al Usuario solo su consulta | ✅ web (nota 1) | ✅ |
| RF-07 | El Administrador remueve a un usuario de un proyecto sin borrar su cuenta | ✅ | por verificar |
| RF-08 | Cualquier usuario elimina su propia cuenta | ✅ | por verificar |
| RF-09 | El sistema debe registrar, consultar, editar y eliminar clientes (empresas), sin permitir eliminar clientes con proyectos asociados | ✅ | — |
| RF-10 | El sistema debe registrar, consultar, editar y eliminar proyectos asociados a un cliente | ✅ | ✅ |
| RF-11 | Eliminar un proyecto junto con el contenido que dependa de él | ✅ | por verificar |
| RF-12 | El sistema debe aplicar dos roles fijos por proyecto: Administrador (1001), que gestiona los datos, y Usuario (1005), de solo lectura; los valores legados 1002–1004 también deben ser de solo lectura | ✅ web (nota 2) | ✅ |
| RF-13 | Crear un guion subiendo un archivo o escribiendo texto, y extraer su contenido para edición | ✅ (ver nota 3) | ✅ |
| RF-14 | Generar una nueva versión del guion en cada edición, conservando el historial | ✅ | ✅ |
| RF-15 | El sistema debe permitir al Administrador agregar notas a una versión específica del guion y a los miembros consultarlas dentro del proyecto | ✅ (ver nota 4) | por verificar |
| RF-16 | Eliminar un guion | ✅ | ✅ |
| RF-17 | Crear y gestionar escenas asociadas a un guion | ✅ | ✅ |
| RF-18 | Versionar la continuidad de una escena con fotos de vestuario, objetos y espacios | ✅ web (nota 5) | 🟡 |
| RF-19 | Crear y gestionar un cronograma de rodaje por proyecto | ✅ | ✅ |
| RF-20 | Gestionar procesos/tareas dentro de un rodaje | ✅ web (nota 1) | por verificar |
| RF-21 | Formulario de contacto público sin autenticación | ✅ | — |

## RF nuevos (RF-22 a RF-30)

| ID | Requisito | Web | Móvil |
|---|---|---|---|
| RF-22 | Gestionar una galería del proyecto con personajes, lugares, objetos y vestuario, con fotos y versiones | ✅ | ✅ |
| RF-23 | Vincular elementos de la galería a escenas y registrar su uso | ✅ | ✅ |
| RF-24 | Generar el desglose de producción de un guion (requerimientos por escena) e importarlo | ✅ | ✅ |
| RF-25 | Importar las escenas de un guion a un rodaje y asignar escenas a jornadas | ✅ | ✅ |
| RF-26 | Escribir el guion por bloques tipados (escena, acción, personaje, paréntesis, diálogo, transición) con formato de la industria | ✅ | 🟡 (lee por texto, falta `gb-*`) |
| RF-27 | Exportar el guion a PDF en formato profesional (Carta, Courier 12, portada, paginación) | ✅ | 🔲 |
| RF-28 | Asignar un código único legible (`TIPO-001`) a proyectos, guiones, versiones, escenas, personajes, lugares, objetos, vestuario y jornadas | ✅ | ✅ |
| RF-29 | Mostrar el código solo al Administrador, copiable, en el módulo de cada elemento | ✅ (ver nota 6) | ✅ |
| RF-30 | Buscar un elemento por su código (solo Administrador) y abrir su ficha | ✅ | ✅ |

## Notas

1. Los permisos son **por proyecto** (`require_project_admin` / `require_project_member`), no solo "Administrador global". Además de las pruebas aisladas de `test_project_resource_ownership.py`, se rechazó el acceso a un proyecto ajeno y a un guion y sus versiones desde otro proyecto; faltan otros recursos y operaciones por rol.
2. Son roles fijos, no un catálogo jerárquico configurable. La tabla `roles` vacía no demuestra por sí sola su cumplimiento o incumplimiento. Perfil y cuenta propios quedan fuera de esta restricción. Las comprobaciones con servicios reales son parciales y no validan todos los permisos.
3. Hoy hay tres entradas: `POST /guiones` (archivo), `/guiones/archivo` y `/guiones/texto`.
4. Notas: `POST` requiere administrador y `GET` permite consulta a miembros en `/guiones/versiones/{id}/notas`. Se guardó y volvió a abrir una nota, un miembro la leyó y su intento de crearla recibió 403; también se comprobó su separación entre dos versiones de prueba.
5. Se subió y volvió a abrir una imagen temporal de continuidad; un miembro pudo cargarla. Faltan más tipos y comprobaciones de permisos.
6. La prueba `test_galeria_solo_objetos` fallaba por `codigo: null` en un elemento sin ficha vinculada y se ajustó la respuesta. Un administrador buscó un código de escena; un Usuario recibió 403 al buscar y no recibió códigos en respuestas de guiones y galería. Faltan los demás módulos.

## Evidencia reciente y pruebas pendientes

Fuente: `docs/agentes/GUIA_PRUEBAS_RF.md` del repositorio FOCCUS y commit `2397a2b`. La guía registra **80 pruebas aisladas de backend y 16 de frontend**, compilación web correcta y análisis sin errores en los archivos web modificados. Los recorridos siguientes son parciales:

- **RF-04 y RF-05:** una invitación creó el miembro pero notificó cero correos enviados; después se recuperó el acceso por correo. Se corrigió el cierre SMTP tras una desconexión observada, sin identificar con certeza la causa original. Queda probar una invitación nueva y su recepción; la llegada de un correo sin identificar no demuestra ese caso.
- **RF-11 y RF-16:** se corrigió la limpieza al eliminar guiones. Se comprobó con datos y archivos aislados y con un guion desechable eliminado por API, incluida la ausencia de sus dependencias y carpeta. Un proyecto desechable también se eliminó por API. Falta confirmar ambos recorridos desde la interfaz; no se hizo respaldo antes de esos borrados.
- **RF-13 a RF-15:** se probaron importaciones mínimas de PDF con texto, DOCX y FDX en la interfaz; el DOCX se reabrió tras recargar. Se comprobaron contenido y nota en versiones diferentes. Faltan documentos complejos y PDF escaneados; no se comprobó OCR.
- **RF-18, RF-20, RF-22 y RF-23:** se volvió a abrir una foto temporal, se conservó una edición de proceso y se consultaron una ficha de galería, su vínculo a escena y una versión de uso. No cubren todas las variantes ni permisos.
- **RF-24 y RF-25:** se corrigieron casos de encabezados y fechas de PDF. Dos PDF sintéticos importados en la aplicación crearon una escena con tres requerimientos y una jornada con esa escena; la jornada persistió tras recargar. Faltan documentos reales complejos y OCR; la reimportación puede modificar datos, por lo que debe probarse con recursos desechables.
- **RF-27:** se corrigió el manejador que impedía exportar pese a existir texto. Se descargaron dos versiones y se comprobó su contenido diferencial; en una se revisaron portada, encabezados, tamaño Carta y Courier. Una prueba aislada con jsPDF real cubrió texto sintético multipágina, Courier 12 y numeración, no márgenes ni descarga. Faltan casos de formato y paginación.
