# FOCCUS — Historias de Usuario (HU)

Formato: *Como [rol], quiero [acción], para [beneficio]*. Cada HU indica RF, evidencia (endpoint o pantalla) y estado. Última revisión: 2026-11-01.

## Autenticación y acceso

- **HU-01** — Como visitante, quiero registrar mi empresa y mi cuenta en un solo formulario, para empezar como administrador de mi espacio de trabajo. · RF-01 · `POST /register`, `Login.jsx` (pestaña Registrar) · ✅
- **HU-02** — Como usuario registrado, quiero iniciar sesión con correo y contraseña, para acceder a mis proyectos. · RF-02 · `POST /users/login`, `Login.jsx` · ✅
- **HU-03** — Como usuario, quiero confirmar mi identidad con un código enviado a mi correo, para proteger mi cuenta aunque alguien conozca mi contraseña. · RF-03 · `POST /users/2fa/send`, `/verify`, `/check`, `TwoFactor.jsx` · ✅
- **HU-04** — Como usuario que olvidó su contraseña, quiero recuperarla con un código por correo, para no perder el acceso. · RF-04 · `POST /users/recover-password`, `/verify-recovery-code`, `/reset-password`, `ForgotPassword.jsx` · ✅

## Equipo y roles

- **HU-05** — Como administrador, quiero invitar a un miembro por correo con un rol, para que cada persona tenga el acceso que le corresponde. · RF-05 · `POST /users/invite`, `/users/complete-invitation`, `Roles.jsx`, `CompleteInvitation.jsx` · ✅
- **HU-06** — Como administrador, quiero que solo los administradores del proyecto puedan crear, editar o borrar información crítica, para evitar cambios por error. · RF-06 · `require_project_admin` / `require_project_member` en `app/utils/auth.py` · ✅
- **HU-07** — Como administrador, quiero sacar a alguien de un proyecto sin borrar su cuenta, para reorganizar equipos. · RF-07 · `DELETE /users/{id_user}/project/{id_project}`, `Roles.jsx` · ✅
- **HU-08** — Como usuario, quiero eliminar mi propia cuenta, para controlar mis datos. · RF-08 · `DELETE /users/me/account`, `Profile.jsx` · ✅
- **HU-12** — Como administrador, quiero definir roles y su jerarquía, para adaptar los permisos a mi equipo. · RF-12 · `/roles` (CRUD) · 🟡 (la tabla `roles` está vacía; se usa el `id_rol` 1001)

## Clientes y proyectos

- **HU-09** — Como administrador, quiero gestionar las empresas cliente, para saber quién encarga cada producción. · RF-09 · `/clients` (CRUD) · ✅
- **HU-10** — Como administrador, quiero crear y editar proyectos asociados a un cliente, para separar cada producción. · RF-10 · `/projects`, `ProjectRegistration.jsx`, `ProjectSelection.jsx` · ✅
- **HU-11** — Como administrador, quiero eliminar un proyecto completo, para mantener ordenado el panel. · RF-11 · `POST /projects/{id}/delete`, `ProjectDashboard.jsx` · ✅

## Guion

- **HU-13** — Como administrador, quiero crear el guion subiendo un archivo o escribiéndolo, para tener un punto de partida oficial. · RF-13 · `POST /guiones`, `/guiones/archivo`, `/guiones/texto`, `Guion.jsx` · ✅
- **HU-14** — Como administrador, quiero que cada edición del guion quede como versión nueva, para comparar su evolución. · RF-14 · `POST /guiones/{id}/versiones`, `/versiones/texto`, tabla `guion_version` · ✅
- **HU-15** — Como miembro, quiero dejar notas en una versión del guion, para comunicar observaciones sin editarlo. · RF-15 · `POST /guiones/versiones/{id}/notas` · 🟡 (sin datos de ejemplo)
- **HU-16** — Como administrador, quiero eliminar un guion, para mantener ordenada la sección. · RF-16 · `DELETE /guiones/{id}` · ✅
- **HU-26** — Como guionista, quiero escribir con bloques (escena, acción, personaje, diálogo…) y exportar a PDF con el formato de la industria, para entregar un guion profesional. · RF-26, RF-27 · `Guion.jsx`, PDF en el frontend · ✅ (web)

## Escenas, galería y desglose

- **HU-17** — Como administrador, quiero dividir el guion en escenas, para trabajar la continuidad escena por escena. · RF-17 · `POST /escenas`, `Escena.jsx` · ✅
- **HU-18** — Como responsable de continuidad, quiero subir fotos por cada actualización de una escena, para comparar la continuidad entre tomas. · RF-18 · `/escenas/{id}/versiones`, `/fotos` · 🟡 (ver nota 5 de RF)
- **HU-22** — Como responsable de continuidad, quiero una galería de personajes, lugares, objetos y vestuario con versiones y fotos, para consultar cómo debe verse cada cosa. · RF-22 · `/projects/{id}/galeria`, `Galeria.jsx` · ✅
- **HU-23** — Como equipo de producción, quiero vincular elementos de la galería a una escena, para saber qué necesita cada escena. · RF-23 · `/escenas/{id}/desglose/galeria` · ✅
- **HU-24** — Como productor, quiero un desglose por escena con sus requerimientos, para planear el rodaje. · RF-24 · `/guiones/{id}/desglose`, `Desglose.jsx` · ✅

## Rodaje

- **HU-19** — Como administrador, quiero un cronograma de rodaje, para organizar fechas y locaciones. · RF-19 · `/rodajes`, `Rodaje.jsx` · ✅
- **HU-20** — Como administrador, quiero registrar procesos dentro de un rodaje, para seguir el avance de cada jornada. · RF-20 · `/rodajes/{id}/procesos` · 🟡 (sin datos de ejemplo)
- **HU-25** — Como productor, quiero importar las escenas del guion a las jornadas, para no cargarlas una por una. · RF-25 · `POST /projects/{id}/rodajes/importar` · ✅

## Códigos y búsqueda (solo administrador)

- **HU-27** — Como administrador, quiero ver un código único (ej. `ESC-003`) en cada elemento, para nombrarlo y hallarlo rápido como en la industria audiovisual. · RF-28, RF-29 · etiqueta `CodigoChip`, tablas `codigos_entidad` y `codigos_contador` · ✅
- **HU-28** — Como administrador, quiero buscar por código y abrir la ficha, para llegar a cualquier elemento sin navegar. · RF-30 · `GET /projects/{id}/buscar-codigo`, `/buscar-codigo` (`BuscarCodigo.jsx`) · ✅

## Móvil

- **HU-29** — Como miembro del equipo, quiero consultar y editar el proyecto desde el celular, para trabajar en el set. · RF-02, 10, 14, 17, 19, 22, 24, 28–30 · app Flutter (rama `mobile`) · 🟡 (falta PDF, bloques `gb-*`)

## Otros

- **HU-21** — Como visitante, quiero escribir un mensaje de contacto sin cuenta, para consultar antes de registrarme. · RF-21 · `POST /contact` · ✅

## Tablero

| ✅ Hecho | 🟡 Parcial | 🔲 Backlog |
|---|---|---|
| HU-01 a 11, 13, 14, 16, 17, 19, 21 a 28 | HU-12, 15, 18, 20, 29 | Token sin validez hasta el 2FA; archivos a la nube; unificar `apiFetch`; una sola librería de estilos; PDF y bloques `gb-*` en móvil |
