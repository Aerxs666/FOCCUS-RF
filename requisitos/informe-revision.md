# Informe de revisión de RF y HU

Fecha: 2026-11-01. Revisado: el `README.md` original del repo (RF-01 a RF-21, HU-01 a HU-21) contra el código actual (rutas de `/openapi.json`, pantallas del frontend, tablas de la BD y app Flutter). Este informe se actualiza cada vez que cambia el producto.

## Resumen

El documento original es **sólido para lo que cubre**: cada HU tiene RF, evidencia y estado, y el backlog es honesto. Pero quedó **desactualizado**: describe 21 HU y hoy el producto tiene al menos 29 funcionalidades. Faltan galería, desglose, códigos, buscador, guion por bloques/PDF y la app móvil.

## Lo que está bien

- Formato correcto de HU ("Como… quiero… para…") con RF relacionado.
- **Trazabilidad con evidencia** (endpoint o pantalla) en cada historia.
- Tablero Kanban y backlog con deuda técnica real (2FA, nube, estilos).
- Los RF cubren el núcleo: autenticación, equipo, clientes, proyectos, guion, escenas y rodaje.

## Lo que se corrigió o hay que corregir

| # | Hallazgo | Acción |
|---|---|---|
| 1 | La nota de contexto y estados como "implementado en esta misma conversación" no sirven en un documento formal | Eliminadas; el estado ahora es ✅/🟡/🔲 |
| 2 | RF-06/HU-06 dicen que solo "Administrador" escribe, citando `require_admin`; hoy los permisos son por proyecto (`require_project_admin` / `require_project_member`) | Reescrito en RF/HU |
| 3 | RF-13/HU-13 dicen "subir un PDF"; hoy hay archivo, texto y editor con bloques | Reescrito |
| 4 | Faltaban RF/HU de galería, desglose, importar rodaje, formato de guion y PDF, códigos, buscador y móvil | Agregados RF-22 a RF-30 y HU-22 a HU-29 |
| 5 | No existían requisitos no funcionales | Creado `RNF.md` (13 RNF) |
| 6 | No había actores definidos ni criterios de aceptación | Actores añadidos en `RF.md`. **Falta** escribir criterios de aceptación por HU |
| 7 | No había prioridad (MoSCoW) ni estimación | **Falta**: asignar prioridad a cada RF |
| 8 | No había matriz de trazabilidad | Creada `matriz-trazabilidad.md` |
| 9 | Funciones marcadas "confirmado funcionando" sin datos en la BD: `guion_nota`, `proceso_rodaje`, `escena_version`, `continuidad_foto` tienen 0 filas | Marcadas 🟡; crear datos de ejemplo o probarlas antes de exponer |
| 10 | La tabla `roles` está vacía; el admin es `id_rol` 1001 fijo | Aclarar en la exposición cómo se manejan los roles (HU-12 🟡) |
| 11 | HU-18 (continuidad por versiones de escena) casi no se usa; la continuidad real está en versiones de galería | Decidir con el equipo si RF-18 se redefine |
| 12 | Sin RF para 2FA/recuperación/invitación en móvil | Marcado "por verificar" |

## Lo que falta (propuesto)

1. **Criterios de aceptación** (Dado/Cuando/Entonces) para las HU principales.
2. **Prioridad** de cada RF (alta/media/baja).
3. **Casos de prueba** ligados a cada RF (hoy solo hay pruebas en móvil).
4. Documento de **casos de uso** más allá del diagrama base (`diagramas/casos-de-uso.md`).
5. Aclarar el alcance de **exportación** (PDF hoy; ¿Final Draft `.fdx`?).
6. Registro de **cambios de requisitos** (versionado del propio documento).

## Riesgos para la exposición

- Si el backend no arranca, revisar que Aiven esté encendido.
- Probar antes los módulos 🟡 (notas de guion, procesos de rodaje, continuidad por escena) y tener datos listos.
- El módulo de códigos solo se ve con el usuario administrador del proyecto.

## Pendientes de otros agentes

- **foccus-web:** 2FA no bloquea el token; estados con acción solo en la lista de guiones; texto menor a 12 px en algunas pantallas.
- **foccus-mobile:** leer bloques `gb-*`; PDF.
- **foccus-bd:** ninguno nuevo.
