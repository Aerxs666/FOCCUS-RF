# FOCCUS — Requisitos Funcionales e Historias de Usuario

## Nota de contexto

Este documento se reconstruyó a partir del código ya implementado, después de que el repositorio original donde se llevaba el registro de RF e HU quedó fuera del alcance del equipo (ver contexto: grupo original de 4 personas, dos se retiraron). No es una reconstrucción especulativa: cada historia de usuario está trazada contra un endpoint y/o pantalla real que existe y funciona en el proyecto.

---

## Requisitos Funcionales (RF)

| ID | Requisito |
|---|---|
| RF-01 | El sistema debe permitir el registro de una nueva empresa junto con su primer usuario, quien queda como Administrador |
| RF-02 | El sistema debe permitir iniciar sesión mediante correo y contraseña |
| RF-03 | El sistema debe verificar la identidad del usuario con un código de un solo uso enviado por correo (2FA) tras el login |
| RF-04 | El sistema debe permitir recuperar el acceso mediante un código de verificación enviado al correo |
| RF-05 | El sistema debe permitir a un Administrador invitar nuevos usuarios a un proyecto, asignándoles un rol |
| RF-06 | El sistema debe restringir la creación, edición y eliminación de datos a usuarios con rol de Administrador |
| RF-07 | El sistema debe permitir a un Administrador remover a un usuario de un proyecto sin eliminar su cuenta |
| RF-08 | El sistema debe permitir a cualquier usuario eliminar su propia cuenta |
| RF-09 | El sistema debe permitir el registro, consulta, edición y eliminación de clientes (empresas) |
| RF-10 | El sistema debe permitir el registro, consulta, edición y eliminación de proyectos, asociados a un cliente |
| RF-11 | El sistema debe permitir eliminar un proyecto junto con el contenido que dependa de él |
| RF-12 | El sistema debe permitir el registro, consulta, edición y eliminación de roles con su nivel jerárquico |
| RF-13 | El sistema debe permitir subir un guion en formato PDF y extraer su contenido para edición |
| RF-14 | El sistema debe generar una nueva versión del guion cada vez que su contenido se edite, conservando el historial completo |
| RF-15 | El sistema debe permitir agregar notas asociadas a una versión específica del guion |
| RF-16 | El sistema debe permitir eliminar un guion |
| RF-17 | El sistema debe permitir crear y gestionar escenas asociadas a un guion |
| RF-18 | El sistema debe permitir versionar la continuidad de una escena mediante fotografías de vestuario, objetos y espacios |
| RF-19 | El sistema debe permitir crear y gestionar un cronograma de rodaje por proyecto |
| RF-20 | El sistema debe permitir gestionar procesos/tareas dentro de un rodaje |
| RF-21 | El sistema debe exponer un formulario de contacto público, sin necesidad de autenticación |

---

## Historias de Usuario (HU)

Formato: *Como [rol], quiero [acción], para [beneficio]*.

### Autenticación y acceso

**HU-01** — Como visitante, quiero registrar mi empresa y mi cuenta en un solo formulario, para empezar a usar la plataforma como administrador de mi propio espacio de trabajo.
- RF relacionado: RF-01
- Evidencia: `POST /register`, pantalla `Login.jsx` (tab "Registrar")
- Estado: ✅ Hecho — probado en vivo durante el desarrollo

**HU-02** — Como usuario registrado, quiero iniciar sesión con mi correo y contraseña, para acceder a mis proyectos.
- RF relacionado: RF-02
- Evidencia: `POST /users/login`, pantalla `Login.jsx`
- Estado: ✅ Hecho

**HU-03** — Como usuario, quiero confirmar mi identidad con un código enviado a mi correo después de iniciar sesión, para que mi cuenta esté protegida aunque alguien más obtenga mi contraseña.
- RF relacionado: RF-03
- Evidencia: `POST /users/2fa/send`, `POST /users/2fa/verify`, pantalla `TwoFactor.jsx`
- Estado: ✅ Hecho — probado en vivo (incluye configuración real de envío por Gmail)

**HU-04** — Como usuario que olvidó su contraseña, quiero recuperarla con un código enviado a mi correo, para no perder el acceso a mi cuenta.
- RF relacionado: RF-04
- Evidencia: `POST /users/recover-password`, `POST /users/reset-password`, pantalla `ForgotPassword.jsx`
- Estado: ✅ Hecho — confirmado funcionando en el frontend

### Gestión de equipo y roles

**HU-05** — Como administrador, quiero invitar a un miembro de mi equipo por correo asignándole un rol específico, para que cada persona tenga solo el acceso que le corresponde.
- RF relacionado: RF-05
- Evidencia: `POST /users/invite`, pantalla `Roles.jsx`
- Estado: ✅ Hecho — probado en vivo, incluyendo el correo de invitación con credenciales temporales

**HU-06** — Como administrador, quiero que solo yo pueda crear, editar o borrar información crítica del proyecto, para evitar que un usuario normal modifique o dañe datos por error o a propósito.
- RF relacionado: RF-06
- Evidencia: dependencia `require_admin` en `app/utils/auth.py`, aplicada en todas las rutas de escritura de clientes, proyectos, roles, guion, escenas y rodaje
- Estado: ✅ Hecho

**HU-07** — Como administrador, quiero poder sacar a alguien de un proyecto sin borrar su cuenta de la plataforma, para poder reorganizar equipos sin perder el historial de esa persona en otros proyectos.
- RF relacionado: RF-07
- Evidencia: `DELETE /users/{id_user}/project/{id_project}`, botón en `Roles.jsx`
- Estado: ✅ Hecho — implementado y probado en esta misma conversación

**HU-08** — Como usuario, quiero poder eliminar mi propia cuenta cuando ya no quiera seguir usando la plataforma, para tener control sobre mis datos personales.
- RF relacionado: RF-08
- Evidencia: `DELETE /users/me/account`, botón "Eliminar mi cuenta" en `Profile.jsx`
- Estado: ✅ Hecho

### Clientes y proyectos

**HU-09** — Como administrador, quiero registrar y gestionar la información de las empresas cliente, para llevar el control de quién encarga cada producción.
- RF relacionado: RF-09
- Evidencia: `client_routes.py` (CRUD completo)
- Estado: ✅ Hecho — confirmado funcionando en el frontend

**HU-10** — Como administrador, quiero crear y editar proyectos asociados a un cliente, para organizar cada producción audiovisual por separado.
- RF relacionado: RF-10
- Evidencia: `project_routes.py`, pantallas `ProjectRegistration.jsx`, `ProjectSelection.jsx`
- Estado: ✅ Hecho

**HU-11** — Como administrador, quiero poder eliminar un proyecto completo cuando ya no esté vigente, para mantener organizado el panel de proyectos activos.
- RF relacionado: RF-11
- Evidencia: `DELETE /projects/{id}`, botón "Eliminar proyecto" en el menú de `ProjectDashboard.jsx`
- Estado: ✅ Hecho — implementado en esta misma conversación

**HU-12** — Como administrador, quiero definir los roles disponibles y su jerarquía, para adaptar la estructura de permisos a cómo funciona realmente mi equipo.
- RF relacionado: RF-12
- Evidencia: `role_routes.py` (CRUD completo)
- Estado: ✅ Hecho — confirmado funcionando en el frontend

### Guion

**HU-13** — Como administrador, quiero subir el guion de mi producción en PDF, para tener un punto de partida único y oficial del documento.
- RF relacionado: RF-13
- Evidencia: `POST /guiones`, pantalla `Guion.jsx`
- Estado: ✅ Hecho

**HU-14** — Como administrador, quiero editar el contenido del guion directamente en la plataforma y que cada cambio quede guardado como una versión nueva, para poder comparar cómo evolucionó el guion sin perder ninguna versión anterior.
- RF relacionado: RF-14
- Evidencia: `POST /guiones/{id_guion}/versiones`, tabla `guion_version`
- Estado: ✅ Hecho

**HU-15** — Como miembro del equipo, quiero dejar notas sobre una versión específica del guion, para comunicar observaciones sin necesidad de editar el documento.
- RF relacionado: RF-15
- Evidencia: `POST /guiones/versiones/{id}/notas`
- Estado: ✅ Hecho — confirmado funcionando en el frontend

**HU-16** — Como administrador, quiero poder eliminar un guion que ya no sea necesario, para mantener ordenada la sección.
- RF relacionado: RF-16
- Evidencia: `DELETE /guiones/{id_guion}`, botón de eliminar en `Guion.jsx`
- Estado: ✅ Hecho — implementado en esta misma conversación

### Escenas y continuidad

**HU-17** — Como administrador, quiero dividir el guion en escenas individuales, para organizar el trabajo de continuidad escena por escena.
- RF relacionado: RF-17
- Evidencia: `POST /escenas`, pantalla `Escena.jsx`
- Estado: ✅ Hecho — confirmado funcionando en el frontend

**HU-18** — Como responsable de continuidad, quiero subir fotos de vestuario, objetos y espacios por cada actualización de una escena, para poder comparar visualmente la continuidad entre tomas grabadas en fechas distintas.
- RF relacionado: RF-18
- Evidencia: `POST /escenas/{id}/versiones`, `POST /escenas/versiones/{id}/fotos`
- Estado: ✅ Hecho — confirmado funcionando en el frontend

### Rodaje

**HU-19** — Como administrador, quiero crear un cronograma de rodaje para mi proyecto, para organizar fechas y locaciones de grabación.
- RF relacionado: RF-19
- Evidencia: `rodaje_routes.py`, pantalla `Rodaje.jsx`
- Estado: ✅ Hecho — confirmado funcionando en el frontend

**HU-20** — Como administrador, quiero registrar procesos o tareas dentro de un rodaje, para hacer seguimiento del avance de cada jornada.
- RF relacionado: RF-20
- Evidencia: `proceso_rodaje_model.py`, endpoints `/rodajes/{id}/procesos`
- Estado: ✅ Hecho — confirmado funcionando en el frontend

### Otros

**HU-21** — Como visitante interesado, quiero poder escribir un mensaje de contacto sin necesidad de crear una cuenta, para consultar antes de registrarme.
- RF relacionado: RF-21
- Evidencia: `POST /contact`
- Estado: ✅ Hecho

---

## Tablero (formato Kanban)


### ✅ Hecho
- HU-01 · Registro de empresa y cuenta admin
- HU-02 · Login con correo y contraseña
- HU-03 · Verificación en dos pasos por correo
- HU-04 · Recuperar contraseña
- HU-05 · Invitar usuarios con rol asignado
- HU-06 · Restricción de acciones por rol (Admin vs Usuario)
- HU-07 · Remover usuario de un proyecto
- HU-08 · Eliminar cuenta propia
- HU-09 · Gestión de clientes
- HU-10 · Crear y editar proyectos
- HU-11 · Eliminar proyecto
- HU-12 · Gestión de roles
- HU-13 · Subir guion en PDF
- HU-14 · Versionamiento de guion al editar
- HU-15 · Notas sobre versiones de guion
- HU-16 · Eliminar guion
- HU-17 · Crear escenas
- HU-18 · Continuidad fotográfica de escenas
- HU-19 · Cronograma de rodaje
- HU-20 · Procesos de rodaje
- HU-21 · Formulario de contacto público

### 📋 Backlog / mejoras identificadas (no bloquean la entrega)
- Migrar almacenamiento de archivos de disco local a almacenamiento en la nube
- Hacer que el token de login no sea válido hasta completar el 2FA (hoy es más una pantalla de flujo que un bloqueo real de API)
- Unificar el uso de `apiFetch` en todas las pantallas (algunas usan `fetch` directo)
- Adoptar una sola librería de estilos (hoy conviven Tailwind y Bootstrap)

---
