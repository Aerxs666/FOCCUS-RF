# Plan de pruebas T6 — FOCCUS

**Aprobado expresamente por el usuario.** La aprobación corresponde al plan, no a los resultados pendientes ni al jurado. El [estado de la lista y la evidencia](README.md) se mantienen por separado.

## Objetivo y alcance

Comprobar el comportamiento y los permisos de acceso, proyectos, guiones y escenas, galería y continuidad, y rodaje. La aplicación móvil está **pendiente** y se terminará y probará para T7. Priorizar recorridos representativos, sin afirmar cobertura total ni ausencia de defectos.

## Niveles y tipos

1. **Unitarias:** validación, reglas, JWT y permisos aislados.
2. **API integrada:** solicitudes con persistencia de prueba, vínculos entre recursos y separación entre proyectos.
3. **Navegador:** interacción web y recorridos end-to-end con login y persistencia cuando esté listo el ambiente.

En cada nivel incluir casos positivos, negativos y de permisos. Registrar también la versión o rama, fecha, entorno, alcance y limitaciones.

## Ambiente y datos

- Ambiente aislado del desarrollo y de producción, con base de datos y archivos de prueba separados; emplear únicamente datos ficticios. No usar credenciales, correos, archivos ni datos reales.
- Como objetivo, usar **MySQL de prueba aislado** para validar el comportamiento de la infraestructura prevista.
- Mientras no esté disponible, usar **SQLite temporal y simulaciones** para los casos compatibles. Sus diferencias frente a MySQL y los servicios reales constituyen una **brecha de fidelidad**: un éxito allí no demuestra que MySQL o la infraestructura real funcionen.
- Los recorridos estáticos sin API ni persistencia solo verifican navegación y protección visual limitada; no reemplazan un flujo integral.

## Diseño y registro de casos

Mantener **al menos 20 casos** con identificador, datos ficticios, pasos reproducibles, resultado esperado, resultado obtenido y estado. Cubrir los tipos y módulos anteriores; la cifra mínima no demuestra cobertura completa. La [matriz ya ejecutada de 27 casos](README.md#t6-08--matriz-de-27-casos) satisface la cantidad y se complementa con [9 casos de API](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/docs/agentes/T6_EVIDENCIA.md#matriz-complementaria-de-api-integrada).

| Área | Cobertura registrada y próximos casos |
|---|---|
| Acceso y permisos | JWT, validaciones y permisos entre proyectos ejecutados aisladamente; pendiente login y 2FA completos. |
| Proyectos | Lista y edición con límites por proyecto en API aislada; pendiente recorrido integral con persistencia real de prueba. |
| Guiones y escenas | Acceso y mutaciones entre proyectos; dos ciclos de analizador en ramas separadas. Pendiente crear escena desde guion en flujo integral. |
| Galería y continuidad | Continuidad y foto simulada parcialmente probadas; pendiente flujo propio de galería con archivos de prueba. |
| Rodaje | Edición de proceso en API aislada; pendiente recorrido completo en navegador. |
| Móvil | Pendiente: definir y ejecutar casos una vez terminada la adaptación. |

No se inventan pasos ni resultados de casos aún no diseñados o ejecutados. Al prepararlos, añadirlos a una matriz con datos, pasos y resultados reales.

## Criterios de ejecución y aceptación

1. Preparar el ambiente aislado y los datos ficticios; registrar versión y dependencias.
2. Ejecutar cada caso y registrar su resultado real, incluido error o bloqueo.
3. **Aprobado** solo si el resultado obtenido coincide con el esperado. Una prueba no ejecutada queda **pendiente**, no aprobada; si el entorno impide ejecutarla, registrar el bloqueo.
4. Reportar fecha, versión, ambiente, conteos de aprobados/fallidos/bloqueados/pendientes y límites. No sumar pruebas distintas como si fueran un flujo end-to-end.
5. Registrar cada defecto reproducible con identificador, pasos, esperado, obtenido, severidad y estado; usar el sistema de seguimiento acordado cuando esté disponible. Después de corregir, vincular commit, repetir el caso y registrar resultado.

## Estado al cierre de esta documentación

La [evidencia pública](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/docs/agentes/T6_EVIDENCIA.md) registra 36 pruebas backend, ejecución de Newman y 2 recorridos de navegador estáticos; **no se ha ejecutado todo este plan**. Faltan, entre otros, MySQL aislado, instalación limpia, login completo, recorrido de galería y demo con persistencia, y pruebas móviles. El reporte registra un defecto con severidad y estado en archivo; aún no se ha demostrado un sistema de seguimiento mediante issues.
