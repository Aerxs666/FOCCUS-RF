# FOCCUS — Requisitos Funcionales (RF)

Última revisión: 2026-11-20. En las columnas de estado, ✅ indica el estado registrado; — indica que no se muestra ✅. Móvil quedó fuera de alcance en esta revisión: sus estados no se validaron y el impacto del contrato 2FA tampoco se revisó. Los símbolos no representan aprobación integral de las pruebas. El alcance, la evidencia y sus límites se detallan en el [informe de revisión](informe-revision.md).

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
| RF-03 | El sistema debe verificar la identidad mediante un código de un solo uso por correo y entregar el JWT de acceso solo tras verificarlo | ✅ | — |
| RF-04 | Recuperar el acceso con un código enviado al correo | ✅ | — |
| RF-05 | El Administrador invita usuarios a un proyecto asignándoles un rol | ✅ | — |
| RF-06 | El sistema debe reservar al Administrador la creación, edición y eliminación de datos del proyecto y permitir al Usuario solo su consulta | ✅ | ✅ |
| RF-07 | El Administrador remueve a un usuario de un proyecto sin borrar su cuenta | ✅ | — |
| RF-08 | Cualquier usuario elimina su propia cuenta | ✅ | — |
| RF-09 | El sistema debe registrar, consultar, editar y eliminar clientes (empresas), sin permitir eliminar clientes con proyectos asociados | ✅ | — |
| RF-10 | El sistema debe registrar, consultar, editar y eliminar proyectos asociados a un cliente | ✅ | ✅ |
| RF-11 | Eliminar un proyecto junto con el contenido que dependa de él | ✅ | — |
| RF-12 | El sistema debe aplicar dos roles fijos por proyecto: Administrador (1001), que gestiona los datos, y Usuario (1005), de solo lectura; los valores legados 1002–1004 también deben ser de solo lectura | ✅ | ✅ |
| RF-13 | Crear un guion subiendo un archivo o escribiendo texto, y extraer su contenido para edición | ✅ | ✅ |
| RF-14 | Generar una nueva versión del guion en cada edición, conservando el historial | ✅ | ✅ |
| RF-15 | El sistema debe permitir al Administrador agregar notas a una versión específica del guion y a los miembros consultarlas dentro del proyecto | ✅ | — |
| RF-16 | Eliminar un guion | ✅ | ✅ |
| RF-17 | Crear y gestionar escenas asociadas a un guion | ✅ | ✅ |
| RF-18 | Versionar la continuidad de una escena con fotos de vestuario, objetos y espacios | ✅ | — |
| RF-19 | Crear y gestionar un cronograma de rodaje por proyecto | ✅ | ✅ |
| RF-20 | Gestionar procesos/tareas dentro de un rodaje | ✅ | — |
| RF-21 | Formulario de contacto público sin autenticación | ✅ | — |

## RF nuevos (RF-22 a RF-30)

| ID | Requisito | Web | Móvil |
|---|---|---|---|
| RF-22 | Gestionar una galería del proyecto con personajes, lugares, objetos y vestuario, con fotos y versiones | ✅ | ✅ |
| RF-23 | Vincular elementos de la galería a escenas y registrar su uso | ✅ | ✅ |
| RF-24 | Generar el desglose de producción de un guion (requerimientos por escena) e importarlo | ✅ | ✅ |
| RF-25 | Importar las escenas de un guion a un rodaje y asignar escenas a jornadas | ✅ | ✅ |
| RF-26 | Escribir el guion por bloques tipados (escena, acción, personaje, paréntesis, diálogo, transición) con formato de la industria | ✅ | — |
| RF-27 | Exportar el guion a PDF en formato profesional (Carta, Courier 12, portada, paginación) | ✅ | — |
| RF-28 | Asignar un código único legible (`TIPO-001`) a proyectos, guiones, versiones, escenas, personajes, lugares, objetos, vestuario y jornadas | ✅ | ✅ |
| RF-29 | Mostrar el código solo al Administrador, copiable, en el módulo de cada elemento | ✅ | ✅ |
| RF-30 | Buscar un elemento por su código (solo Administrador) y abrir su ficha | ✅ | ✅ |

Para consultar el alcance de la revisión, la evidencia disponible, sus límites y las pruebas pendientes, véase el [informe de revisión](informe-revision.md).
