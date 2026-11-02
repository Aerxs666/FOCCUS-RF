# FOCCUS — Requisitos No Funcionales (RNF)

Propuestos a partir de lo que el proyecto ya hace. Verificar cada uno antes de exponerlo.

| ID | Categoría | Requisito | Estado |
|---|---|---|---|
| RNF-01 | Seguridad | Las contraseñas se guardan cifradas (bcrypt) y la sesión usa JWT firmado con `JWT_SECRET_KEY` | ✅ |
| RNF-02 | Seguridad | Las acciones de escritura exigen token válido y permiso por rol en el proyecto | ✅ |
| RNF-03 | Seguridad | Los secretos (`.env`, claves, backups) no se suben a git | ✅ |
| RNF-04 | Seguridad | El token no debería servir hasta completar el 2FA | 🔲 (backlog) |
| RNF-05 | Usabilidad | Texto mínimo de 12 px, foco visible y estados con acción (cargando, error, vacío) | 🟡 (solo algunos módulos) |
| RNF-06 | Usabilidad | Modo claro y oscuro en móvil | ✅ |
| RNF-07 | Compatibilidad | Web en navegadores modernos; móvil en Android (iOS sin probar) | 🟡 |
| RNF-08 | Rendimiento | Las listas principales cargan en menos de 3 s con la BD en la nube | por medir |
| RNF-09 | Disponibilidad | La BD en el plan gratis de Aiven puede apagarse; el backend no arranca sin ella | 🟡 |
| RNF-10 | Mantenibilidad | Backend en capas (routes → controllers → models) y API documentada en `/docs` | ✅ |
| RNF-11 | Integridad | Los códigos únicos son inmutables y no se reutilizan | ✅ |
| RNF-12 | Respaldo | Backups de la BD con fecha antes de cada cambio estructural | ✅ |
| RNF-13 | Almacenamiento | Archivos subidos en disco local (migrar a la nube) | 🔲 (backlog) |
