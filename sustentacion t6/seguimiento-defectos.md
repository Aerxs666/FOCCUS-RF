# Seguimiento de defectos T6

Registro persistente de los defectos reproducibles documentados en los ciclos T6. Las correcciones están en ramas separadas y **pendientes de integración**; no se afirma que estén en `main` ni verificadas en producción.

## T6-D02 — Encabezado mixto I/E

- **Severidad:** Media, valoración técnica: el formulario podía reconstruir el encabezado con una ubicación incorrecta y alterar el texto al aplicarlo.
- **Estado:** Corregido en rama; integración pendiente.
- **Versión y fecha:** Base `9126d8f0ab691ee7b6fd5c33c76e725ae3d8e85a`; ciclo ejecutado el 2026-11-21.
- **Pasos reproducibles:** En un worktree limpio de la base, ejecutar desde la raíz:

  ```text
  git restore --source fix/t6-ciclo-a -- frontend/src/utils/guionPrefijoMixto.test.js
  node --test frontend/src/utils/guionPrefijoMixto.test.js
  git restore --source fix/t6-ciclo-a -- frontend/src/utils/guionEscenas.js
  node --test frontend/src/utils/guionPrefijoMixto.test.js
  ```
- **Esperado:** `I/E. CASA` se interpreta como vista `Int/Ext` y ubicación `CASA`.
- **Obtenido antes:** Vista vacía y ubicación `I/E. CASA`; prueba fallida (1 fallo).
- **Prueba antes/después:** Antes, el comando indicado falló. Después de aplicar la corrección de la rama, pasó (1/1). En esa rama también se registraron `npm test` (17/17), `npm run build` y ESLint de los archivos indicados, todos con código 0.
- **Rama y commit:** [`fix/t6-ciclo-a`](https://github.com/Cr4ckJu4nF3/FOCCUS/tree/fix/t6-ciclo-a), `fef8a86010d09ea00c4dd0eb82b4c1b6ddd19ac0`.
- **Evidencia:** [ciclo I/E](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/fix/t6-ciclo-a/docs/agentes/T6_CICLO_IE.md).

## T6-D03 — Lugares que empiezan por INT o EXT

- **Severidad:** Media, valoración técnica: el formulario podía confundir el comienzo del nombre de un lugar con un modo interior/exterior y modificar el texto al aplicarlo.
- **Estado:** Corregido en rama; integración pendiente.
- **Versión y fecha:** Base `9126d8f0ab691ee7b6fd5c33c76e725ae3d8e85a`; ciclo ejecutado el 2026-11-21.
- **Pasos reproducibles:** En un worktree limpio de la base, ejecutar desde la raíz:

  ```text
  git restore --source fix/t6-ciclo-b -- frontend/src/utils/guionPrefijoPalabra.test.js
  node --test frontend/src/utils/guionPrefijoPalabra.test.js
  git restore --source fix/t6-ciclo-b -- frontend/src/utils/guionEscenas.js
  node --test frontend/src/utils/guionPrefijoPalabra.test.js
  ```
- **Esperado:** `INTERNADO - DÍA` y `EXTERIOR DEL TEATRO` se conservan como nombres de ubicación, no como prefijos `INT` o `EXT`.
- **Obtenido antes:** `INTERNADO - DÍA` se interpretaba como modo `Int` y ubicación `ERNADO`; prueba fallida (1 fallo).
- **Prueba antes/después:** Antes, el comando indicado falló. Después de aplicar la corrección de la rama, pasó (2/2, incluida una prueba de compatibilidad). En esa rama también se registraron `npm test` (18/18), `npm run build` y ESLint de los archivos indicados, todos con código 0.
- **Rama y commit:** [`fix/t6-ciclo-b`](https://github.com/Cr4ckJu4nF3/FOCCUS/tree/fix/t6-ciclo-b), `3a73e33c77b05cb37973e89d4ae27530d0c222e6`.
- **Evidencia:** [ciclo de encabezados INTERNADO/EXTERIOR](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/fix/t6-ciclo-b/docs/agentes/T6_CICLO_LUGARES.md).

## Mantenimiento del registro

1. Al reportar un defecto, agrega un ID único y anota solo pasos y resultados comprobados, además de severidad y su justificación técnica.
2. Usa `Abierto`, `En corrección` o `Corregido en rama; integración pendiente`, según corresponda. No marques integrado hasta comprobar la rama de destino; no afirmes pruebas de producción sin evidencia.
3. Al corregir, registra la rama y el commit, repite la misma prueba y anota el resultado antes/después y la fecha.
4. Conserva los enlaces a la evidencia publicada y actualiza la fila del punto 10 en el README de sustentación. Confirma con el instructor si acepta el seguimiento en archivo; el registro no implica su aprobación.

## Referencias T6

- [Reporte de ejecución y evidencia](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/docs/agentes/T6_EVIDENCIA.md).
- [Matriz de estado de la sustentación](README.md), punto 10.
