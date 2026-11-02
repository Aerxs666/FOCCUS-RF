# Diagramas

Todos en Mermaid: GitHub los dibuja solo.

## Casos de uso

```mermaid
flowchart LR
  V([Visitante]) --> A1[Registrarse]
  V --> A2[Contacto]
  M([Miembro]) --> B1[Iniciar sesión y 2FA]
  M --> B2[Ver guion y escenas]
  M --> B3[Consultar galería y desglose]
  M --> B4[Ver cronograma de rodaje]
  AD([Administrador]) --> B1
  AD --> C1[Invitar y quitar usuarios]
  AD --> C2[Gestionar clientes y proyectos]
  AD --> C3[Crear y versionar guiones]
  AD --> C4[Gestionar escenas, galería y rodaje]
  AD --> C5[Ver códigos y buscar por código]
```

## Arquitectura

```mermaid
flowchart LR
  W[Web React + Vite] -->|HTTP JSON + JWT| API[FastAPI]
  F[App Flutter] -->|HTTP JSON + JWT| API
  API --> DB[(MySQL Aiven)]
  API --> FS[Archivos subidos en disco]
  API --> SMTP[Gmail SMTP]
```

## Entidad-relación (simplificado)

```mermaid
erDiagram
  clients ||--o{ projects : tiene
  projects ||--o{ user_projects : miembros
  users ||--o{ user_projects : participa
  projects ||--o{ guion : contiene
  guion ||--o{ guion_version : versiones
  guion ||--o{ escenas : se_divide
  projects ||--o{ personajes : tiene
  projects ||--o{ escenarios : tiene
  projects ||--o{ galeria_items : galeria
  galeria_items ||--o{ galeria_versiones : versiones
  projects ||--o{ rodaje : jornadas
  escenas ||--o{ desglose : desglose
  projects ||--o{ codigos_entidad : codigos
```

## Secuencia: inicio de sesión con 2FA

```mermaid
sequenceDiagram
  actor U as Usuario
  participant W as Web/Móvil
  participant A as API
  participant M as Correo
  U->>W: correo y contraseña
  W->>A: POST /users/login
  A-->>W: token
  W->>A: POST /users/2fa/send
  A->>M: código de un solo uso
  U->>W: código
  W->>A: POST /users/2fa/verify
  A-->>W: acceso
```

## Secuencia: buscar por código (admin)

```mermaid
sequenceDiagram
  actor AD as Administrador
  participant W as Web/Móvil
  participant A as API
  participant D as BD
  AD->>W: escribe ESC-003
  W->>A: GET /projects/{id}/buscar-codigo?q=ESC-003
  A->>A: valida rol 1001 (403 si no)
  A->>D: busca en codigos_entidad
  D-->>A: tipo, id, código
  A-->>W: resultados
  W-->>AD: abre la ficha
```
