## RF-01 — Registro de empresa y administrador

```sql
SELECT c.id_cliente, c.razon_social, u.id_user, u.id_rol FROM clients c JOIN users u ON u.id_client = c.id_cliente WHERE c.razon_social = 'EMPRESA_DE_PRUEBA' AND u.id_user = 999999;
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
SELECT u.id_user, up.id_project, up.id_rol FROM users u LEFT JOIN user_projects up ON up.id_user = u.id_user AND up.id_project = 'PROYECTO_DESECHABLE' WHERE u.id_user = 999999;
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
SELECT c.id_cliente, c.razon_social, p.id_project FROM clients c LEFT JOIN projects p ON p.id_client = c.id_cliente WHERE c.id_cliente = 999999;
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
SELECT tipo, entidad_id, codigo FROM codigos_entidad WHERE id_project = 'PROYECTO_DESECHABLE';
```

## RF-12 — Roles fijos

```sql
SELECT id_user, id_project, id_rol FROM user_projects WHERE id_project = 'PROYECTO_PRUEBA' AND id_user = 999999;
```

## RF-13 — Crear guion

```sql
SELECT g.id_guion, g.nombre, g.id_guion_version_actual, v.id_guion_version, v.numero_de_version FROM guion g LEFT JOIN guion_version v ON v.id_guion = g.id_guion WHERE g.id_project = 'PROYECTO_PRUEBA' AND g.id_guion = 999999;
```

## RF-14 — Versiones del guion

```sql
SELECT g.id_guion, g.id_guion_version_actual, v.id_guion_version, v.numero_de_version FROM guion g JOIN guion_version v ON v.id_guion = g.id_guion WHERE g.id_guion = 999999 ORDER BY v.numero_de_version;
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
SELECT v.id_escena_version, v.id_escena, v.numero_version, f.id_foto, f.tipo FROM escena_version v LEFT JOIN continuidad_foto f ON f.id_escena_version = v.id_escena_version WHERE v.id_escena = 'ESCENA_PRUEBA';
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
SELECT i.id_galeria, i.tipo, i.categoria, v.id_version, v.numero_version, f.id_foto FROM galeria_items i LEFT JOIN galeria_versiones v ON v.id_galeria = i.id_galeria LEFT JOIN galeria_version_fotos f ON f.id_version = v.id_version WHERE i.id_project = 'PROYECTO_PRUEBA' AND i.id_galeria = 999999;
```

## RF-23 — Vincular galería a escena

```sql
SELECT id_escena, id_galeria FROM escena_galeria_items WHERE id_escena = 'ESCENA_PRUEBA' AND id_galeria = 999999;
SELECT id_version, id_galeria, id_escena FROM galeria_versiones WHERE id_escena = 'ESCENA_PRUEBA' AND id_galeria = 999999;
```

## RF-24 — Desglose e importación

```sql
SELECT e.id_escena, e.id_desglose, r.id_requerimiento, r.departamento, r.etiqueta, r.cantidad FROM escenas e LEFT JOIN desglose_requerimientos r ON r.id_desglose = e.id_desglose WHERE e.id_escena = 'ESCENA_PRUEBA';
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
SELECT ambito, tipo, entidad_id, codigo FROM codigos_entidad WHERE id_project = 'PROYECTO_PRUEBA';
SELECT ambito, codigo, COUNT(*) AS repeticiones FROM codigos_entidad WHERE id_project = 'PROYECTO_PRUEBA' GROUP BY ambito, codigo HAVING COUNT(*) > 1;
```

## RF-29 — Códigos solo para administrador

```sql
-- No se comprueba mediante SQL.
```

## RF-30 — Buscar por código

```sql
SELECT tipo, entidad_id, codigo FROM codigos_entidad WHERE id_project = 'PROYECTO_PRUEBA' AND codigo = 'ESC-001';
```
