# Sustentación T6 — FOCCUS

Guía de preparación, no calificación. Los estados son una valoración documental del equipo: **la aprobación de la lista corresponde al jurado**. El usuario aprobó el plan de pruebas, no sustituyó esa decisión.

## Resultados principales

- **Cierre:** el equipo considera terminado el producto web para T6, incluyendo cambios en creación de escenas desde guion, galería y dashboard. Es una valoración del equipo, no una certificación de ausencia de defectos ni de integración completa. T7 se orienta al producto final, terminar móvil e implementar los requisitos adicionales que indiquen.
- **Ejecución registrada el 21-11-2026:** 36 pruebas backend (27 de seguridad y 9 de API), 108/116 sentencias de `auth.py` (93 %) y Newman 7/7 aserciones. Son resultados parciales en pruebas aisladas, no contra MySQL real.
- **Navegador:** 2 recorridos estáticos sin login ni persistencia. **Frontend:** 37 pruebas y build aprobados sobre un árbol con cambios no publicados; lint global falló con 14 errores. No se repitieron estas ejecuciones para esta guía.
- **Dos ciclos** de defecto, corrección y reejecución están publicados en ramas independientes. No están integrados ni demuestran corrección en producción.
- [Plan de pruebas aprobado por el usuario](plan-pruebas.md) · [Matriz de 27 casos](#t6-08--matriz-de-27-casos) · [Evidencia independiente](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/docs/agentes/T6_EVIDENCIA.md).

## Matriz de los 15 puntos

✅ evidencia de todos los componentes del criterio; 🟡 parcial; 🔴 no aprobado por falta de evidencia o por resultado desfavorable; ⏸ en proceso o pausado; ➖ no aplica por decisión del equipo. No son decisiones del jurado.

| ID | Criterio resumido | Estado | Resultado o pendiente |
|---|---|---|---|
| [01](#t6-01--cierre) | Visión de cierre T6 y T7 | ✅ | Decisión documentada, con límites. |
| [02](#t6-02--retrospectivas) | Dos retrospectivas de pruebas | ⏸ En proceso | Faltan dos retrospectivas reales. |
| [03](#t6-03--cuarto-backend) | Cuarto backend funcional y diferenciado | 🟡 | Un FastAPI con routers; interpretación del criterio pendiente de validación del instructor. |
| [04](#t6-04--validación-jwt-e-instalación) | Validación, JWT e instalación limpia | 🟡 | Pruebas aisladas y arranque simulado; faltan instalación limpia y login completo. |
| [05](#t6-05--arquitectura-y-demo) | Arquitectura y demo integral | 🟡 | Arquitectura contrastada con código; demo completa no demostrada. |
| [06](#t6-06--bonificación-iot) | Bonificación IoT | ➖ No aplica | Equipo decidió no realizarla. |
| [07](#t6-07--plan-de-pruebas) | Plan con alcance, niveles y ambiente | ✅ | [Plan aprobado por usuario](plan-pruebas.md); no implica ejecución completa. |
| [08](#t6-08--matriz-de-27-casos) | ≥20 casos con datos, pasos y resultados | ✅ | 27 casos registrados, más 9 integrados; alcance parcial del producto. |
| [09](#t6-09--automatización-y-postman) | Cobertura ≥50 % de módulo crítico y colección con tests | ✅ | 93 % de sentencias de `auth.py`; 7/7 aserciones de API parcial. |
| [10](#t6-10--reporte-y-defectos) | Reporte y defectos en sistema de seguimiento | 🟡 | Reporte y defecto con severidad/estado en archivo; no hay issue creado ni sistema demostrado. |
| [11](#t6-11--ciclos-de-corrección) | Dos ciclos con caso, commit y reejecución | ✅ | Dos ciclos reales en ramas independientes, sin integración publicada. |
| [12](#t6-12--readme-y-api) | README de pruebas y API del cuarto backend | 🟡 | README y OpenAPI en arranque simulado; interpretación del cuarto backend pendiente. |
| [13](#t6-13--historial-de-commits) | Commits de construcción y corrección | ✅ | Ejemplos `feat` y `fix`; asociación a incidencias no demostrada. |
| [14](#t6-14--lint-y-regresiones) | Linter sin errores críticos y sin regresiones T5 | 🔴 No aprobado | 14 errores; criticidad funcional desconocida y sin línea base T5. |
| [15](#t6-15--comparación-y-deuda) | Comparación de cuatro backends y deuda priorizada | ⏸ Pausado | Deuda documentada; faltan antecedentes y comparación. |

## Evidencia por requisito

### T6-01 — Cierre

Para el equipo, T6 cierra la construcción web, con cambios de guion/creación de escena, galería y dashboard. Las pantallas públicas de [guion](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/9126d8f/frontend/src/screen/Guion.jsx), [galería](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/9126d8f/frontend/src/screen/Galeria.jsx) y [dashboard de proyecto](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/9126d8f/frontend/src/screen/ProjectDashboard.jsx) muestran esas áreas, no prueban cada flujo completo. Las brechas verificadas siguen abiertas. En T7 se terminará móvil y se incorporarán los requisitos adicionales que indiquen para el producto final.

### T6-02 — Retrospectivas

En proceso. Faltan dos retrospectivas de sprints reales con reflexión explícita sobre pruebas; no se han inventado.

### T6-03 — Cuarto backend

[La aplicación FastAPI](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/9126d8f/backend/api_usuarios/app/main.py) incluye routers para usuarios, proyectos, guiones, escenas, galería y rodaje: **un backend**, con responsabilidades por router, no cuatro servicios independientes. El equipo interpreta así el criterio «4.º backend»; **no existe aquí evidencia de una exención aprobada por el instructor**. Falta validar la interpretación y justificar la responsabilidad frente a los backends anteriores. El arranque comprobado fue simulado, no con infraestructura real.

### T6-04 — Validación, JWT e instalación

La [evidencia publicada](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/docs/agentes/T6_EVIDENCIA.md#ejecución-y-límites) registra validaciones, JWT firmado y validado con clave ficticia, y arranque de `app.main` completo con motor simulado, creación de tablas desactivada y BD deshabilitada. `/`, `/docs` y `/openapi.json` respondieron 200; el esquema de la base describió 69 rutas. Existe `.env.example`. **No se probó instalación limpia ni login exitoso completo**, ni la infraestructura real.

### T6-05 — Arquitectura y demo

El diagrama de abajo refleja la estructura de `main.py` y el [README público de la rama de evidencia](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/README.md#estructura-del-proyecto); es una vista simplificada, no una prueba de integración. Solo hay dos comprobaciones de navegador con servidor estático: inicio → login y `/guion` sin sesión → inicio. No incluyen autenticación, API ni persistencia y usaron el `dist` de un árbol con cambios sin publicar. **La demo end-to-end completa no está demostrada**; no se presenta la lista como aprobada.

### T6-06 — Bonificación IoT

El equipo decidió no realizar el componente IoT. La bonificación opcional no aplica; no se afirma que exista un prototipo.

### T6-07 — Plan de pruebas

El [plan de pruebas](plan-pruebas.md) fue aprobado expresamente por el usuario: define alcance, niveles, ambiente aislado, datos ficticios, criterio por caso y reporte. La aprobación es del **plan**, no de las pruebas aún pendientes ni del jurado.

### T6-08 — Matriz de 27 casos

La [matriz original publicada](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/README.md#matriz-de-casos-ejecutados) registra 27 casos ejecutados con datos ficticios. Paso para cada fila: ejecutar el método `test_NN` correspondiente en [`test_t6_seguridad_aislada.py`](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/backend/api_usuarios/tests/test_t6_seguridad_aislada.py), que contiene preparación, datos y aserciones; el [comando reproducible](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/README.md#backend-seguridad-y-cobertura) ejecuta la suite junto con las pruebas integradas. «Coincide» significa que las aserciones pasaron en la ejecución registrada, no que se haya probado producción.

| ID | Datos y acción | Esperado | Obtenido |
|---|---|---|---|
| 01 | JWT firmado, usuario ficticio y 2FA verificado | Devuelve usuario | Coincide |
| 02 | Sin cabecera | 401 | Coincide |
| 03 | Esquema Basic | 401 | Coincide |
| 04 | Bearer malformado | 401 | Coincide |
| 05 | JWT expirado | 401 | Coincide |
| 06 | JWT sin usuario | 401 | Coincide |
| 07 | JWT sin 2FA | 401 | Coincide |
| 08 | JWT con 2FA falso | 401 | Coincide |
| 09 | Rol vigente de administrador, claim obsoleto no administrador | Autoriza rol vigente | Coincide |
| 10 | Rol vigente no administrador, claim obsoleto administrador | 403 | Coincide |
| 11 | Administrador con cuenta inexistente | 401 | Coincide |
| 12 | Esquema de login con dispositivo válido | Acepta | Coincide |
| 13 | Login sin dispositivo | Error de validación | Coincide |
| 14 | Login con dispositivo vacío | Error de validación | Coincide |
| 15 | Login con dispositivo de 256 caracteres | Error de validación | Coincide |
| 16 | Recuperación: contraseña de 72 bytes | Acepta | Coincide |
| 17 | Recuperación: contraseña de 73 bytes | Error de validación | Coincide |
| 18 | Recuperación: 37 caracteres ñ, 74 bytes | Error de validación | Coincide |
| 19 | Invitación ficticia con espacios alrededor del nombre | Acepta y normaliza | Coincide |
| 20 | Invitación con nombre solo espacios | Error de validación | Coincide |
| 21 | Invitación con nacimiento hoy | Error de validación | Coincide |
| 22 | Invitación con nacimiento futuro | Error de validación | Coincide |
| 23 | Contraseña de invitación corta | Error de validación | Coincide |
| 24 | Contraseña sin mayúscula | Error de validación | Coincide |
| 25 | Contraseña sin minúscula | Error de validación | Coincide |
| 26 | Contraseña sin número | Error de validación | Coincide |
| 27 | Contraseña sin carácter especial | Error de validación | Coincide |

Además, la [matriz de 9 casos de API integrada](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/docs/agentes/T6_EVIDENCIA.md#matriz-complementaria-de-api-integrada) cubre, con SQLite temporal, acceso por proyecto, lecturas y mutaciones entre proyectos, recursos vinculados, continuidad, rodaje, personajes y escenarios, foto simulada y edición de proyecto. Todos pasaron en la ejecución registrada. Galería no se probó como flujo propio y falta navegador con persistencia.

### T6-09 — Automatización y Postman

Se registran **36/36 pruebas backend**, 27 unitarias de seguridad y 9 integradas, y **108/116 sentencias (93 %) de `auth.py`**, módulo elegido por JWT, 2FA, roles y separación por proyecto. No se midió cobertura de ramas ni del backend completo. La [colección Postman publicada](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/backend/api_usuarios/tests/FOCCUS_T6.postman_collection.json) registró **7 solicitudes y 7 aserciones aprobadas** con Newman sobre una API parcial de cuatro rutas, BD simulada y datos ficticios: login inexistente y dispositivo inválido, usuarios sin JWT o con JWT inválido, límite de contraseña y 2FA sin intento. No prueba login exitoso, MySQL ni correo reales. Véanse [comandos y límites](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/README.md#pruebas-y-evidencia-t6).

### T6-10 — Reporte y defectos

El [reporte de ejecución y registro T6-D01](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/docs/agentes/T6_EVIDENCIA.md#registro-local-de-defectos-y-seguimiento) documenta lint con 14 errores, severidad **media** por bloqueo del control estático, impacto funcional no establecido y estado **abierto**. Se intentó crear GitHub Issues, pero GitKraken solicitó iniciar sesión; **no se crearon issues**. El registro en archivo no demuestra por sí solo un sistema de seguimiento. Falta registrar el defecto en el sistema acordado.

### T6-11 — Ciclos de corrección

| Ciclo | Defecto y prueba antes → después | Commit y evidencia |
|---|---|---|
| A | `I/E. CASA` se interpretaba como ubicación completa; prueba 0/1 → 1/1. | [fef8a86](https://github.com/Cr4ckJu4nF3/FOCCUS/commit/fef8a86010d09ea00c4dd0eb82b4c1b6ddd19ac0) · [rama y reproducción](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/fix/t6-ciclo-a/docs/agentes/T6_CICLO_IE.md) |
| B | `INTERNADO` se cortaba como modo `INT` y ubicación `ERNADO`; prueba 0/1 → 2/2, incluida compatibilidad añadida después. | [3a73e33](https://github.com/Cr4ckJu4nF3/FOCCUS/commit/3a73e33c77b05cb37973e89d4ae27530d0c222e6) · [rama y reproducción](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/fix/t6-ciclo-b/docs/agentes/T6_CICLO_LUGARES.md) |

Ambas ramas parten de `9126d8f` y afectan `guionEscenas.js`; no se integraron. Según informó el usuario, una integración resuelta y probada quedó **solo local, sin commit**, porque falla el lint general; no se presenta como integración publicada ni como corrección en producción. La evidencia T6 principal se publicó antes de estos ciclos y su frase sobre la falta de ciclos quedó desactualizada.

### T6-12 — README y API

El [README de la rama de evidencia](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/README.md#pruebas-y-evidencia-t6) contiene pruebas y módulos API. En el arranque simulado completo `/docs` y `/openapi.json` respondieron 200; se registraron 69 rutas. La colección usa aparte una API parcial de cuatro rutas. FOCCUS tiene un FastAPI con responsabilidades por routers: llamarlo «cuarto backend» es interpretación del equipo, **no una exención del instructor**. Falta validar esa interpretación y la API en instalación real de prueba.

### T6-13 — Historial de commits

El historial público muestra construcción [`feat(web)`](https://github.com/Cr4ckJu4nF3/FOCCUS/commit/7ff51433c5d85f577053f33636fd6c6d1483c2ac) y corrección [`fix(web)`](https://github.com/Cr4ckJu4nF3/FOCCUS/commit/2397a2b121bfe9367107a86a1d85ade52f5777c5). En adelante el equipo propone usar `feat`, `fix` o `docs` según el tipo de cambio; **no se promete un control automatizado**. No se demuestra asociación a incidencias, que la lista presenta como deseable.

### T6-14 — Lint y regresiones

**No aprobado:** `npm run lint` registró 14 errores, cero advertencias; la criticidad funcional individual es desconocida. No existe línea base T5 verificable, por lo que no se demuestra ausencia de regresiones. Los resultados de frontend (37 pruebas y build) provienen de un árbol con cambios no publicados y no deben atribuirse al commit base ni a la rama de evidencia. [Detalle](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/docs/agentes/T6_EVIDENCIA.md#ejecución-y-límites).

### T6-15 — Comparación y deuda

**Pausado.** Falta reunir antecedentes reales y acordar qué se compara entre los cuatro backends del programa. La deuda está priorizada abajo; no se inventa una comparación.

## Arquitectura y backend

```mermaid
flowchart LR
  W[Web React] -->|HTTP| API
  M[App Flutter] -.->|integración pendiente de verificar| API
  subgraph B["Un servicio FastAPI"]
    API[API y routers] --> L[Controladores y validación]
    L --> ORM[Persistencia]
  end
  ORM --> DB[(MySQL configurado)]
  L --> FS[Archivos locales]
  L --> MAIL[Correo]
```

Vista de componentes, no prueba de ejecución real. Una API compartida centraliza controles, pero un cambio puede afectar varios módulos y clientes. Ver [código del servicio](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/9126d8f/backend/api_usuarios/app/main.py).

## Recorrido propuesto de la demo

**Sin ejecución integral demostrada.** Usar datos ficticios y ambiente autorizado; no mostrar credenciales ni datos privados.

1. Verificar instalación y disponibilidad del entorno.
2. Iniciar sesión y completar 2FA cuando corresponda.
3. Abrir proyecto, dashboard, guion y crear una escena.
4. Mostrar galería, continuidad y rodaje, verificando persistencia.
5. Si móvil aún no está verificado, indicarlo como pendiente.
6. Explicar resultados parciales, defectos y límites.

No hacer depender la demo del catálogo de bloques con migración pendiente.

## Pendientes y deuda priorizada

1. **Alta:** instalación limpia; login y 2FA completos; demo con persistencia y ambiente MySQL de prueba aislado; terminar y probar móvil en T7.
2. **Alta:** analizar y resolver los 14 errores de lint, establecer criticidad y una referencia T5; repetir pruebas para regresiones.
3. **Alta:** resolver, publicar y probar la integración de las ramas de los dos ciclos; no asumir que ya están corregidos en producción.
4. **Alta:** crear el defecto en el sistema de seguimiento acordado; completar pruebas pendientes del [plan](plan-pruebas.md).
5. **Media:** completar las dos retrospectivas; aclarar con instructor el criterio de cuarto backend; retomar la comparación de cuatro backends.
6. **Media:** catálogo de bloques bloqueado por migración pendiente; Docker pausado. Evaluar recuperación de archivos locales y manejo compartido de errores HTTP.

## Fuentes

- [Lista oficial T6](https://github.com/ergrato-dev/checklist-proyectos-adso/blob/main/listas-de-chequeo/listas-oferta-abierta/t6/6t-lista-de-chequeo-oa.md).
- [Evidencia y reporte T6, rama independiente](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/docs/agentes/T6_EVIDENCIA.md); [README y matriz de esa misma rama](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/README.md#pruebas-y-evidencia-t6).
- [Ciclo A](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/fix/t6-ciclo-a/docs/agentes/T6_CICLO_IE.md) y [ciclo B](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/fix/t6-ciclo-b/docs/agentes/T6_CICLO_LUGARES.md): ramas independientes, no integradas.
- [Diagramas documentales existentes](https://github.com/Aerxs666/FOCCUS-RF/blob/50b8bd5/diagramas/README.md).
