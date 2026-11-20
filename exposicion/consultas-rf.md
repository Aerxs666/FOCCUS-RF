## RF-01 — Registro de empresa y administrador

```sql
SELECT id_cliente, razon_social FROM clients WHERE razon_social = 'EMPRESA_DE_PRUEBA';
SELECT id_user, id_client, id_rol FROM users WHERE id_user = 999999;
```

## RF-02 — Inicio de sesión

```sql
-- No se comprueba mediante SQL.
```

## RF-03 — Verificación por correo

```sql
-- No se comprueba mediante SQL.
```

## RF-04 — Recuperación de acceso

```sql
-- No se comprueba mediante SQL.
```

## RF-05 — Invitar miembro

```sql
SELECT id_user, id_project, id_rol FROM user_projects WHERE id_project = 'PROYECTO_PRUEBA' AND id_user = 999999;
```

## RF-06 — Permisos de escritura y consulta

```sql
-- No se comprueba mediante SQL.
```

## RF-07 — Retirar miembro

```sql
-- Antes y después, con IDs desechables.
SELECT id_user FROM users WHERE id_user = 999999;
SELECT id_user, id_project, id_rol FROM user_projects WHERE id_user = 999999 AND id_project = 'PROYECTO_DESECHABLE';
```

## RF-08 — Eliminar cuenta

```sql
-- Antes y después, con ID desechable.
SELECT id_user FROM users WHERE id_user = 999999;
SELECT id_user, id_project FROM user_projects WHERE id_user = 999999;
```

## RF-09 — Gestionar empresas

```sql
-- Antes y después, con ID desechable.
SELECT id_cliente, razon_social FROM clients WHERE id_cliente = 999999;
SELECT id_project, id_client FROM projects WHERE id_client = 999999;
```

## RF-10 — Gestionar proyectos

```sql
-- Antes y después, con ID desechable.
SELECT id_project, project_name, id_client, sinopsis FROM projects WHERE id_project = 'PROYECTO_DESECHABLE';
```

## RF-11 — Eliminar proyecto y dependencias

```sql
-- Antes y después, con IDs desechables.
SELECT id_project FROM projects WHERE id_project = 'PROYECTO_DESECHABLE';
SELECT id_user, id_project FROM user_projects WHERE id_project = 'PROYECTO_DESECHABLE';
SELECT id_guion, id_project FROM guion WHERE id_project = 'PROYECTO_DESECHABLE';
SELECT id_guion_version, id_guion FROM guion_version WHERE id_guion = 999999;
SELECT id_escena, id_guion FROM escenas WHERE id_guion = 999999;
SELECT id_rodaje, id_project FROM rodaje WHERE id_project = 'PROYECTO_DESECHABLE';
SELECT id_proceso, id_rodaje FROM proceso_rodaje WHERE id_rodaje = 'RODAJE_DESECHABLE';
SELECT id_galeria, id_project FROM galeria_items WHERE id_project = 'PROYECTO_DESECHABLE';
SELECT id_version, id_galeria FROM galeria_versiones WHERE id_galeria = 999999;
SELECT * FROM codigos_entidad WHERE id_project = 'PROYECTO_DESECHABLE';
```

## RF-12 — Roles fijos

```sql
SELECT id_user, id_project, id_rol FROM user_projects WHERE id_project = 'PROYECTO_PRUEBA' AND id_user = 999999;
```

## RF-13 — Crear guion

```sql
SELECT id_guion, nombre, id_guion_version_actual FROM guion WHERE id_project = 'PROYECTO_PRUEBA' AND id_guion = 999999;
SELECT id_guion_version, id_guion, numero_de_version FROM guion_version WHERE id_guion = 999999;
```

## RF-14 — Versiones del guion

```sql
SELECT id_guion, id_guion_version_actual FROM guion WHERE id_guion = 999999;
SELECT id_guion_version, id_guion, numero_de_version FROM guion_version WHERE id_guion = 999999;
```

## RF-15 — Notas de versión

```sql
SELECT id_nota, id_guion_version, id_user FROM guion_nota WHERE id_guion_version = 999999;
```

## RF-16 — Eliminar guion

```sql
-- Antes y después, con IDs desechables.
SELECT id_guion FROM guion WHERE id_guion = 999999;
SELECT id_guion_version, id_guion FROM guion_version WHERE id_guion = 999999;
SELECT id_nota, id_guion_version FROM guion_nota WHERE id_guion_version = 999999;
SELECT id_escena, id_guion FROM escenas WHERE id_guion = 999999;
SELECT id_escena_version, id_escena FROM escena_version WHERE id_escena = 'ESC_DESECHABLE';
SELECT id_galeria, id_guion, id_escena FROM galeria_items WHERE id_galeria = 999999;
```

## RF-17 — Escenas

```sql
SELECT id_escena, id_guion, numero_de_escena, encabezado FROM escenas WHERE id_guion = 999999;
```

## RF-18 — Continuidad visual

```sql
SELECT id_escena_version, id_escena, numero_version FROM escena_version WHERE id_escena = 'ESCENA_PRUEBA';
SELECT id_foto, id_escena_version, tipo FROM continuidad_foto WHERE id_escena_version = 999999;
```

## RF-19 — Cronograma

```sql
SELECT id_rodaje, id_project, nombre, fecha_inicio, estado FROM rodaje WHERE id_project = 'PROYECTO_PRUEBA';
```

## RF-20 — Procesos del rodaje

```sql
-- Antes y después, con ID desechable si se comprueba un borrado.
SELECT id_proceso, id_rodaje, nombre, fecha, estado FROM proceso_rodaje WHERE id_rodaje = 'RODAJE_DESECHABLE' AND id_proceso = 999999;
```

## RF-21 — Contacto público

```sql
-- No se comprueba mediante SQL.
```

## RF-22 — Galería

```sql
SELECT id_galeria, tipo, categoria FROM galeria_items WHERE id_project = 'PROYECTO_PRUEBA' AND id_galeria = 999999;
SELECT id_version, id_galeria, numero_version FROM galeria_versiones WHERE id_galeria = 999999;
SELECT id_foto, id_version FROM galeria_version_fotos WHERE id_version = 999999;
```

## RF-23 — Vincular galería a escena

```sql
SELECT id_escena, id_galeria FROM escena_galeria_items WHERE id_escena = 'ESCENA_PRUEBA' AND id_galeria = 999999;
SELECT id_version, id_galeria, id_escena FROM galeria_versiones WHERE id_escena = 'ESCENA_PRUEBA' AND id_galeria = 999999;
```

## RF-24 — Desglose e importación

```sql
SELECT id_escena, id_desglose FROM escenas WHERE id_escena = 'ESCENA_PRUEBA';
SELECT id_requerimiento, id_desglose, departamento, etiqueta, cantidad FROM desglose_requerimientos WHERE id_desglose = 'DESGLOSE_PRUEBA';
```

## RF-25 — Escenas en jornadas

```sql
SELECT id_escena, id_guion, id_rodaje FROM escenas WHERE id_escena = 'ESCENA_PRUEBA' AND id_guion = 999999;
```

## RF-26 — Bloques tipados

```sql
-- No se comprueba mediante SQL.
```

## RF-27 — Exportar PDF

```sql
-- No se comprueba mediante SQL.
```

## RF-28 — Códigos únicos

```sql
SELECT * FROM codigos_entidad WHERE id_project = 'PROYECTO_PRUEBA';
```

## RF-29 — Códigos solo para administrador

```sql
-- No se comprueba mediante SQL.
```

## RF-30 — Buscar por código

```sql
SELECT tipo, entidad_id, codigo FROM codigos_entidad WHERE id_project = 'PROYECTO_PRUEBA' AND codigo = 'ESC-001';
```
