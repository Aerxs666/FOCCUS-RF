# Requisito 15: comparación y deuda técnica

La [lista T6](https://github.com/ergrato-dev/checklist-proyectos-adso/blob/main/listas-de-chequeo/listas-oferta-abierta/t6/6t-lista-de-chequeo-oa.md) pide «Reflexión comparativa de los 4 backends del programa; deuda técnica documentada y priorizada».

**Estado: parcial.** Hay deuda priorizada abajo; no hay información suficiente para comparar los cuatro backends del programa. La prioridad es una propuesta para el equipo, no un compromiso de fecha o responsable.

## Lo que sí sabemos

En FOCCUS se identificó un servicio FastAPI, organizado en routers; [main.py](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/backend/api_usuarios/app/main.py) muestra su composición. No se identificaron aquí los otros backends del programa. Estos hitos son **cambios del proyecto**, no cuatro backends:

| Hito | Evidencia |
|---|---|
| Conexión del backend a MySQL | [Commit de conexión](https://github.com/Cr4ckJu4nF3/FOCCUS/commit/35c08f3). |
| Corrección del acceso y correo 2FA | [Commit de autenticación](https://github.com/Cr4ckJu4nF3/FOCCUS/commit/1e57fe6). |
| Catálogo y gestión de escenas | [Commit de catálogo](https://github.com/Cr4ckJu4nF3/FOCCUS/commit/60e43ad). |
| Entorno local con Docker | [Commit de Docker](https://github.com/Cr4ckJu4nF3/FOCCUS/commit/93d57e6). |

El usuario indica que Docker funciona. La [guía Docker](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/docs/DOCKER_LOCAL.md) registra pruebas anteriores de catálogo con MySQL local y datos ficticios. El entorno no configura SMTP ni crea automáticamente el catálogo en un volumen nuevo. Docker no demuestra por sí solo la comparación pedida ni una demo integral; no se ejecutaron pruebas nuevas en esta revisión.

## Deuda técnica priorizada

| Prioridad | Deuda y evidencia | Acción propuesta |
|---|---|---|
| Alta | **Recorrido integral:** las [pruebas T6](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/docs/agentes/T6_EVIDENCIA.md) registran cobertura parcial, no login, persistencia y cierre de sesión de principio a fin. | Ejecutar y registrar ese recorrido con datos ficticios en un ambiente autorizado. |
| Alta | **Móvil y contratos:** el [registro web](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/docs/agentes/CAMBIOS_WEB.md) señala adaptación de 2FA y otros cambios pendiente; aquí no se verificó la rama móvil. | Contrastar la versión móvil vigente y probar login y contratos con la API. |
| Alta | **Docker local:** la [guía](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/docs/DOCKER_LOCAL.md#limitaciones-importantes) indica que SMTP no está configurado y que un volumen nuevo no incluye la migración del catálogo. | Definir un correo de prueba seguro y coordinar con BD una migración local verificable. |
| Media | **Dependencias:** varias no tienen versión fijada en [requirements.txt](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/backend/api_usuarios/requirements.txt); una instalación posterior puede resolver versiones distintas. | Fijar y probar versiones de forma coordinada. |
| Media | **Archivos:** [file_storage.py](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/backend/api_usuarios/app/utils/file_storage.py) guarda archivos en disco local; su disponibilidad depende de ese almacenamiento. | Definir y probar una estrategia de persistencia y recuperación. |

Se priorizan primero las brechas que impiden demostrar o integrar el producto; después, la reproducibilidad y la conservación de archivos.

## Información necesaria para completar la comparación

**Pregunta al equipo:** ¿cuáles son los cuatro backends del programa y cuál corresponde a FOCCUS? Compartan para cada uno el nombre, repositorio o entrega, tecnología y responsabilidad principal. Con eso se puede comparar propósito, tecnología, datos, seguridad y pruebas.

Si no existen cuatro implementaciones distintas, consultar al instructor si acepta comparar **cuatro etapas comprobables del mismo backend** o sus responsabilidades. Son alternativas de presentación, no equivalencias ya aprobadas ni evidencia de cuatro backends.
