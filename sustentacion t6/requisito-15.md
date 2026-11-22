# Requisito 15: comparación y deuda técnica

La [lista T6](https://github.com/ergrato-dev/checklist-proyectos-adso/blob/main/listas-de-chequeo/listas-oferta-abierta/t6/6t-lista-de-chequeo-oa.md) pide «Reflexión comparativa de los 4 backends del programa; deuda técnica documentada y priorizada».

**Estado: ✅ alcance acordado con el usuario.** El usuario indica que siempre trabajaron con un solo backend y pide comparar su evolución. Se presenta esa adaptación, sin afirmar que el instructor haya aceptado cambiar el criterio original. La deuda está priorizada como propuesta, sin fechas ni responsables acordados.

## Comparación histórica: un backend

El usuario identifica [RACCORD Alpha](https://github.com/Aerxs666/RACCORD-ALPHA-.0.0.1) como antecedente. La comparación usa su estado publicado y el historial de FOCCUS; son etapas del proyecto, **no cuatro servicios**.

| Aspecto | Antes | Hoy |
|---|---|---|
| Servidor | RACCORD Alpha usaba [Flask y rutas de autenticación](https://github.com/Aerxs666/RACCORD-ALPHA-.0.0.1/blob/826c92232a2562218e95ecf27551ddf17ce84fa3/backend/app.py). El [primer FOCCUS](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/368ace4304c0fc6daec1085dc5347268941b72bb/backend/api_usuarios/app/main.py) ya usaba FastAPI. | Un [servicio FastAPI](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/backend/api_usuarios/app/main.py) reúne los routers. |
| Datos | El antecedente incluía el conector de PostgreSQL en sus [dependencias](https://github.com/Aerxs666/RACCORD-ALPHA-.0.0.1/blob/826c92232a2562218e95ecf27551ddf17ce84fa3/backend/requirements.txt). El segundo commit de FOCCUS registra la [conexión a MySQL](https://github.com/Cr4ckJu4nF3/FOCCUS/commit/35c08f3). | [SQLAlchemy y MySQL](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/backend/api_usuarios/app/config/database.py) conectan el servicio con la base configurada. |
| Acceso | Alpha incluía JWT y protegía el perfil; ver sus [rutas de autenticación](https://github.com/Aerxs666/RACCORD-ALPHA-.0.0.1/blob/826c92232a2562218e95ecf27551ddf17ce84fa3/backend/routes/auth.py). En el [primer FOCCUS](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/368ace4304c0fc6daec1085dc5347268941b72bb/backend/api_usuarios/app/routes/user_routes.py), la ruta de proyectos por usuario no declaraba una dependencia JWT. | La [ruta actual](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/backend/api_usuarios/app/routes/user_routes.py) exige usuario autenticado y verifica su identidad. El [recorrido](backend-y-recorrido.md#recorrido-de-acceso-y-consulta-de-proyectos) explica 2FA y JWT. |
| Funcionalidad | El primer FOCCUS reunía rutas de usuarios, clientes, proyectos, roles y contacto. | Se añadieron guion, escenas, galería, rodaje y otros routers; el [catálogo](https://github.com/Cr4ckJu4nF3/FOCCUS/commit/60e43ad) es un cambio posterior. |
| Entorno | En la versión inicial de FOCCUS revisada no se encontró el montaje Docker actual. | El [commit Docker](https://github.com/Cr4ckJu4nF3/FOCCUS/commit/93d57e6) incorporó un entorno local para web, API y MySQL. |

**Reflexión:** la evolución pasó de un backend centrado en autenticación a uno con más funciones de producción y controles de acceso. El aumento de alcance también exige más pruebas de integración y coordinación entre web, móvil y base de datos. Estos enlaces describen código y cambios; no prueban por sí solos todo el funcionamiento.

El usuario indica que Docker funciona. La [guía Docker](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/docs/DOCKER_LOCAL.md#aplicación-al-volumen-compose-de-esta-instalación-22-11-2026) registra pruebas anteriores del catálogo con datos ficticios y MySQL local: HTTP 200 al guardar y listar, 403 sin permiso y 401 sin JWT. El entorno no configura SMTP ni crea automáticamente el catálogo en un volumen nuevo. Docker no demuestra por sí solo la comparación pedida ni una demo integral; no se ejecutaron pruebas nuevas en esta revisión.

## Deuda técnica priorizada

| Prioridad | Deuda y evidencia | Acción propuesta |
|---|---|---|
| Alta | **Recorrido integral:** las [pruebas T6](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/docs/t6-evidencia-20261121/docs/agentes/T6_EVIDENCIA.md) registran cobertura parcial, no login, persistencia y cierre de sesión de principio a fin. | Ejecutar y registrar ese recorrido con datos ficticios en un ambiente autorizado. |
| Alta | **Móvil y contratos:** el [registro web](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/docs/agentes/CAMBIOS_WEB.md) señala adaptación de 2FA y otros cambios pendiente; aquí no se verificó la rama móvil. | Contrastar la versión móvil vigente y probar login y contratos con la API. |
| Alta | **Docker local:** la [guía](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/docs/DOCKER_LOCAL.md#limitaciones-importantes) indica que SMTP no está configurado y que un volumen nuevo no incluye la migración del catálogo. | Definir un correo de prueba seguro y coordinar con BD una migración local verificable. |
| Media | **Dependencias:** varias no tienen versión fijada en [requirements.txt](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/backend/api_usuarios/requirements.txt); una instalación posterior puede resolver versiones distintas. | Fijar y probar versiones de forma coordinada. |
| Media | **Archivos:** [file_storage.py](https://github.com/Cr4ckJu4nF3/FOCCUS/blob/cc96590fcb5ce8e1c063110c0b3beb6ecbe89e25/backend/api_usuarios/app/utils/file_storage.py) guarda archivos en disco local; su disponibilidad depende de ese almacenamiento. | Definir y probar una estrategia de persistencia y recuperación. |

Se priorizan primero las brechas que impiden demostrar o integrar el producto; después, la reproducibilidad y la conservación de archivos.

## Validación pendiente

Confirmar con el instructor si acepta comparar la evolución de un solo backend frente al texto original de cuatro. La aprobación del usuario no equivale a aprobación del jurado.
