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

- **¿Cómo se protege la información?** JWT, contraseñas con bcrypt, permisos por rol en cada proyecto, secretos fuera de git.
- **¿Por qué códigos?** En audiovisual todo se identifica con un código para hallarlo rápido; solo el admin los ve.
- **¿Qué falta?** 2FA que bloquee el token, archivos en la nube, PDF y bloques en móvil.
- **¿Cómo se respalda la BD?** Script de backup con fecha antes de cada cambio estructural.
