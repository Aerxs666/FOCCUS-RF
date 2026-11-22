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

| ID | Requisito | Web | Móvil (histórico) |
|---|---|---|---|
| RF-01 | El sistema debe registrar una empresa junto con su primer usuario, que queda como Administrador | ✅ | — |
| RF-02 | El sistema debe permitir iniciar sesión con correo y contraseña | ✅ | ✅ |
| RF-03 | El sistema debe verificar la identidad mediante un código de un solo uso por correo y entregar el JWT de acceso solo tras verificarlo | ✅ | — |
| RF-04 | El sistema debe permitir recuperar el acceso con un código enviado al correo | ✅ | — |
| RF-05 | El sistema debe permitir al Administrador invitar usuarios a un proyecto asignándoles un rol | ✅ | — |
| RF-06 | El sistema debe reservar al Administrador la creación, edición y eliminación de datos del proyecto y permitir al Usuario solo su consulta | ✅ | ✅ |
| RF-07 | El sistema debe permitir al Administrador retirar a un usuario de un proyecto sin borrar su cuenta | ✅ | — |
| RF-08 | El sistema debe permitir a cada usuario eliminar su propia cuenta | ✅ | — |
| RF-09 | El sistema debe registrar, consultar, editar y eliminar clientes (empresas), sin permitir eliminar clientes con proyectos asociados | ✅ | — |
| RF-10 | El sistema debe registrar, consultar, editar y eliminar proyectos asociados a un cliente | ✅ | ✅ |
| RF-11 | El sistema debe permitir eliminar un proyecto junto con el contenido que dependa de él | ✅ | — |
| RF-12 | El sistema debe aplicar dos roles fijos por proyecto: Administrador (1001), que gestiona los datos, y Usuario (1005), de solo lectura; los valores legados 1002–1004 también deben ser de solo lectura | ✅ | ✅ |
| RF-13 | El sistema debe permitir crear un guion subiendo un archivo o escribiendo texto, y extraer su contenido para edición | ✅ | ✅ |
| RF-14 | El sistema debe generar una nueva versión del guion en cada edición, conservando el historial | ✅ | ✅ |
| RF-15 | El sistema debe permitir al Administrador agregar notas a una versión específica del guion y a los miembros consultarlas dentro del proyecto | ✅ | — |
| RF-16 | El sistema debe permitir eliminar un guion | ✅ | ✅ |
| RF-17 | El sistema debe permitir crear y gestionar escenas asociadas a un guion | ✅ | ✅ |
| RF-18 | El sistema debe permitir versionar la continuidad de una escena con fotos de vestuario, objetos y espacios | ✅ | — |
| RF-19 | El sistema debe permitir crear y gestionar un cronograma de rodaje por proyecto | ✅ | ✅ |
| RF-20 | El sistema debe permitir gestionar procesos o tareas dentro de un rodaje | ✅ | — |
| RF-21 | El sistema debe ofrecer un formulario de contacto público sin autenticación | ✅ | — |

## RF nuevos (RF-22 a RF-30)

| ID | Requisito | Web | Móvil (histórico) |
|---|---|---|---|
| RF-22 | El sistema debe permitir gestionar una galería del proyecto con personajes, lugares, objetos y vestuario, con fotos y versiones | ✅ | ✅ |
| RF-23 | El sistema debe permitir vincular elementos de la galería a escenas y registrar su uso | ✅ | ✅ |
| RF-24 | El sistema debe permitir generar el desglose de producción de un guion (requerimientos por escena) e importarlo | ✅ | ✅ |
| RF-25 | El sistema debe permitir importar las escenas de un guion a un rodaje y asignarlas a jornadas | ✅ | ✅ |
| RF-26 | El sistema debe permitir escribir el guion por bloques tipados (escena, acción, personaje, paréntesis, diálogo, transición) con formato de la industria | ✅ | — |
| RF-27 | El sistema debe permitir exportar el guion a PDF en formato profesional (Carta, Courier 12, portada, paginación) | ✅ | — |
| RF-28 | El sistema debe asignar un código único legible (`TIPO-001`) a proyectos, guiones, versiones, escenas, personajes, lugares, objetos, vestuario y jornadas | ✅ | ✅ |
| RF-29 | El sistema debe mostrar el código copiable solo al Administrador, en el módulo de cada elemento | ✅ | ✅ |
| RF-30 | El sistema debe permitir al Administrador buscar un elemento por su código y abrir su ficha | ✅ | ✅ |

Para consultar el alcance de la revisión, la evidencia disponible, sus límites y las pruebas pendientes, véase el [informe de revisión](informe-revision.md).
