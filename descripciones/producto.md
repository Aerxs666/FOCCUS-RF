# Descripción del producto

**FOCCUS** es una plataforma para la gestión de continuidad en producciones audiovisuales (cine, series, comerciales). Es un proyecto estudiantil de Camilo (Aerxs666) y Juan (Cr4ckJu4nF3).

## Problema

En un rodaje, la misma escena se graba en días distintos. Si el vestuario, los objetos o el espacio cambian entre tomas, se rompe la continuidad. FOCCUS centraliza guion, escenas, fotos y cronograma para evitarlo.

## Módulos

| Módulo | Para qué sirve |
|---|---|
| Autenticación | Registro, login, 2FA por correo, recuperación e invitaciones |
| Proyectos y clientes | Organiza cada producción y la empresa que la encarga |
| Equipo y roles | Quién participa y qué puede hacer |
| Guion | Guion versionado, por bloques con formato de la industria, PDF y notas |
| Escenas | División del guion y continuidad por escena |
| Galería | Personajes, lugares, objetos y vestuario con versiones y fotos |
| Desglose | Requerimientos de cada escena para planear el rodaje |
| Rodaje | Cronograma por jornadas con escenas y procesos |
| Códigos y buscador | Código único por elemento y búsqueda (solo admin) |
| App móvil | Consulta y edición desde el celular (Flutter) |

## Roles

- **Administrador** (`id_rol` 1001 en el proyecto): crea, edita, borra, invita, ve códigos.
- **Miembro**: consulta y aporta según permisos.
- **Visitante**: solo landing, registro y contacto.

## Códigos únicos

Formato `TIPO-001`, consecutivo por proyecto y tipo, generado por el backend, inmutable y no reutilizable. Solo lo ve el administrador.

| Prefijo | Elemento | Prefijo | Elemento |
|---|---|---|---|
| PRO | Proyecto | PER | Personaje |
| GUI | Guion | LOC | Lugar |
| VGU | Versión de guion | OBJ | Objeto |
| ESC | Escena | VES | Vestuario |
| DRO | Jornada de rodaje | | |

## Tecnología

Backend FastAPI + SQLAlchemy + MySQL (Aiven); frontend React 19 + Vite; móvil Flutter. Código en https://github.com/Cr4ckJu4nF3/FOCCUS.

## Glosario

- **Continuidad:** que lo visible en una escena (ropa, objetos, lugar) sea coherente entre tomas.
- **Desglose:** lista de lo que cada escena necesita (personajes, utilería, vestuario...).
- **Jornada de rodaje:** un día de grabación.
- **Bloque de guion:** unidad con formato propio (escena, acción, personaje, diálogo, paréntesis, transición).
- **RF / RNF / HU:** requisito funcional / no funcional / historia de usuario.
