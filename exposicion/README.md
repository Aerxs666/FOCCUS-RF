# Guía de exposición

Esquema base de 10 a 15 minutos. Los datos de acceso están en `privado/` (no se sube a git).

## Estructura

1. **Problema** (1 min): la continuidad en un rodaje.
2. **Solución** (1 min): qué es FOCCUS y quiénes lo usan.
3. **Demo web** (6 min), con el proyecto "estrella" (ver `privado/`):
   - Login y 2FA
   - Guion con bloques y PDF
   - Escenas, galería y desglose
   - Rodaje
   - Códigos y búsqueda (con el usuario admin)
4. **Demo móvil** (3 min): lo mismo desde el celular.
5. **Arquitectura y datos** (2 min): diagramas de `diagramas/README.md`.
6. **Pendientes y cierre** (1 min).

## Lista de comprobación antes de exponer

- [ ] Aiven encendido (si no, el backend no arranca).
- [ ] Backend en marcha: `uvicorn app.main:app --host 0.0.0.0 --port 8000`.
- [ ] Celular: cable, depuración USB y `adb reverse tcp:8000 tcp:8000`.
- [ ] Probar login y 2FA (el correo debe poder enviarse).
- [ ] Revisar `requisitos/informe-revision.md`, sección "Riesgos".
- [ ] Tener a mano `privado/accesos_exposicion.md`.

## Preguntas probables

- **¿Cómo se protege la información?** JWT, contraseñas con bcrypt, controles por rol y secretos fuera de git. La suite web incluye pruebas aisladas de pertenencia de recursos al proyecto; no equivale a una validación con BD real.
- **¿Por qué códigos?** En audiovisual todo se identifica con un código para hallarlo rápido; solo el admin los ve.
- **¿Qué falta?** Guardar archivos en la nube. La prueba HTTP aislada de RF-10 verifica que el administrador edita y persiste su propio proyecto, obtiene 403 al editar otro y que el proyecto ajeno permanece igual. El lint focalizado de los archivos JS modificados, incluido `Login`, pasó. El lint global conserva 14 errores preexistentes en `Escena.jsx`, `Landing.jsx`, `Profile.jsx`, `ProjectRegistration.jsx` y `ProjectSelection.jsx`, archivos no modificados en esta pasada. Móvil no se revisó, incluido el impacto del nuevo contrato 2FA.
- **¿Cómo se respalda la BD?** Script de backup con fecha antes de cada cambio estructural.
