# Sustentación T6 — FOCCUS

Resumen del equipo para preparar la exposición; la calificación corresponde al instructor. Revisión: 22-11-2026. Las pruebas son parciales: no se ha demostrado una demo completa de inicio a fin.

Lista original: [15 criterios T6](https://github.com/ergrato-dev/checklist-proyectos-adso/blob/main/listas-de-chequeo/listas-oferta-abierta/t6/6t-lista-de-chequeo-oa.md).

## Matriz de estado y evidencia

| # | Criterio | Estado | Evidencia breve y qué falta |
|---|---|---|---|
| 01 | Cierre T6 y orientación T7 | ✅ | El equipo sitúa el cierre web en los cambios de guion, galería y panel; para T7 quedan móvil y los nuevos requisitos que se indiquen. Las pantallas de [guion](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/frontend/src/screen/Guion.jsx) y [proyecto](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/frontend/src/screen/ProjectDashboard.jsx) no prueban una demo completa. |
| 02 | Retrospectivas | ⏸ En proceso | El usuario indica que se están realizando; falta comprobar dos retrospectivas con reflexión sobre las pruebas. |
| 03 | Backend funcional y responsabilidades | ✅ | El usuario confirma que el backend arranca. [Cómo encenderlo y explicar sus responsabilidades](backend-y-recorrido.md). La lista original también pide diferenciarlas frente a los backends anteriores; su interpretación corresponde al instructor. |
| 04 | JWT, validación e instalación | ✅ | El usuario confirma el criterio; hay [pruebas aisladas](#comandos-para-repetir-las-pruebas) de JWT y validación. El agente no probó la instalación limpia ni el login real; falta evidencia reproducible. |
| 05 | Arquitectura y recorrido integral | ✅ | El usuario aprueba la arquitectura y el [recorrido explicado](backend-y-recorrido.md#recorrido-de-acceso-y-consulta-de-proyectos); la demo completa con API y persistencia no se ha demostrado. |
| 06 | Bonificación IoT | ➖ No se realiza | Decisión del equipo; no se presenta un prototipo. |
| 07 | Plan de pruebas | ✅ | [Plan aprobado por el usuario](plan-pruebas.md); aprobar el plan no significa que se hayan ejecutado todos los casos. |
| 08 | Casos de prueba | ✅ | 27 casos de seguridad y 9 de API registrados en la [evidencia pública](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/docs/agentes/T6_EVIDENCIA.md#matriz-complementaria-de-api-integrada). |
| 09 | Automatización y cobertura | ✅ | 93 % de sentencias de `auth.py`; Newman: 7/7 aserciones en una API parcial. No representa cobertura integral del producto. |
| 10 | Reporte y seguimiento de defectos | 🟡 Parcial | Hay [reporte](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/docs/agentes/T6_EVIDENCIA.md) y [registro en archivo](seguimiento-defectos.md), con severidad y estado. Falta confirmar si el instructor acepta el archivo como sistema de seguimiento; no se crearon GitHub Issues. |
| 11 | Ciclos de corrección | ✅ | Dos ciclos publicados: [A](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/fix/t6-ciclo-a/docs/agentes/T6_CICLO_IE.md) y [B](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/fix/t6-ciclo-b/docs/agentes/T6_CICLO_LUGARES.md). Ramas separadas, aún no integradas en `main`. |
| 12 | README y documentación de API | ✅ | El usuario aprueba el criterio. El [README](https://github.com/Cr4ckJu4nF3/FOCCUS/tree/docs/t6-evidencia-20261121#pruebas-y-evidencia-t6) incluye pruebas y rutas; `/openapi.json` documentó 69 rutas en arranque simulado, no una instalación limpia completa. |
| 13 | Historial de construcción y corrección | ✅ | Hay commits de tipo [`feat`](https://github.com/Cr4ckJu4nF3/FOCCUS/commit/7ff51433c5d85f577053f33636fd6c6d1483c2ac) y [`fix`](https://github.com/Cr4ckJu4nF3/FOCCUS/commit/2397a2b121bfe9367107a86a1d85ade52f5777c5). No se demuestra vínculo con issues. |
| 14 | Linter y regresiones T5 | ➖ No se realiza | Decisión del equipo. No se afirma una exención oficial ni que el criterio esté aprobado. |
| 15 | Comparación de backends y deuda | ✅ Alcance acordado | [Evolución del único backend y deuda priorizada](requisito-15.md). El usuario adapta la comparación a uno; la aceptación de esa adaptación por el instructor está pendiente. |

**Estados:** ✅ evidencia del entregable o confirmación del usuario, según se indique; 🟡 falta evidencia o aclaración para el criterio completo; ⏸ en proceso o pausado; ➖ el equipo decidió no realizarlo. No son calificaciones oficiales.

## Avances recientes y límites

- **Base de datos:** el registro local de `foccus-bd` indica que se aplicó `catalogo_bloques` en Aiven y se verificó su estructura por metadatos. El tercer respaldo previo se restauró y verificó; los otros dos no completaron esa comprobación. Este registro aún no está publicado.
- **Guion:** se informó una prueba de API real que guardó, recuperó y reinsertó cuatro tipos de bloques y editó una ficha. «Quitar de versión» se probó en borrador y se canceló. No demuestra el resto de los flujos.
- El usuario confirma uso de Aiven y escritura manual en el guion, sin resultados detallados por opción. La revisión visual sigue en curso con web; no se adelanta su resultado.

## Comandos para repetir las pruebas

Usar la rama publicada `docs/t6-evidencia-20261121`, abrir `backend/api_usuarios` y utilizar un entorno Python con las dependencias instaladas. Estos comandos no hacen una instalación limpia: las pruebas usan datos ficticios y dobles de prueba, sin conectarse a MySQL real ni leer `.env`.

**27 pruebas de JWT y validación:**

```text
python -B -m unittest -v tests.test_t6_seguridad_aislada
```

**Arranque aislado de FastAPI:**

```text
python -B -m unittest -v tests.test_t6_arranque_aislado
```

**Las 36 pruebas y cobertura de sentencias** (requiere `coverage` ya disponible en el entorno):

```text
python -m coverage run --source=app.utils.auth -m unittest -v tests.test_t6_seguridad_aislada tests.test_project_resource_ownership tests.test_projects_client_permissions
python -m coverage report -m
```

**Newman, API parcial local** (desde `backend/api_usuarios`, con Newman disponible; terminales separadas):

```text
# Terminal 1
python -m uvicorn tests.postman_app_aislada:app --host 127.0.0.1 --port 8765 --no-access-log

# Terminal 2
newman run tests/FOCCUS_T6.postman_collection.json --env-var baseUrl=http://127.0.0.1:8765 --reporters cli
```

El resultado registrado fue 36 pruebas aprobadas, 93 % de sentencias y 7/7 aserciones de Newman. El arranque simulado no comprueba MySQL, SMTP ni una instalación desde cero. La [evidencia publicada](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/docs/agentes/T6_EVIDENCIA.md#verificación-complementaria-22-11-2026) documenta un entorno virtual nuevo y la instalación de dependencias, no una instalación completa. El usuario confirma el criterio 4; esa confirmación no detalla una prueba reproducible de instalación completa.

## Evidencia requisito 5

### Arquitectura

El código reúne los routers en un solo servicio FastAPI. React es el cliente web; la integración móvil con la API queda pendiente de validar.

<!-- mermaid-checked: no \n, no em-dash/en-dash, no {} in labels, subgraphs are id["label"], arrows are -->|"label"|, all subgraphs closed by end, ids unique -->
```mermaid
flowchart LR
  U["Usuario"] --> W["Web React"]
  U -.-> M["App Flutter - validación pendiente"]
  W -->|"Solicitudes HTTP"| API
  M -.->|"API por validar"| API
  subgraph B["Un solo servicio FastAPI"]
    API["Autenticación y routers"]
  end
  API -->|"SQLAlchemy"| DB[("MySQL previsto")]
  API -->|"Guiones y fotos"| F["Archivos locales"]
  API -->|"Códigos y otros correos"| S["SMTP"]
```

1. **Presentación:** el usuario navega por [rutas y pantallas React](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/frontend/src/routes.jsx); [api.js](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/frontend/src/api.js) prepara solicitudes y añade el JWT cuando hay sesión.
2. **Servicio y seguridad:** [main.py](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/backend/api_usuarios/app/main.py) reúne los routers; [auth.py](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/backend/api_usuarios/app/utils/auth.py) valida el token en rutas protegidas.
3. **Datos:** [database.py](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/backend/api_usuarios/app/config/database.py) configura SQLAlchemy; MySQL es la infraestructura prevista, no probada por el arranque simulado.
4. **Archivos y correo:** [file_storage.py](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/backend/api_usuarios/app/utils/file_storage.py) maneja archivos locales y [mail.py](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/backend/api_usuarios/app/utils/mail.py) envía correos por SMTP.

### Flujo end-to-end de ejemplo

La app web tiene rutas para [login, verificación y módulos](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/frontend/src/routes.jsx). Este recorrido es una **visita de ejemplo**, no una secuencia obligatoria entre módulos ni evidencia de que se haya hecho una demo integral:

<!-- mermaid-checked: no \n, no em-dash/en-dash, no {} in labels, subgraphs are id["label"], arrows are -->|"label"|, all subgraphs closed by end, ids unique -->
```mermaid
flowchart LR
  L["Correo y contraseña"] --> V["Enviar y verificar código 2FA"]
  V -->|"Código válido"| P["Seleccionar proyecto"]
  P --> G["Guion"]
  G --> E["Escenas"]
  E --> C["Galería o continuidad"]
  C --> D["Desglose"]
  D --> R["Rodaje"]
```

1. **Acceso y 2FA:** [Login.jsx](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/frontend/src/screen/Login.jsx) solicita el acceso y el envío del código; [TwoFactor.jsx](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/frontend/src/screen/TwoFactor.jsx) lo verifica. Las [rutas](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/backend/api_usuarios/app/routes/user_routes.py) y el [controlador](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/backend/api_usuarios/app/controllers/user_controller.py) exigen 2FA en cada nuevo login exitoso y entregan el token tras verificar el código.
2. **Proyecto:** [ProjectSelection.jsx](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/frontend/src/screen/ProjectSelection.jsx) permite escoger un proyecto; las [rutas de proyecto](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/backend/api_usuarios/app/routes/project_routes.py) atienden las operaciones correspondientes.
3. **Guion y escenas:** las pantallas de [guion](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/frontend/src/screen/Guion.jsx) y [escenas](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/frontend/src/screen/Escena.jsx) se apoyan en sus rutas de [guion](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/backend/api_usuarios/app/routes/guion_routes.py) y [escenas](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/backend/api_usuarios/app/routes/escena_routes.py).
4. **Galería y continuidad:** [Galeria.jsx](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/frontend/src/screen/Galeria.jsx) muestra recursos del proyecto; el backend organiza las rutas de [galería](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/backend/api_usuarios/app/routes/galeria_routes.py) y [continuidad](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/backend/api_usuarios/app/routes/continuidad_routes.py).
5. **Desglose y rodaje:** [Desglose.jsx](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/frontend/src/screen/Desglose.jsx) consulta el desglose y [Rodaje.jsx](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/frontend/src/screen/Rodaje.jsx) gestiona rodajes; sus rutas están en [desglose](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/backend/api_usuarios/app/routes/desglose_routes.py) y [rodaje](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/02ffb2de7c123b5b228aa2e2df9298faf4278eca/backend/api_usuarios/app/routes/rodaje_routes.py).

**Alcance del 2FA:** no se encontró una excepción para dispositivos recordados. «Recordarme» afecta la duración y el almacenamiento de la sesión verificada; si esta sigue vigente, se puede reutilizar sin iniciar sesión de nuevo. Los tests ejecutados sustituyeron servicios reales; el diagrama no prueba persistencia ni una demo completa.

## Referencias

- [Plan de pruebas T6](plan-pruebas.md).
- [Evidencia T6 publicada en FOCCUS](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/docs/agentes/T6_EVIDENCIA.md).
- [Registro persistente de seguimiento de defectos](seguimiento-defectos.md).
- [README de la rama de evidencia](https://github.com/Cr4ckJu4nF3/FOCCUS/tree/docs/t6-evidencia-20261121).
- [Ciclo A](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/fix/t6-ciclo-a/docs/agentes/T6_CICLO_IE.md) y [ciclo B](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/fix/t6-ciclo-b/docs/agentes/T6_CICLO_LUGARES.md); ramas distintas, aún no integradas.
