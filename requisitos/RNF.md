# FOCCUS — Requisitos No Funcionales (RNF)

Propuestos a partir de lo que el proyecto ya hace. Verificar cada uno antes de exponerlo.

| ID | Categoría | Requisito | Estado |
|---|---|---|---|
| RNF-01 | Seguridad | Las contraseñas se guardan como hashes bcrypt y la sesión usa JWT firmado | ✅; la clave debe configurarse para un entorno persistente |
| RNF-02 | Seguridad | Las acciones de escritura de datos del proyecto exigen token válido y permiso por rol en el proyecto | ✅ web (código y pruebas aisladas de pertenencia recurso→proyecto; móvil y servicios reales no validados) |
| RNF-03 | Seguridad | Los secretos (`.env`, claves, backups) no deben subirse a git | Por verificar en cada cambio |
| RNF-04 | Seguridad | El JWT de acceso se entrega solo después de completar el 2FA | ✅ (web: 7/7 pruebas HTTP aisladas comunicadas; no prueba de correo o BD reales) |
| RNF-05 | Usabilidad | Texto mínimo de 12 px, foco visible y estados con acción (cargando, error, vacío) | 🟡 (solo algunos módulos) |
| RNF-06 | Usabilidad | Modo claro y oscuro en móvil | Estado histórico sin validar |
| RNF-07 | Compatibilidad | Web en navegadores modernos; móvil en Android (iOS sin probar) | 🟡 |
| RNF-08 | Rendimiento | Las listas principales cargan en menos de 3 s con la BD en la nube | por medir |
| RNF-09 | Disponibilidad | La base configurada debe estar disponible para los flujos que la necesitan | 🟡; comprobar el entorno antes de la demo |
| RNF-10 | Mantenibilidad | Backend en capas (routes → controllers → models) y API documentada en `/docs` | ✅; documentación observada en un arranque aislado, no en una instalación limpia completa |
| RNF-11 | Integridad | Los códigos únicos son inmutables y no se reutilizan | ✅ |
| RNF-12 | Respaldo | Crear y verificar respaldos antes de cambios estructurales | 🟡; no se ha demostrado para todos los cambios |
| RNF-13 | Almacenamiento | Archivos subidos en disco local (migrar a la nube) | 🔲 (backlog) |
