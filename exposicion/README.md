# Guía de exposición

Para T6 consulta el [cierre](cierre-t6.md), la [demo propuesta](demo-t6.md), la [API y los commits](api-y-commits-t6.md) y la [deuda priorizada](deuda-tecnica-t6.md). La demo integral y la integración móvil siguen sin verificarse.

Esquema base de 10 a 15 minutos. Los datos de acceso están en `privado/` (no se sube a git).

[Consultas SQL por RF](consultas-rf.md)

## Estructura

1. **Problema** (1 min): la continuidad en un rodaje.
2. **Solución** (1 min): qué es FOCCUS y quiénes lo usan.
3. **Demo web** (6 min), con el proyecto "estrella" (ver `privado/`):
   - Login y 2FA
   - Guion con bloques y PDF
   - Escenas, galería y desglose
   - Rodaje
   - Códigos y búsqueda (con el usuario admin)
4. **Demo móvil** (3 min): consultar el mismo proyecto solo si se verificó la app instalada y su conexión; de lo contrario, explicar que está pendiente.
5. **Arquitectura y datos** (2 min): diagramas de `diagramas/README.md`.
6. **Pendientes y cierre** (1 min).

## Lista de comprobación antes de exponer

- [ ] Base de datos configurada y disponible; si se usa Aiven, comprobar que esté encendido.
- [ ] Backend en marcha: `uvicorn app.main:app --host 0.0.0.0 --port 8000`.
- [ ] Si se mostrará móvil: comprobar la app y su conexión; usar cable, depuración USB y `adb reverse tcp:8000 tcp:8000` si el entorno lo necesita.
- [ ] Probar login y 2FA (el correo debe poder enviarse).
- [ ] Revisar [pendientes y precauciones](../requisitos/informe-revision.md#pendientes-y-precauciones).
- [ ] Tener a mano `privado/accesos_exposicion.md`.

## Preguntas probables

- **¿Cómo se protege la información?** JWT, contraseñas con bcrypt, controles por rol y secretos fuera de git. La suite web incluye pruebas aisladas de pertenencia de recursos al proyecto; no equivale a una validación con BD real.
- **¿Por qué códigos?** En audiovisual todo se identifica con un código para hallarlo rápido; solo el admin los ve.
- **¿Qué falta?** Validar móvil y la demo integral, además de definir una estrategia para los archivos. Una ejecución anterior registró 14 errores de lint global; no se ha confirmado la cifra actual. Ver [deuda técnica](deuda-tecnica-t6.md) y [evidencia T6](../sustentacion%20t6/README.md).
- **¿Cómo se respalda la BD?** Antes de cambios estructurales se debe crear un respaldo y verificar su restauración. Consulta el registro de BD para cada caso; no asumas que todos los respaldos están verificados.
