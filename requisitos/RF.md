# FOCCUS — Requisitos Funcionales (RF)

Última revisión: 2026-11-01. Estados: ✅ implementado · 🟡 parcial · 🔲 pendiente.
"Web" = frontend React + backend FastAPI. "Móvil" = app Flutter (rama `mobile` del repo de código).

## Actores

| Actor | Descripción |
|---|---|
| Visitante | Persona sin cuenta (landing, registro, contacto). |
| Administrador | Rol `id_rol` 1001 dentro de un proyecto. Crea, edita, borra, invita y ve los códigos. |
| Miembro | Usuario del proyecto con otro rol; consulta y aporta según su permiso (p. ej. galería). |

## RF originales (RF-01 a RF-21)

| ID | Requisito | Web | Móvil |
|---|---|---|---|
| RF-01 | Registrar una empresa junto con su primer usuario, que queda como Administrador | ✅ | — |
| RF-02 | Iniciar sesión con correo y contraseña | ✅ | ✅ |
| RF-03 | Verificar la identidad con un código de un solo uso por correo (2FA) tras el login | ✅ | por verificar |
| RF-04 | Recuperar el acceso con un código enviado al correo | ✅ | por verificar |
| RF-05 | El Administrador invita usuarios a un proyecto asignándoles un rol | ✅ | por verificar |
| RF-06 | Restringir la creación, edición y eliminación de datos según el rol en el proyecto (administrador / miembro) | ✅ (ver nota 1) | ✅ |
| RF-07 | El Administrador remueve a un usuario de un proyecto sin borrar su cuenta | ✅ | por verificar |
| RF-08 | Cualquier usuario elimina su propia cuenta | ✅ | por verificar |
| RF-09 | Registrar, consultar, editar y eliminar clientes (empresas) | ✅ | — |
| RF-10 | Registrar, consultar, editar y eliminar proyectos asociados a un cliente | ✅ | ✅ |
| RF-11 | Eliminar un proyecto junto con el contenido que dependa de él | ✅ | por verificar |
| RF-12 | Registrar, consultar, editar y eliminar roles con su nivel jerárquico | ✅ (ver nota 2) | ✅ |
| RF-13 | Crear un guion subiendo un archivo o escribiendo texto, y extraer su contenido para edición | ✅ (ver nota 3) | ✅ |
| RF-14 | Generar una nueva versión del guion en cada edición, conservando el historial | ✅ | ✅ |
| RF-15 | Agregar notas a una versión específica del guion | ✅ (ver nota 4) | por verificar |
| RF-16 | Eliminar un guion | ✅ | ✅ |
| RF-17 | Crear y gestionar escenas asociadas a un guion | ✅ | ✅ |
| RF-18 | Versionar la continuidad de una escena con fotos de vestuario, objetos y espacios | 🟡 (ver nota 5) | 🟡 |
| RF-19 | Crear y gestionar un cronograma de rodaje por proyecto | ✅ | ✅ |
| RF-20 | Gestionar procesos/tareas dentro de un rodaje | ✅ (ver nota 4) | por verificar |
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
| RF-29 | Mostrar el código solo al Administrador, copiable, en el módulo de cada elemento | ✅ | ✅ |
| RF-30 | Buscar un elemento por su código (solo Administrador) y abrir su ficha | ✅ | ✅ |

## Notas

1. Los permisos son **por proyecto** (`require_project_admin` / `require_project_member`), no solo "Administrador global". Hay que reflejarlo en la HU-06.
2. La tabla `roles` está vacía en la BD actual; el admin se identifica por `id_rol` 1001. Aclarar cómo se manejan los roles en la exposición.
3. Hoy hay tres entradas: `POST /guiones` (archivo), `/guiones/archivo` y `/guiones/texto`.
4. Las tablas `guion_nota` y `proceso_rodaje` tienen 0 filas: la función existe pero no hay datos de ejemplo. Crear datos antes de exponerla.
5. `escena_version` y `continuidad_foto` tienen 0 filas; la continuidad fotográfica se usa hoy sobre todo a través de las **versiones de galería**. Decidir si RF-18 se redefine así.
